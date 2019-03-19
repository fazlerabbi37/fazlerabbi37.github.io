docker
======
shell access on a docker container
----------------------------------
two ways to do it [1]_. ``attach`` and ``exec``.

using ``attach``
````````````````
::
    sudo docker attach 665b4a1e17b6 #by ID

    #OR

    sudo docker attach loving_heisenberg #by Name
    
using ``exec``
``````````````
::
    sudo docker exec -i -t 665b4a1e17b6 /bin/bash #by ID

    #OR

    sudo docker exec -i -t loving_heisenberg /bin/bash #by Name


source
------
.. [1] `How to get bash or ssh into a running container in background mode? <https://askubuntu.com/a/507009/502875>`_
