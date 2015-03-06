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
Styling is based on a fork of [openstreetmap-carto](https://github.com/planemad/openstreetmap-carto). Read the [install instructions](https://github.com/planemad/openstreetmap-carto/blob/master/INSTALL.md) for how to load the osm data, download the required shapefiles and fonts.

Once setup, you can load the project into [Tilemill](https://www.mapbox.com/tilemill/) to test the style and export the mapnik.xml stylesheet for use with the mapnik renderer.

- **Note:** A pre compiled mapnik stylesheet can be found at  ```/tileserver/openstreetmap-carto.xml```. Using this stylesheet will require correcting the paths that reference the downloaded .shp shapefiles.

- To setup multiple style layers, follow the instructions here http://stackoverflow.com/questions/24492029/switch-styles-on-an-openstreetmap-server-using-mapnik-postgis-etc

## Contact
* [osm:talk-in list](https://lists.openstreetmap.org/listinfo/talk-in)