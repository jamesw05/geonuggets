***OGR commands

#explode a .kml with multiple geometry types into separate files
    ogr2ogr -explodecollections -f "KML" S2_grid_explode.kml S2_grid.kml

#import a .gdb into a new, blank .gdb
    ogr2ogr -progress -f "FileGDB" mergedGDB.gdb templateGDB.gdb

#import a whole folder of .gdb's to append to the one just created (minus the one used to create):
    for f in *.gdb; do ogr2ogr -update -append -progress mergedGDB.gdb $f -f "FileGDB"; done;

#export a postgis table (only selected features) to a .gdb
    ogr2ogr -progress -f "FileGDB" -sql "SELECT * FROM osm_secondary" secondary_rds.gdb  PG:"host=localhost user=username dbname=osm_database" 

#export a whole postgis table to a .shp (osm in this case)
    ogr2ogr -f "ESRI Shapefile" osm_motorway.shp PG:"host=localhost user=username dbname=osm_database" "osm_motorway"