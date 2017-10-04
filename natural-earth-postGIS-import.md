

**Import Natural Earth Data into a PostGIS database**

#a pretty version of this is at:

http://downfallnotes.com/index.php/2017/01/19/loading-natural-earth-data-into-postgis-for-illustratormapublisher/

#Install Postgres app:

http://postgresapp.com/

#making a new postgis database:

CREATE DATABASE naturalearth;
\c naturalearth
CREATE EXTENSION postgis;
CREATE SCHEMA z10m_cultural;
CREATE SCHEMA z10m_physical;
CREATE SCHEMA z50m_cultural;
CREATE SCHEMA z50m_physical;
CREATE SCHEMA z110m_cultural;
CREATE SCHEMA z110m_physical;
CREATE EXTENSION hstore;

#add the different schemas to the DB search path, so that the MAPublisher spatial filter can be used

ALTER DATABASE naturalearth SET search_path = z10m_physical, z10m_cultural, z50m_cultural, z50m_physical, z110m_cultural, z110m_physical, public;

#import all of the NEData .shp's into the database in the correct schema

for f in *.shp; do PGCLIENTENCODING=LATIN1 ogr2ogr -update -append -progress -skipfailures -nlt GEOMETRY -lco GEOMETRY_NAME=geom -lco SCHEMA=z50m_cultural -f "PostgreSQL" PG:"dbname=naturalearth user=username" $f; done;