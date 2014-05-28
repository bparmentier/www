<!-- 
.. title: ConnectBot: Authenticate with a SSH key
.. slug: connectbot-authenticate-with-a-ssh-key
.. date: 02/18/2013 00:00:00 AM UTC+02:00
.. tags: android, ssh
.. link: 
.. description: 
.. type: text
-->

First, make sure openssh-server is installed on the machine you want to connect

# Generate the key

Launch ConnectBot, hit the `Menu key` and select `Manage Pubkeys`.
Hit `Menu → Generate`.

Give your key a nickname.

Then choose encryption type. Default RSA 1024 bits should be good enough.

You now have the choice to set a password or not. You can leave it blank, but
you have to know that a SSH key without password is like a bank card without PIN
code; if anyone gains access to your phone or at least to your private key, he
would be able to connect to every server where your public key is installed.

Check `Load key on start` if you want.

Press `Generate` and move your finger around the box to gather randomness.

# Add your key on the server

Your key is now created.
Long press on its name and choose `Copy public key`.
Log in to the server (with your password) and type the following command:

```bash
$ echo "your public key" >> .ssh/authorized_keys
```

To paste your key using ConnectBot, tap on `Menu → Paste`. Don't forget the
quotes.
