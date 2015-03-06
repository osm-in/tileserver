# OpenStreetMap India
The OSM India community repository.

## Website
Currently running at http://14.139.123.10:8080/osm/slippymap.html

## Tile Server
Hosted by HBCSE-TIFR

### Fixing the boundaries
The Indian boundaries rendered on openstreetmap need to be modified to comply with Indian law. This can be fixed by adding the legal boundary shapes to the postgres database and making some changes to the mapnik xml to render it as per requirements

#### Downloading the Extended Boundaries
There is a relation created in osm of the boundary lines that match the legal requirement. It can be  downloaded using the following overpass api query:
```
[out:xml][timeout:25];
// gather results
(
  // query part for: “claimed_by=IN”
  node["claimed_by"="IN"]({{bbox}});
  way["claimed_by"="IN"]({{bbox}});
  relation["claimed_by"="IN"]({{bbox}});
);
// print results
out meta;
>;
out meta qt;
```
[Overpass Result](http://overpass-turbo.eu/s/82S). A snapshot is available in the /tileserver/data folder

Save the data to the disk as india-claim-boundaries.osm.xml

#### Load the boundaries into a new database
Use ```psql``` to setup a new postgis database for holding the new boundaries

```
create database india_boundaries;
\connect india_boundaries
create extension postgis;
\quit
```

Use ```osm2pgsql``` to load the data into the database
```
osm2pgsql -cGs -d india_boundaries ~/Desktop/india-claim-boundaries.osm.xml
```


## Contact
* [osm:talk-in list](https://lists.openstreetmap.org/listinfo/talk-in)