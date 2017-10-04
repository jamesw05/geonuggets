***PostGIS Troubleshooting*

#sometimes after editing tables with postgis from terminal, they mess up in qgis:

Unable to access the "public"."tablename" relation.
            The error message from the database was:
            no result buffer.

restart qgis to fix this.

#sometimes running postgis queries will put a ton of system memory into 'inactive' or cached state. clear cached memory:

    sudo purge

#show processes, to find one that is idle or hanging

    SELECT * FROM pg_stat_activity;

#remove the process by pid

    SELECT pg_terminate_backend( <procpid> );

#for remote connections, test if the port is open

    sudo lsof -PiTCP -sTCP:LISTEN

#for remote connections, test if the port is open, only 5432

    sudo lsof -PiTCP -sTCP:LISTEN | grep 5432

#allow from all hosts

open pg_hba.conf and add following entry at the very end.

host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5