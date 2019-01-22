osmfilter Cheat Sheet
=====================
A quick reference of osmfilter.

drop tags
---------
Generate a osm without specified tags from a large osm file::

    osmfilter $file.osm --drop-tags="admin_level= boundary= amenity= man_made= name= office= shop= addr:housenumber= addr:housename= addr:street= addr:postcode= addr:place= level= lanes= turn= " -o=main_$file.osm

keep tags
---------
Generate a osm with only specified tags from a large osm file [1]_::

    osmfilter planet.o5m -v --keep-tags="amenity=" -o=amenities.osm

Source
------
.. [1] `How to filter out all amenities with osmfilter together with any other tag information they have? <https://stackoverflow.com/a/27870896/5350059>`_
