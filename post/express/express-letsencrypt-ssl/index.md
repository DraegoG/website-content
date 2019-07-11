---
title: Setup Let's Encrypt for Express
description: "How to set up HTTPS using the popular free solution Let's Encrypt"
date: 2018-09-18T07:00:00+02:00
tags: express
tags_weight: 5
path: express-letsencrypt-ssl
---

If you run a Node.js application on your own VPS, you need to manage getting an SSL certificate.

Today the standard for doing this is to use [Let's Encrypt](https://letsencrypt.org) and [Certbot](https://certbot.eff.org/), a tool from [EFF](https://www.eff.org/), aka Electronic Frontier Foundation, the leading nonprofit organization focused on privacy,  free speech, and in general civil liberties in the digital world.

These are the steps we'll follow:

<!-- TOC -->

- [Install Certbot](#install-certbot)
- [Generate the SSL certificate using Certbot](#generate-the-ssl-certificate-using-certbot)
- [Allow Express to serve static files](#allow-express-to-serve-static-files)
- [Confirm the domain](#confirm-the-domain)
- [Obtain the certificate](#obtain-the-certificate)
- [Setup the renewal](#setup-the-renewal)

<!-- /TOC -->

## Install Certbot

Those instructions assume you are using Ubuntu, Debian or any other Linux distribution that uses `apt-get`:

```bash
sudo add-apt repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install certbot
```

You can also install Certbot on a Mac to test:

```bash
brew install certbot
```

but you will need to link that to a real domain name, in order for it to be useful.

## Generate the SSL certificate using Certbot

Now that Certbot is installed, you can invoke it to generate the certificate. You must run this as root:

```bash
certbot certonly --manual
```

or call sudo

```bash
sudo certbot certonly --manual
```

The installer will ask you the domain of your website.

This is the process in detail.

It asks for the email


```txt
➜ sudo certbot certonly --manual
Password: XXXXXXXXXXXXXXXXXX
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator manual, Installer None
Enter email address (used for urgent renewal and security notices) (Enter 'c' to
cancel): flavio@flaviocopes.com
```

It asks to accept the ToS:

```txt
Please read the Terms of Service at
https://letsencrypt.org/documents/LE-SA-v1.2-November-15-2017.pdf. You must
agree in order to register with the ACME server at
https://acme-v02.api.letsencrypt.org/directory

(A)gree/(C)ancel: A
```

It asks to share the email address

```txt
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: Y
```

And finally we can enter the domain where we want to use the SSL certificate:

```txt
Please enter in your domain name(s) (comma and/or space separated)  (Enter 'c'
to cancel): copesflavio.com
```

It asks if it's ok to log your IP:

```txt
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for copesflavio.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
NOTE: The IP of this machine will be publicly logged as having requested this
certificate. If you're running certbot in manual mode on a machine that is not
your server, please ensure you're okay with that.

Are you OK with your IP being logged?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y
```

And finally we get to the verification phase!

```txt
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Create a file containing just this data:

TS_oZ2-ji23jrio3j2irj3iroj_U51u1o0x7rrDY2E.1DzOo_voCOsrpddP_2kpoek2opeko2pke-UAPb21sW1c

And make it available on your web server at this URL:

http://copesflavio.com/.well-known/acme-challenge/TS_oZ2-ji23jrio3j2irj3iroj_U51u1o0x7rrDY2E
```

Now let's leave Certbot alone for a couple minutes.

We need to verify we own the domain, by creating a file named `TS_oZ2-ji23jrio3j2irj3iroj_U51u1o0x7rrDY2E` in the  `.well-known/acme-challenge/` folder. Pay attention! The weird string I just pasted change every single time.

You'll need to create the folder and the file, since they do not exist by default.

In this file you need to put the content that Certbot printed:

```txt
TS_oZ2-ji23jrio3j2irj3iroj_U51u1o0x7rrDY2E.1DzOo_voCOsrpddP_2kpoek2opeko2pke-UAPb21sW1c
```

As for the filename, this string is unique each time you run Certbot.

## Allow Express to serve static files

In order to serve that file from Express, you need to enable serving static files. You can create a `static` folder, and add there the `.well-known` subfolder, then configure Express like this:

```js
const express = require('express')
const app = express()

//...

app.use(express.static(__dirname + '/static', { dotfiles: 'allow' } ))

//...
```

The `dotfiles` option is mandatory otherwise `.well-known`, which is a dotfile as it starts with a dot, won't be made visible. This is a security measure, because dotfiles can contain sensitive information and they are better off preserved by default.

## Confirm the domain

Now run the application and make sure the file is reachable from the public internet, and go back to Certbot, which is still running, and press ENTER to go on with the script.

## Obtain the certificate

That's it! If all went well, Certbot created the certificate, and the private key, and made them available in a folder on your computer (and it will tell you which folder, of course).

Now copy/paste the paths into your application, to start using them to serve your requests:

```js
const fs = require('fs')
const https = require('https')
const app = express()

app.get('/', (req, res) => {
  res.send('Hello HTTPS!')
})

https.createServer({
  key: fs.readFileSync('/etc/letsencrypt/path/to/key.pem'),
  cert: fs.readFileSync('/etc/letsencrypt/path/to/cert.pem'),
  ca: fs.readFileSync('/etc/letsencrypt/path/to/chain.pem')
}, app).listen(443, () => {
  console.log('Listening...')
})
```

Note that I made this server listen on port 443, so you need to run it with root permissions.

Also, the server is exclusively running in HTTPS, because I used `https.createServer()`. You can also run an HTTP server alongside this, by running:

```js
http.createServer(app).listen(80, () => {
  console.log('Listening...')
})

https.createServer({
  key: fs.readFileSync('/etc/letsencrypt/path/to/key.pem'),
  cert: fs.readFileSync('/etc/letsencrypt/path/to/cert.pem'),
  ca: fs.readFileSync('/etc/letsencrypt/path/to/chain.pem')
}, app).listen(443, () => {
  console.log('Listening...')
})
```

## Setup the renewal

The SSL certificate is not going to be valid for 90 days. You need to set up an automated system for renewing it.

How? Using a cron job.

A cron job is a way to run tasks every interval of time. It can be eery week, every minute, every month.

In our case we'll run the renewal script twice per day, as recommended in the Certbot documentation.

First find out the absolute path of `certbot` on you system. I use `type certbot` on macOS to get it, and in my case it's `/usr/local/bin/certbot`.

Here's the script we need to run:

`certbot renew`

This is the cron job entry:

```txt
0 */12 * * * root /usr/local/bin/certbot renew >/dev/null 2>&1
```

It means run it every 12 hours, every day: at 00:00 and at 12:00.

> Tip: I generated this line using <https://crontab-generator.org/>

Add this script to your crontab, by using the command:

```bash
env EDITOR=pico crontab -e
```

This opens the `pico` editor (you can choose the one you prefer). You enter the line, save, and the cron job is installed.

Once this is done, you can see the list of cron jobs active using

```bash
crontab -l
```