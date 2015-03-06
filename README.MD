The openstreetmap India community repository.

## Website
Currently running at http://14.139.123.10:8080/osm/slippymap.html

## Tile Server
Hosted by HBCSE-TIFR

#### Fixing the boundaries
The Indian boundaries rendered on openstreetmap need to be modified to comply with Indian law. This can be fixed by adding the legal boundary shapes to the postgres database and making some changes to the mapnik xml to render it as per requirements

Use ```psql``` to setup a new postgis database for the custom boundaries

```
create database india_boundaries;
\connect india_boundaries
create extension postgis;
\quit
```

Use ```osm2pgsql``` to load the new boundaries into the database
```
osm2pgsql -cGs -d india_boundaries tileserver/india-claim-boundaries.osm.xml
```
The boundaries were generated using [this overpass query](http://overpass-turbo.eu/s/82S)

### Styling
Styling is based on a fork of [openstreetmap-carto](https://github.com/planemad/openstreetmap-carto). Read the install instructions to make sure all the shapefile dependencies are met.

Once setup, you can use [Tilemill]() to test the style and export the mapnik.xml file. Or you can use the one in ```/tileserver/openstreetmap-carto.xml```

## Contact
* [osm:talk-in list](https://lists.openstreetmap.org/listinfo/talk-in)