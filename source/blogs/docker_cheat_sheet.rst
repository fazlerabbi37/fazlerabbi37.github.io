Docker Cheat Sheet
==================
A quick reference to Docker.

Created on: 2019-03-19

.. warning:: under heavy construction and not well organized



install docker on ubuntu
------------------------
to docker install on ubuntu::

    sudo apt-get remove docker docker-engine docker.io -y
    sudo apt-get update
    
    sudo apt-get install apt-transport-https ca-certificates curl software-properties-common -y
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update

    sudo apt-get install docker-ce -y

source: https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/

after install::

    sudo groupadd docker
    sudo usermod -aG docker $USER

Now logout or reboot to see the change in effect.

source: https://docs.docker.com/v17.09/engine/installation/linux/linux-postinstall

test your installation::

    docker run hello-world


install docker-compose on ubuntu
--------------------------------
to install docker-compose on ubuntu::

    sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose

source: https://docs.docker.com/compose/install/


docker-compose bash compilation
-------------------------------
to have bash compilation for docker-compose::

    sudo curl -L https://raw.githubusercontent.com/docker/compose/1.24.1/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose

now restart bash

source: https://docs.docker.com/compose/completion/


shell access on a docker image
------------------------------


https://stackoverflow.com/questions/30172605/how-do-i-get-into-a-docker-containers-shell#comment75385171_30172605
https://stackoverflow.com/questions/22049212/copying-files-from-docker-container-to-host#22050116

list container
--------------
to list running container::

    docker ps

to list all container::

    docker ps -a


run a docker image as a container in background
-----------------------------------------------
to run a docker image as a container do the following::

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

completely remove docker
------------------------
to completely remove docker and all related file, first identify what installed package we have::

    dpkg -l | grep -i docker

Then run the following::

    sudo apt-get purge -y docker-engine docker docker.io docker-ce docker-ce-cli
    sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce docker-ce-cli

Make sure the above commands has all the following packages from the `dpkg -l` command. If not add them at the end. The above commands will not remove images, containers, volumes, or user created configuration files on your host. If you wish to delete all images, containers, and volumes run the following commands::

    sudo rm -rf /var/lib/docker
    sudo rm /etc/apparmor.d/docker
    sudo groupdel docker
    sudo rm -rf /var/run/docker.sock
    sudo rm -rf /etc/docker
    sudo rm -rf ~/.docker

Finally remove docker-compose::

    sudo rm /usr/local/bin/docker-compose

source: https://askubuntu.com/a/1021506/502875

install tzdata without user interaction
---------------------------------------
to install tzdata without user interaction, put this in Dockerfile::

    ARG DEBIAN_FRONTEND=noninteractive

source: https://askubuntu.com/a/1013396/502875

remove all images and containers
--------------------------------
to remove all images and containers::

    docker rm $(docker ps -a -q)
    docker rmi -f $(docker images -q)

source: https://techoverflow.net/2013/10/22/docker-remove-all-images-and-containers/

execute `source` command inside Dockerfile
------------------------------------------
to execute `source` command inside Dockerfile::

    RUN /bin/bash -c "source /path/to/file"

source: https://stackoverflow.com/a/25086628/5350059

rebuild docker image
--------------------
to rebuild docker image with docker-compose::

    docker-compose build -f /path/to/docker-compose.yml

source: https://stackoverflow.com/a/57027380/5350059

remove unused data
------------------
to removed unused data::

    docker system prune

source: https://docs.docker.com/engine/reference/commandline/system_prune/

see log
-------
to see log::

    docker logs container_id

stop container
--------------
to stop a container gracefully with `SIGTERM`::

    docker stop container_id

to kill a container with `SIGKILL` when it is stuck::

    docker kill container_id

run command inside a container
------------------------------
to run command inside a container::

    docker exac -it container_id command


Source
------
.. [1] `How to get bash or ssh into a running container in background mode? <https://askubuntu.com/a/507009/502875>`_
