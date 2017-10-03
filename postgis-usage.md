#Postgis usage

#connect to a database
\c dbname

#connect to remote DB using Postgres.app 9.6 binary
/Applications/Postgres.app/Contents/Versions/9.6/bin/psql -U username -h remote.host.com -p 5432 dbname

#connect to a database (using specific pG version from postgres.app and a different user than the system user):
"/Applications/Postgres.app/Contents/Versions/9.6/bin/psql" -p5432 -d "database" -U username

#list all databases, list all databases with details (like size on disk)
\l or \l+

#show all tables in search path
\dt

#show a given table
\dt table_name 

#show all tables in given schema (make sure schemas dont have CAPS or special characters)
\dt schemaname.* 

#list detail of table, like columns, size, etc.
\d+ table_name; 

#show all unique values form a particular field
SELECT DISTINCT feature_cl FROM gnis;

#delete records matching a certain value in a field
DELETE FROM gnis WHERE feature_cl = 'Summit';

#rename column
ALTER TABLE tablename RENAME oldfieldname TO newfieldname;

#drop a schema and all tables within
DROP SCHEMA schemaname CASCADE;
#recreate the schema
CREATE SCHEMA schemaname;

#show all schemas
select schema_name from information_schema.schemata;

#show search path
show search_path;

#set search path
set search_path TO schemaname,public;

#drop column from table
ALTER TABLE tablename DROP COLUMN badcolumn;

#add a column
ALTER TABLE tablename ADD COLUMN goodcolumn text(10);

#rename a schema (if you messed up and made it with CAPS and/or scecial characters)
ALTER SCHEMA "S_USA" RENAME TO susa;

#rename table and sequence
ALTER TABLE oldtablename RENAME TO onewtablename;
ALTER SEQUENCE oldtablename_ogc_fid_seq RENAME TO oldtablename_ogc_fid_seq;

#export a psql table
pg_dump -U username databasename > outputfilename.pgsql

#export a subset of features from one table into a new pgsql table with LIKE function
SELECT * INTO dest_table FROM src_table WHERE ATTRIBUTENAME LIKE '%County%' OR ATTRIBUTENAME2 LIKE '%County%' OR ATTRIBUTENAME3 = 5;

#export a subset of osm features from one table into a new pgsql table
SELECT * INTO osm_trunk FROM planet_osm_line WHERE highway = 'trunk' OR highway = 'trunk_link';

#add centroids for polygons to table
ALTER TABLE "tablename" ADD x double precision;
ALTER TABLE "tablename" ADD y double precision;
UPDATE "tablename" SET x = ST_X(ST_Centroid(the_geom));
UPDATE "tablename" SET y = ST_Y(ST_Centroid(the_geom));