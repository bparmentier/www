.. title: Nginx: Redirect non-www and/or HTTP traffic to HTTPS and www domain
.. slug: nginx-redirect-non-www-andor-http-traffic-to-https-and-www-domain
.. date: 2015-11-19 14:10:19+01:00
.. tags: nginx
.. category:
.. link:
.. description:
.. type: text

As you may have seen, I have now forced the use of HTTPS on my website. The
certificate is signed by Let's Encrypt and should therefore be recognized by all
major browsers. I used the
`letsencrypt-nosudo <https://github.com/diafygi/letsencrypt-nosudo>`_ tool made
by Daniel Roesler to manually generate my certificates because I didn't want the
letsencrypt client to mess with my Nginx config files (I will probably try when
I'm sure it is stable enough and working well on my server OS).

I wanted to redirect all traffic coming from the non-www domain to the www
domain, and all HTTP traffic to HTTPS.

Basically, like this:

+---------------------------------------+----------------------------------------+
| From                                  | To                                     |
+=======================================+========================================+
| :code:`http://brunoparmentier.be`     |                                        |
+---------------------------------------+                                        +
| :code:`http://www.brunoparmentier.be` | :code:`https://www.brunoparmentier.be` |
+---------------------------------------+                                        +
| :code:`https://brunoparmentier.be`    |                                        |
+---------------------------------------+----------------------------------------+

Here is the configuration I use on my server:

.. code:: nginx

    # Redirect all non-www traffic to www
    server {
        server_name     brunoparmentier.be;
        listen          80;
        listen          443 ssl spdy;
        listen          [::]:80;
        listen          [::]:443 ssl spdy;

        ssl_certificate /path/to/certs/chained.pem;
        ssl_certificate_key /path/to/certs/domain.key;

        return          301 https://www.brunoparmentier.be$request_uri;
    }

    # Redirect all non-encrypted traffic to encrypted
    server {
        server_name     www.brunoparmentier.be;
        listen          80;
        listen          [::]:80;

        return          301 https://www.brunoparmentier.be$request_uri;
    }

    # Main server block
    server {
        server_name     www.brunoparmentier.be;
        listen          443 ssl spdy;
        listen          [::]:443 ssl spdy;

        ssl_certificate /path/to/certs/chained.pem;
        ssl_certificate_key /path/to/certs/domain.key;

        root            /usr/share/nginx/html/www;

        # ...
    }

Note that I'm using a SAN (Subject Alternative Name) certificate which is valid
for both :code:`brunoparmentier.be` and :code:`www.brunoparmentier.be`.

:code:`chained.pem` contains this certificate, along with the "Let’s Encrypt
Intermediate X1" certificate.

:code:`domain.key` contains the certificate private key.
