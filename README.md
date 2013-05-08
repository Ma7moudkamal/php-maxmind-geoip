### Requirements

None (only the 'GeoIP.dat' file is needed).  To download a free GeoIP Standard Country
database, go to
http://dev.maxmind.com/geoip/geolite

### Install

Add the following lines in your composer.json file:

```json
{
    "require": {
        "maxromanovsky/php-maxmind-geoip": "1.*"
    }
}
```

_**Note** : You may want to adapt the version._

### Usage

* Gets country name by ip :

```php
<?php 

$gi = geoip_open("/usr/local/share/GeoIP/GeoIP.dat",GEOIP_STANDARD);

echo geoip_country_code_by_addr($gi, "24.24.24.24") . "\t" .
     geoip_country_name_by_addr($gi, "24.24.24.24") . "\n";
echo geoip_country_code_by_addr($gi, "80.24.24.24") . "\t" .
     geoip_country_name_by_addr($gi, "80.24.24.24") . "\n";

geoip_close($gi);
```

_**Note** : You have to include `geoip.inc` manually in case you are not using composer package._

* Gets region details by ip:

```php
<?php

$gi = geoip_open("/usr/local/share/GeoIP/GeoIP.dat",GEOIP_STANDARD);

$record = GeoIP_record_by_addr($gi, "24.24.24.24");

geoip_close($geoIp);

echo sprintf("Country code: %s\n", $record->country_code);
echo sprintf("Country: %s\n", $record->country_name);
echo sprintf("Region: %s\n", $record->region);
echo sprintf("City: %s\n", $record->city);
echo sprintf("Latitude: %s\n", $record->latitude);
echo sprintf("Longitude: %s\n", $record->longitude);
```

_**Note** : You have to include `geoip.inc` and `geoipcity.inc` manually in case you are not using composer package._

### Memory Caching:

To enable memory caching, pass GEOIP_SHARED_MEMORY or
GEOIP_MEMORY_CACHE to the second argument of geoip_open

For GEOIP_SHARED_MEMORY, requires php >= 4.0.4,
and --enable-shmop passed at configure time, see
http://us2.php.net/manual/en/ref.shmop.php
In addition, you should call geoip_load_shared_mem
before calling geoip_open.  See sample_city.php for an
example of shared memory caching.

### Working with PHP5.
geoip_country_code_by_addr should work
with PHP.  For help with the other
routines, please contact support@maxmind.com

Thanks to Jim Winstead.
