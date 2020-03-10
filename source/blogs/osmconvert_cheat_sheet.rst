osmconvert Cheat Sheet
======================
`< Blog <../blog.html>`_

A quick reference to osmconvert.

Created on: 2019-01-22

Tag: `cheat_sheet <blogs/tag_cheat_sheet.html>`_

osm to pbf
----------
Converting osm to pbf::

    osmconvert test.osm --out-pbf > test.osm.pbf

pbf to osm
----------
Converting pbf to osm::

    osmconvert test.osm.pbf --out-osm > test.osm

osm to csv
----------
Converting osm to csv::

    osmconvert test.osm --all-to-nodes --csv="@id @lon @lat amenity shop name" --csv-headline -o=test.csv

extract osm with poly
---------------------
Extracting pbf of a specific geo-bound from a large pbf with poly file::

    osmconvert $pbf_file -B=$poly_file -o=$output_pbf_file

extract osm with bbox
---------------------
Extracting pbf of a specific geo-bound from a large pbf with bbox::

    osmconvert bangladesh.osm.pbf -b=90.32908,23.66621,90.51599,23.90121 -o=dhaka.osm.pbf

osm file statistics
-------------------
Getting osm file statistics::

    osmconvert $file --out-statistics

Source
------
- `Osmconvert - OpenStreetMap Wiki <https://wiki.openstreetmap.org/wiki/Osmconvert>`_
