{:menu SW}

# Setting up local server

* toc
{:toc}

I am using nginx and gunicorn to host local web pages. The nginx service may be launched by
`brew services start nginx`, and it seems to get hosted by root for a reason that I haven't been able to figure out. Configuration files for nginx are located at `/opt/homebrew/etc/nginx/` and involve three pieces. The main file is `nginx.conf`

~~~~ shell
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
error_log  logs/error.log  info;

#pid        logs/nginx.pid;

events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;
	add_header Content-Security-Policy "frame-ancestors localhost djphys";

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

	include       /opt/homebrew/etc/nginx/sites-enabled/*;

    sendfile        on;
    #tcp_nopush     on;
    keepalive_timeout 15;
    include servers/*;
}
~~~~

The `sites-enabled` directory has soft links to configuration files in `sites-available`, which are `base.conf`, `mysrc.conf`, and `djphys.conf`. The base configuration services files with autoindex on from `~/www/`.

To enable https for local web serving with multiple Django apps, it was
necessary to generate a self-signed certificate with multiple SANs, to get it
properly installed and respected by the system, and then configure both nginx
and gunicorn to enable secure connections.

As far as I can tell, to generate the self-signed certificate with multiple
local server names, you need a configuration file. The following files seemed to
do the trick:

**/opt/homebrew/etc/ssl/cmds**

To save a bit on typing as I went around and around, I put the openssl commands in a short script file.

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

**/opt/homebrew/etc/ssl/openssl-ca.cnf**

~~~~ shell
cat openssl-ca.cnf
HOME             = .
RANDFILE         = $ENV::HOME/.rnd

#######################################################################
[ ca ]
default_ca       = CA_default        # The default ca section

[ CA_default ]

default_days     = 3000
default_crl_days = 300
default_md       = sha256
preserve         = no                # keep passed DN ordering

x509_extensions  = ca_extensions     # the extensions to add to the cert

email_in_dn      = no                # don't concat the email in the DN
copy_extensions  = copy              # required to copy SANs from CSR to cert

base_dir         = .
certificate      = $base_dir/cacert.pem  # the CA certificate
private_key      = cakey.pem   # the CA private key
new_certs_dir    = $base_dir
database         = $base_dir/index.txt   # Database index file
serial           = $base_dir/serial.txt  # current serial number

unique_subject   = no # allows creation of several certificates w/ same subject

#########################################################################
[ req ]
default_bits       = 4096
default_keyfile    = cakey.pem
distinguished_name = ca_distinguished_name
x509_extensions    = ca_extensions
string_mask        = utf8only

################################################################################
[ ca_distinguished_name ]
countryName           = Country Name (2 letter code)
countryName_default   = US

stateOrProvinceName   = State or Province Name (full name)
stateOrProvinceName_default = California

localityName          = Locality Name (e.g., city)
localityName_default  = Claremont

organizationName      = Organization Name (e.g., company)
organizationName_default = Peter N. Saeta

organizationalUnitName = Organizational Unit (e.g., division)
organizationalUnitName_default = myself

commonName            = Common Name (e.g., server FQDN or YOUR name)
commonName_default    = PNS

emailAddress          = Email Address
emailAddress_default  = saeta@hmc.edu

################################################################################
[ ca_extensions ]

subjectKeyIdentifier   = hash
authorityKeyIdentifier = keyid:always, issuer
basicConstraints       = critical, CA:true
keyUsage               = keyCertSign, cRLSign

####################################################################
[ signing_policy ]
countryName            = optional
stateOrProvinceName    = optional
localityName           = optional
organizationName       = optional
organizationalUnitName = optional
commonName             = supplied
emailAddress           = optional

####################################################################
[ signing_req ]
subjectKeyIdentifier   = hash
authorityKeyIdentifier = keyid,issuer
basicConstraints       = CA:FALSE
keyUsage               = digitalSignature, keyEncipherment
~~~~

~~~~ shell
HOME            = .
RANDFILE        = $ENV::HOME/.rnd

####################################################################
[ req ]
default_bits       = 2048
default_keyfile    = serverkey.pem
distinguished_name = server_distinguished_name
req_extensions     = server_req_extensions
string_mask        = utf8only

####################################################################
[ server_distinguished_name ]
countryName                 = Country Name (2 letter code)
countryName_default         = US

stateOrProvinceName         = State or Province Name (full name)
stateOrProvinceName_default = California

localityName                = Locality Name (eg, city)
localityName_default        = Claremont

organizationName            = Organization Name (eg, company)
organizationName_default    = PNS Chaos

commonName                  = Common Name (e.g. server FQDN or YOUR name)
commonName_default          = Self

emailAddress                = Email Address
emailAddress_default        = saeta@hmc.edu

####################################################################
[ server_req_extensions ]

subjectKeyIdentifier = hash
basicConstraints     = CA:FALSE
keyUsage             = digitalSignature, keyEncipherment
subjectAltName       = @alternate_names
nsComment            = "OpenSSL Generated Certificate"

####################################################################
[ alternate_names ]

DNS.1  = localhost
DNS.2  = mysrc
DNS.3  = djphys
~~~~