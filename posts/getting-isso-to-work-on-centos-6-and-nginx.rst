.. title: Getting Isso to work on CentOS 6 and nginx
.. slug: getting-isso-to-work-on-centos-6-and-nginx
.. date: 2015-11-21 17:07:31+01:00
.. tags: isso, centos, nginx
.. category:
.. link:
.. description:
.. type: text

`Isso <https://posativ.org/isso/>`_ is an open source alternative to Disqus.
Users can post anonymous comments and everything is stored in an SQLite database
on your server.

The server is written in Python and the client is pure JavaScript.

Warning: this post explains how I got Isso to work on my server, this is not
aimed to be a reference guide! There probably are some installation procedures
to improve and maybe some bugs to report.

Installation
============

They provide prebuilt packages for most GNU/Linux distributions but,
unfortunately, not for CentOS (which is powering my VPS). So I had to install
Isso with pip.

First install virtualenv, Python development headers, SQLite and C compiler with
yum:

.. code:: console

    # yum install python-setuptools python-virtualenv python-devel sqlite
    # yum groupinstall "Development tools"

Then create a new directory in /opt and chown it to your user and group:

.. code:: console

    # mkdir /opt/isso
    # chown <user>:<group> /opt/isso

Activate virtualenv as regular user:

.. code:: console

    $ virtualenv /opt/isso
    $ source /opt/isso/bin/activate

We can now install Isso with pip:

.. code:: console

    $ pip install isso

*Optional*:

Note that I encountered some problems while installing the isso package.

First, the :code:`libffi` package was not found by misaka (an isso dependency),
I had to install :code:`libffi-devel`:

.. code:: console

    # yum install libffi-devel

Then, the current version of the misaka package needed by isso wouldn't build,
so I had to force the installation of a previous version. This will probably
soon be fixed, but just in case, this is what I did:

.. code:: console

    $ pip install misaka==1.0.2

I also had to install :code:`argparse`:

.. code:: console

    $ pip install argparse

And finally, this exception appeared when running the server:

.. code::

    Exception happened during processing of request from ('127.0.0.1', 55431)
    Traceback (most recent call last):
      File "/usr/lib64/python2.6/SocketServer.py", line 570, in process_request_thread
        self.finish_request(request, client_address)
      File "/usr/lib64/python2.6/SocketServer.py", line 332, in finish_request
        self.RequestHandlerClass(request, client_address, self)
      File "/usr/lib64/python2.6/SocketServer.py", line 627, in __init__
        self.handle()
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/serving.py", line 217, in handle
        rv = BaseHTTPRequestHandler.handle(self)
      File "/usr/lib64/python2.6/BaseHTTPServer.py", line 329, in handle
        self.handle_one_request()
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/serving.py", line 252, in handle_one_request
        return self.run_wsgi()
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/serving.py", line 201, in run_wsgi
        traceback = get_current_traceback(ignore_system_exceptions=True)
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/debug/tbtools.py", line 184, in get_current_traceback
        tb = Traceback(exc_type, exc_value, tb)
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/debug/tbtools.py", line 235, in __init__
        self.frames.append(Frame(exc_type, exc_value, tb))
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/debug/tbtools.py", line 402, in __init__
        self.filename = to_unicode(fn, get_filesystem_encoding())
      File "/opt/isso/lib/python2.6/site-packages/werkzeug/filesystem.py", line 62, in get_filesystem_encoding
        'filesystem encoding instead of {!r}'.format(rv),
    ValueError: zero length field name in format

I just removed the line 62 in
:code:`/opt/isso/lib/python2.6/site-packages/werkzeug/filesystem.py`. Dirty as
hell, but hey, it's working.

Configuration
=============

Let's create a configuration file for Isso in, for example,
:code:`/opt/isso/etc/isso.cfg` with the following:

.. code:: ini

    [general]
    ; database location, check permissions, automatically created if not exists
    dbpath = /opt/isso/comments.db
    ; your website or blog (not the location of Isso!)
    host = https://www.brunoparmentier.be/

    [server]
    listen = http://localhost:8080/

You can launch Isso with:

.. code:: console

    $ isso -c /opt/isso/etc/isso.cfg run

The last thing we need to do is to configure nginx as a proxy to the Isso
server.

The official documentation suggests that you use :code:`comments.example.tld` as
server name. I prefer :code:`www.example.tld/comments` as it doesn't need
another certificate when using HTTPS.

Add a :code:`location` block in your nginx config and tell nginx to pass
requests beginning with :code:`/comments` to the local Isso server:

.. code:: nginx

    server {
        server_name     www.brunoparmentier.be;

        listen          443 ssl spdy;
        listen          [::]:443 ssl spdy;

        ssl_certificate /path/to/chained.pem;
        ssl_certificate_key /path/to/domain.key;

        root            /usr/share/nginx/html/www;

        location /comments {
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Script-Name /comments;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_pass http://localhost:8080;
        }
    }

We're done! We can now
`tweak <https://posativ.org/isso/docs/configuration/server/>`_ the configuration
file to activate moderation queue, email notifications, etc.
