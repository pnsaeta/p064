{:menu SW}

# Setting up local server

* toc
{:toc}

To enable https for local web serving with multiple Django apps, it was
necessary to generate a self-signed certificate with multiple SANs, to get it
properly installed and respected by the system, and then configure both nginx
and gunicorn to enable secure connections.

As far as I can tell, to generate the self-signed certificate with multiple
local server names, you need a configuration file. The following files seemed to
do the trick:

**/opt/homebrew/etc/ssl/cmds**

~~~~ shell
#! /bin/bash

# Create a self-signed certificate that will be the root of trust
openssl req -x509 -config openssl-ca.cnf -days 3000 -newkey rsa:4096 -nodes -sha256 -out cacert.pem -outform PEM

# Generate a certificate request
openssl req -config openssl-server.cnf -newkey rsa:4096 -nodes -keyout serverkey.pem -out servercert.csr -outform PEM

# Generate a signed certificate
openssl ca -config openssl-ca.cnf -policy signing_policy -extensions signing_req -out servercert.pem -infiles servercert.csr

mv cacert.pem servercert.pem /opt/homebrew/etc/ssl/certs/
mv cakey.pem serverkey.pem /opt/homebrew/etc/ssl/private/
~~~~

