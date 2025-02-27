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
