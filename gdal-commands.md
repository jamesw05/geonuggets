***GDAL commands

#change the active version of GDAL on a mac system that has multiple versions of gdal installed. For example, as of 01.2017, if you want to write to filegeodatabases, you need to be running 1.11.x in order to have support for the ESRI filegeodatabase API. I had gdal 1.11.4 installed from a previous installation of QGIS, but, newer versions of qgis install and run GDAL 2.1.x.  

>so, how to re-activate the GDAL 1.11.x installation while being able to switch back to GDAL 2.1.x. ?

#cd over to the GDAL Framework 'Versions' directory
    cd /Library/Frameworks/GDAL.framework/Versions/

#duplicate the 'Current' gdal symlink

#set the symlink to version 1.11
    unlink Current && ln -s 1.11 /Library/Frameworks/GDAL.framework/Versions/Current

#set the symlink to version 2.1
    unlink Current && ln -s 2.1 /Library/Frameworks/GDAL.framework/Versions/Current