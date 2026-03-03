# Nginx Reverse Proxy
## 1. Create the folder structure
```
mkdir ~/nginx-proxy
mkdir ~/nginx-proxy/conf
touch ~/nginx-proxy/conf/nextcloud.conf
mkdir ~/nginx-proxy/certs
mkdir ~/nginx-proxy/certs/fileshare
mkdir ~/nginx-proxy/certs/secret
```

## 2. Add the conf file and certificate
Replace the `nextcloud.conf` in `~/nginx-proxy/conf` with the file in this directory.

Move the certificate files from `/fileshare` to `~/nginx-proxy/certs/fileshare`
and `/secret` to `~/nginx-proxy/certs/secret`.

## 3. Start the conainer
```
docker compose up -d
```