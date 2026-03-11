# BNSS-UpDog-network
The repository for the EP2520 Building Network Systems Security project for group UpDog (Group 10)

# Nginx Reverse Proxy
cd into `nginx-proxy` folder and follow the README.

# Unbound DNS
cd into `unbound-dns` folder and follow the README.

# Nextcloud & Nextcloud-critical
## 1. Start the containers
```
cd nextcloud
docker compose up -d

cd ../nextcloud-critical
docker compose up -d

cd ..
```

Create an admin account and do the following steps as admin.

## 2. (Both) Enable LDAP
Search for the LDAP app in nextcloud and tell Axel to start the LDAP server.
```
LDAP server address: `192.168.1.161`
Discover port.
Username DN: `cn=admin,dc=ldap,dc=local`
Password: `axel`
Base DN: `dc=ldap,dc=local`
Login attributes: `uid`
```

## 3. (Nextcloud-critical) Enable TOTP 2FA
1. Enable the app `Two-Factor TOTP Provider` under `Your apps`
2. Click your profile then `Administration -> Security -> Force Two-Factor Authentication`


## 4. (Optional) Change language:
In the container terminal (`docker exec -it nextcloud bash`):
```
docker exec -u www-data nextcloud php /var/www/html/occ config:system:set force_language --value=en
```

# SmallStep
## Issue new certificate
`step ca certificate <subject> <cert-file> <key-file>`

Password: `opnsense`
