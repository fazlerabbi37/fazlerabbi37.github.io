osmosis Cheat Sheet
===================
A quick reference of osmosis.

Using osmosis to populate a database from .osm.pbf
--------------------------------------------------
::

    osmosis --read-pbf <absulute_path_of_.osm.pbf_file> --write-apidb host="localhost" database="<database_name>" user="<psql_username>" password="<psql_password>" validateSchemaVersion="no"

Using osmosis to create a .osm form a database
----------------------------------------------
::

    osmosis --read-apidb host="localhost" database="" user="<psql_username>" password="<psql_password" validateSchemaVersion="no" --write-xml file="planet.osm"

merge two .osm.pbf file into one
--------------------------------
::

    osmosis --read-pbf file=$input1.osm.pbf --read-pbf file=$input2.osm.pbf --merge --write-pbf omitmetadata=true file=$output.osm.pbf

load new osm data to local db
-----------------------------
::

    osmosis --read-xml filename=".osm.gz" --write-apidb host="localhost" database="openstreetmap" user="openstreetmap" password="secret" populateCurrentTables=yes validateSchemaVersion=no

generate a diff(osc) file between two osm file
----------------------------------------------
::

    osmosis --read-xml file="planet1.osm" --read-xml file="planet2.osm" --derive-change --write-xml-change file="planetdiff-1-2.osc"

generate a diff(osc) file between a osm file and a postgres database
--------------------------------------------------------------------
::

    osmosis --read-xml /home/map_server/test_server/data/bangladesh_$current_date.osm --read-apidb host="localhost" database="openstreetmap" user="map_server" password="pathaomap" validateSchemaVersion=no --derive-change --write-xml-change file="bangladesh_$current_date_diff.osc"

update a osm file with osc
--------------------------
::

    osmosis --read-xml-change file="$osc_file.osc" --read-xml file="$old_osm_file.osm" --apply-change --write-xml file="$new_osm_file.osm"
