# Unbound DNS Resolver
The only action required before starting the container is to change the logging level in the configuration file. Follow the steps below to go from 0 to hero!

## 1. Copy conf file and mount container to host
```
mkdir ~/unbound-config
```
IMPORTANT! Create the `unbound-config` folder in your home folder to avoid OS permission restrictions when copying over the files (from container to host).

Start a temporary container:
```
docker run -d --name unbound-temp mvance/unbound:1.12.0
```

Copy the config file:
```
docker cp unbound-temp:/opt/unbound/etc/unbound/unbound.conf ~/unbound-config/
```

Remove the temp container:
```
docker rm -f unbound-temp
```

Start and mount the container:
```
docker run -d \
  --name unbound \
  -p 53:53/udp \
  -p 53:53/tcp \
  -v ~/unbound-config/unbound.conf:/opt/unbound/etc/unbound/unbound.conf:ro \
  mvance/unbound:1.12.0
```

## 2. Edit and restart container
Replace the content of the `~/unbound-config/unbound.conf` file with the `unbound.conf` in this repo.

Restart the container:
```
docker restart unbound
```

## 3. Test DNS lookup
Running this should give `status: SERVFAIL` because the lookup fails to verify DNSSEC signature.
```
dig @127.0.0.1 dnssec-failed.org
```

Running this should have the flag `ad` meaning Authenticated Data:
```
dig @127.0.0.1 dnssec.works
```

## Clean container(s)
This removes all containers.
```
docker rm -f unbound unbound-temp
```
You may now start form step 1.