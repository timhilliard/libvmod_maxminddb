libvmod_maxminddb
=================

Varnish 4 vmod for loading maxminddb (geoip2)

**I have no clue what I'm doing, will most likely be insecure.**

Requirement:
=================
Packages: build-essential libtool libvarnishapi-dev python-docutils 

Build:
=================
You need libmaxminddb in order to build this.

```
 ./autogen.sh
 ./configure  VMOD_DIR=/usr/lib/varnish/vmods/
 make
 make install
```

Usage:
=================
```
import maxminddb;

sub vcl_init{
  maxminddb.init_db("/path/to/GeoLite2-City.mmdb");
}

sub vcl_recv {
  set req.http.continentcode = maxminddb.query_continent(client.ip);
  set req.http.countrycode = maxminddb.query_country(client.ip);
  set req.http.state = maxminddb.query_state(client.ip);
  set req.http.city = maxminddb.query_city(client.ip);
  set req.http.postalcode = maxminddb.query_postalcode(client.ip);
}

```
