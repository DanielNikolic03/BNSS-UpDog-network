# BNSS-UpDog-network
The repository for the EP2520 Building Network Systems Security project for group UpDog (Group 10)

# How to run
## Nextcloud
```
cd nextcloud
docker compose up -d
```

### Configuration changes made:
In the container terminal (`docker exec -it nextcloud bash`):

**Remove device login option**
```
su -s /bin/bash www-data -c "php occ config:system:set --type boolean --value false auth.webauthn.enabled"
```

From the hosts terminal (not the container terminal):
**Change language**
```
docker exec -u www-data nextcloud php /var/www/html/occ config:system:set force_language --value=en
```

## Unbound DNS
### How to run?
cd into `unbound-dns` folder and follow the README.