docker
======
A quick reference to Docker.

shell access on a docker image
------------------------------

https://stackoverflow.com/questions/30172605/how-do-i-get-into-a-docker-containers-shell#comment75385171_30172605
https://stackoverflow.com/questions/22049212/copying-files-from-docker-container-to-host#22050116

run a docker image as a container in background
-----------------------------------------------
to run a docker image as a container do the following [4]_::

    docker run -d repository
    docker run -d repository:tag
    docker run -d image_id

source: https://stackoverflow.com/a/50208526/5350059

shell access on a docker container
----------------------------------
two ways to do it [1]_. ``attach`` and ``exec``.

using ``attach``
````````````````
::

    sudo docker attach image_id

    #OR

    sudo docker attach repository #by Name

using ``exec``
``````````````
::

    sudo docker exec -i -t image_id /bin/bash

    #OR

    sudo docker exec -i -t repository /bin/bash

duplicate an image
------------------
to duplicate an image::

    docker tag image new_image

source: https://stackoverflow.com/a/45779866/5350059

sleep in between two commands
-----------------------------
we can put pause in between two commands for 60 seconds by putting the following in between those commands::

    RUN sleep 60

source: https://forums.docker.com/t/how-to-delay-execution-of-next-line-in-dockefile/50022/2


source
------
.. [1] `How to get bash or ssh into a running container in background mode? <https://askubuntu.com/a/507009/502875>`_
