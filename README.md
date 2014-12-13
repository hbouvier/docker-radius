# FreeRadius

Before the initial startup, you have to create the Certificates.

```bash
$ cd certs
$ vi ca.cnf server.cnf
$ make
$ cd ..
```


## Create a test user
sqlite3 db/radius.sqlite3
INSERT INTO radcheck VALUES('1', 'test', 'Cleartext-Password', ':=', 'secret');

## Start the container
```bash
$ docker run --name radius -d -e primary_shared_secret=radius_password -e "TIMEZONE=America/Montreal" -p 1812:1812/udp -v `pwd`/db:/opt/db -v `pwd`/certs:/etc/freeradius/certs hbouvier/radius
```

## To Debug Radius

```bash
$ docker run -ti -e DEBUG=true -e primary_shared_secret=radius_password -e "TIMEZONE=America/Montreal" -p 1812:1812/udp -v `pwd`/db:/opt/db -v `pwd`/certs:/etc/freeradius/certs radius
```
