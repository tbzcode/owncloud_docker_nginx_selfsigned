# ownCloud docker setup with nginx selfsigned certificates
This is the ownCloud docker setup running with nginx reverse proxy with self signed certificates. 
Purpose of this setup is to run on local network and access via HTTPS.
Since HTTPS is supported, owncloud server can be connected to FolderSync mobile app.

I searched all over internet, but didn'y found this type of setup. So keeping it here.

## Assumptions
Local IP Address: 192.168.0.12
Port to access server: 8443

## Communication port mapping
nginx docker will listen to port 8443 which is mapped to its internal port 443 (8443:443)
ngixx will communcate to owncloud docker on port 8080 which is mapped to owncloud's internal port 8080 (8080:8080)

## Installation
- Download or Clone the repo



