# ownCloud docker setup with nginx selfsigned certificates
This is the ownCloud docker setup running with nginx reverse proxy with self signed certificates. 
Purpose of this setup is to run on local network and access via HTTPS.
Since HTTPS is supported, owncloud server can be connected to FolderSync mobile app.

I searched all over internet, but didn'y found this type of setup. So keeping it here.

## Assumptions
- Local IP Address: 192.168.0.12
- Port to access server: 8443
- Its better to assign a static IP address to you server machine in the router so its not changed dynamically.

## Communication port mapping
- nginx docker will listen to port 8443 which is mapped to its internal port 443 (8443:443)
- ngixx will communcate to owncloud docker on port 8080 which is mapped to owncloud's internal port 8080 (8080:8080)

## Installation
- Download or Clone the repo. owncloud is going to be main directory of installation.
  ```
  cd owncloud
  ```
- Generated self signed certificates.
  ```
  sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout nginx/certs/server.key -out nginx/certs/server.crt -subj "/CN=192.168.0.12"
  ```
- Install and run docker images.
  ```
  docker compose up -d
  ```
## Post installation configuration
- Open config.php
  ```
  docker compose down                       # Stop container to allow some configuration change
  sudo nano owncloud_data/config/config.php # Open congiguration file
  ```
- Add following lines
  ```
  'overwriteprotocol' => 'https',                   
  'overwritehost' => '192.168.0.12:8443',          
  'overwritewebroot' => '/',                        
  'trusted_proxies' => ['192.168.0.12'],            
  'enable_previews' => false,                       
  #'files_external_allow_create_new_local' => true,  # Use if you want to add external USB drive
  ```
## Start container again
  ```
  docker compose up -d
  ```
## Accessing owncloud server
Open web browser in same computer or any other computer in same network. Open below URL
  ```
  https://192.168.0.12:8443
  ```


