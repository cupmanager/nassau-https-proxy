Simple HTTPS for development
============================

This is a simple SSL-stripping proxy for local development. You don’t need to configure your apache or nginx or vagrant or whatever to use SSL. Just complete a simple setup and all of your local projects will be available over HTTPS without browser warnings.

Requirements & Setup
====================

After getting the code fetch required dependencies:

```
npm install
```

You need to have `openssl` available on your system, since it’s used to generate certs. 

Run proxy
=========

For convinience, proxy listens on the default HTTPS port (443) so it needs to be ran as root:

```
$ sudo node index.js
Listening on 443
Generating: /home/bob/.nassau-proxy/ssl.proxy.nassau.pass.key
Generating: /home/bob/.nassau-proxy/ssl.proxy.nassau.key
Generating: /home/bob/.nassau-proxy/ssl.proxy.nassau.csr
Add this cert as a trusted root to get rid of SSL warnings: /home/bob/.nassau-proxy/ssl.proxy.nassau.crt
```

Do as instructed, open the cert in your KeyChain:
```
open ~/.nassau-proxy/ssl.proxy.nassau.crt
```
And set it to "always trust". [Google it if you have any problems](http://superuser.com/questions/404178/importing-a-self-signed-ssl-certificate-on-macos)

Alternate port
==============

If you need to run it on a different port, use `PORT` env:

```
env PORT=8443 node index.js
```


Enjoy
=====

After trusting the generated root certificate (`ssl.proxy.nassau.crt`), your browser will accept any dummy cert generated for your domains by the proxy. Navigate to [https://localhost](https://localhost) to check the results.
