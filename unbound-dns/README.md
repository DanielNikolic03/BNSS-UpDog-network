# Unbound DNS Resolver
The only action required before starting the container is to change the logging level in the configuration file. Follow the steps below to go from 0 to hero!

## 1. Create the folder structure
```
mkdir ~/unbound-config
touch ~/unbound-config/unbound.conf
touch ~/unbound-config/a-records.conf
```

## 2. Add the conf files
Replace the `unbound.conf` and `a-records.conf` in `~/unbound-config/` with the files in this directory.

## 3. Start the container
```
docker compose up -d
```

## 4. Force DNS lookups through Unbound
Log into the router config page (router running OpenWRT).

Under `Network -> Interfaces -> wan -> Edit` set the IP of the host computer under "Use custom DNS servers" and disable "Use DNS servers advertised by peers".

And under `Network -> Forwards` remove all addresses under  "DNS Forwards" and add the IP of the host computer.

Save and Apply changes.

## 5. Test DNS lookup
Running this should give `status: SERVFAIL` because the lookup fails to verify DNSSEC signature.
```
dig @127.0.0.1 dnssec-failed.org
```

Running this should have the flag `ad` meaning Authenticated Data:
```
dig @127.0.0.1 dnssec.works
```