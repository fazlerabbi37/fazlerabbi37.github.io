osmosis Cheat Sheet
===================
A quick reference to osmosis.

Created on: 2019-01-22

Populate a PostgreSQL database with pbf
---------------------------------------
To populate a PostgreSQL database with a pbf file, run this command::

    osmosis --read-pbf $absulute_file_path_of.osm.pbf --write-apidb host="$host" database="$database_name" user="$psql_username" password="$psql_password" validateSchemaVersion="no"

Create a .osm form a PostgreSQL database
----------------------------------------
We can create a ``.osm`` file from a PostgreSQL database::

    osmosis --read-apidb host="$host" database="$database_name" user="$psql_username" password="$psql_password" validateSchemaVersion="no" --write-xml file="$file_name.osm"

Merge two pbf
-------------
We can marge two pbf file using this command::

    osmosis --read-pbf file=$input1.osm.pbf --read-pbf file=$input2.osm.pbf --merge --write-pbf omitmetadata=true file=$output.osm.pbf

Load new osm data on PostgreSQL
-------------------------------
.. warning:: this is not working anymore.

Loading a new osm data on PostgreSQL database::

    osmosis --read-xml filename="$file.osm.gz" --write-apidb host="$host" database="$database_name" user="$psql_username" password="$psql_password" populateCurrentTables=yes validateSchemaVersion=no

Generate diff between two osm
-----------------------------
We can generate a diff in ``.osc`` or osm change format between two ``.osm`` file using this command::

    osmosis --read-xml file="input1.osm" --read-xml file="input2.osm" --derive-change --write-xml-change file="output_diff_1_to_2.osc"

Generate diff between osm and PostgreSQL db
-------------------------------------------
We can generate a diff in ``.osc`` between a ``.osm`` file and a PostgreSQL database::

    osmosis --read-xml file="input.osm" --read-apidb host="$host" database="$database_name" user="$psql_username" password="$psql_password" validateSchemaVersion=no --derive-change --write-xml-change file="output_diff_input_to_db.osc"

update a osm with diff
----------------------
We can update a ``.osm`` file with the diff generated in ``.osc``::

    osmosis --read-xml-change file="$osc_file.osc" --read-xml file="$old_osm_file.osm" --apply-change --write-xml file="$new_osm_file.osm"

Source
------
- `Osmosis OpenStreetMap Wiki <https://wiki.openstreetmap.org/wiki/Osmosis>`_
- `Osmosis/Examples OpenStreetMap Wiki <https://wiki.openstreetmap.org/wiki/Osmosis/Examples>`_
