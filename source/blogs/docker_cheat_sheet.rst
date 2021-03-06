Docker Cheat Sheet
==================
`< Blog <../blog.html>`_

A quick reference to Docker.

Created on: 2019-03-19

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

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

.. warning:: This is not recommanded as it creates an attack serface for privilege escalation. See more at: `Privilege escalation via Docker<https://fosterelli.co/privilege-escalation-via-docker>`. To fix this just remove the user from `docker` group with `sudo gpasswd -d $USER docker`.

after install::

    sudo groupadd docker
    sudo usermod -aG docker $USER

Now logout or reboot to see the change in effect.

source: https://docs.docker.com/v17.09/engine/installation/linux/linux-postinstall

test your installation::

    sudo docker run hello-world


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

    sudo docker ps

to list all container::

    docker ps -a

source: https://docs.docker.com/engine/reference/commandline/ps/

run docker behind proxy
-----------------------
Running docker daemon behind proxy can lead to problem like failing to download image. To solve that we need to add the proxy to docker daemon systemd service. First, we need to create a systemd directory for docker service::

    sudo mkdir /etc/systemd/system/docker.service.d

Now we will create a file with a text editor and put the environment variables in that file::

    sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf

The content would look like this::

    [Service]
    Environment="HTTP_PROXY=http://proxy.example.com:80/"
    Environment="HTTPS_PROXY=http://proxy.example.com:80/"

Now save the file and exit. To see the change in effect we need to flush changes in systemd and restart docker daemon::

    sudo systemctl daemon-reload
    sudo systemctl restart docker

More details: `Control Docker with systemd: HTTP/HTTPS proxy <https://docs.docker.com/config/daemon/systemd/#httphttps-proxy>`_

source: https://stackoverflow.com/a/28093517

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


docker-compose environment variables
------------------------------------
in compose either::

    .env file

or::

    environment:
      - key1=value1
      - key2=value2

source: https://docs.docker.com/compose/environment-variables/

docker run environment variables
--------------------------------
to use environment variables in docker run either::

     docker run --env-file ./env.list ubuntu bash


or::

    docker run -e "key1=value1" -e "key2=value2" ubuntu bash
   
source: https://docs.docker.com/engine/reference/run/#env-environment-variables https://stackoverflow.com/a/30494145/5350059

update docker images
--------------------
.. warning:: need to test

::

    docker-compose pull

    docker-compose up -d

https://stackoverflow.com/a/43515922/5350059

https://stackoverflow.com/a/49316987/5350059


docker nginx custom config
--------------------------
to use a custom configuration for nginx::

    FROM nginx

    COPY more_web_nginx.conf /etc/nginx/conf.d/

    RUN rm /etc/nginx/conf.d/default.conf

    COPY . /usr/share/nginx/html


source: https://stackoverflow.com/a/30152496/5350059

map docker container port to a specific interface on host
---------------------------------------------------------
to map docker container port to a specific interface on host::

    docker run -p <interface IP>:<outside port>:<inside port> $REST_OF_THE_COMMAND

source: https://stackoverflow.com/a/48874124/5350059
 
give name to a image
--------------------
to give name to a image::

	version: '3'
	services:
	  # for an image already build just put container_name bellow image
	  db:
		image: postgres:10.1-alpine
		container_name: pg_db
	  # for an image we are building put container_name bellow build
	  web:
		build:
		  context: .
		  dockerfile: Dockerfile
		container_name: web_dev

source: `How do I define the name of image built with docker-compose <https://stackoverflow.com/a/35662191/5350059>`_

COPY as non root
----------------
to COPY as non root::

    COPY --chown=<user>:<group> <hostPath> <containerPath>

source: `How do I Docker COPY as non root? <https://stackoverflow.com/a/44766666/5350059>`_

useful aliases
--------------
stop and remove all container
`````````````````````````````
::

    sudo docker stop $(sudo docker ps -a -q); sudo docker rm $(sudo docker ps -a -q)

remove unfinished build (<none>) image
``````````````````````````````````````
::

    sudo docker rmi -f $(sudo docker images | grep "<none>" | awk "{print $3}")

update all docker images
````````````````````````
::

    update_docker_images() {
    for iid in $(sudo docker images | awk 'FNR>1 {print $1 ":" $2}')
    do
        echo updating $iid...
        sudo docker pull $iid
    done
    }

OR one-liner::

    for iid in $(sudo docker images | awk 'FNR>1 {print $1 ":" $2}'); do     echo updating $iid..;     sudo docker pull $iid; done

remove all image containing string
``````````````````````````````````
::

    sudo docker rmi -f $(sudo docker images | grep $string | awk '{print $3}')


remove all volume
`````````````````
::

    sudo docker volume rm $(sudo docker volume ls -q)


persistent data volume for PostgreSQL
-------------------------------------
to add persistent data volume for PostgreSQL::

    postgres:
      container_name: postgres
      restart: always
      image: postgres:latest
      volumes:
        - ./database:/var/lib/postgresql/data
      ports:
        - "5432:5432

source: https://stackoverflow.com/a/41650891

shared persistent data volume
-----------------------------
to add persistent data volume::

	version: "2.4"

	services:
	  db:
	    image: db
	    volumes:
	      - data-volume:/var/lib/db
	  backup:
	    image: backup-service
	    volumes:
	      - data-volume:/var/lib/backup/data

	volumes:
	  data-volume:

source: https://docs.docker.com/compose/compose-file/compose-file-v2/#volume-configuration-reference    


docker-compose not getting the host environment variables
---------------------------------------------------------
While running docker-compose with `sudo` docker-compose doesn't get the host environment variables. The `-E` flag of the `sudo` command solves the problem::

    sudo -E docker-compose up

source: https://forums.docker.com/t/docker-compose-not-seeing-environment-variables-on-the-host/11837/8

supply docker build args inside docker-compose
----------------------------------------------
consider the following ``Dockerfile`` contains::

    FROM ubuntu:18.04

    ARG PACKAGE

    RUN apt update && apt install $PACKAGE

We need to supply a value for the PACKAGE variable in the build stage and to do that in the ``docker-compose.yml`` we will do::

    version: '3'

    services:
      docker-installer:
        image: docker-installer:v1
        build:
          context: .
          dockerfile: Dockerfile
          args:
            - PACKAGE=docker-ce


source: https://stackoverflow.com/a/41792420

docker ignore
-------------
ignore file from being coping to docker image while building with ``.dockerignore``. Just put the file and directories to be ignored in the ``.dockerignore`` file lie::

    # comment
    */temp*
    */*/temp*
    temp?

source: https://docs.docker.com/engine/reference/builder/#dockerignore-file

docker compose build specific service image
-------------------------------------------
to build specific service image::

    sudo docker-compose build $SERVICE_NAME

source: https://stackoverflow.com/a/35256698

docker compose start specific service
-------------------------------------
to start specific service::

    sudo docker-compose up $SERVICE_NAME

source: https://stackoverflow.com/a/30234588

comment in a Dockerfile
-----------------------
to comment in a Dockerfile, use `#`::

	# Everything on this line is a comment

More doc `Dockerfile reference: Format <https://docs.docker.com/engine/reference/builder/#format>`_

source: https://stackoverflow.com/a/36710513

build time arguments
--------------------
For the following `Dockerfile`::

	FROM ubuntu:18.04

	ARG PACKAGE

	RUN apt update && apt install $PACKAGE

Pass the build time arguments in `docker build` like this::

	sudo docker build --build-arg PACKAGE=docker-ce .

The general format is::

	sudo docker build --build-arg $KEY=$VALUE --build-arg $KEY1=$VALUE1 .

More doc `docker build: Set build-time variables (--build-arg) <https://docs.docker.com/engine/reference/commandline/build/#set-build-time-variables---build-arg>`_

source: https://stackoverflow.com/a/42297949

use a variable inside a Dockerfile CMD
--------------------------------------
to use a variable inside a Dockerfile CMD, run it with `sh`::

	CMD ["sh", "-c", "django-admin startproject $PROJECTNAME"]

	#OR

	CMD django-admin startproject $PROJECTNAME

source: https://stackoverflow.com/a/40454758

docker compose can't find node_modules directory
------------------------------------------------
this happens because ``node_modules`` directory is created during build time inside the container and root directory is mounted during run time and ``node_modules`` is not present in the host directory. to solve this we just need to do a one way mount of the ``node_modules`` directory::

	volumes:
	  - ./worker/:/worker/
	  - /worker/node_modules

source: https://stackoverflow.com/a/32785014

Quickstart
----------

Django
``````
- `Dockerfile`::

    FROM python:3
    ENV PYTHONUNBUFFERED 1
    RUN mkdir /code
    WORKDIR /code
    COPY requirements.txt /code/
    RUN pip install -r requirements.txt
    COPY . /code/

- `docker-compose.yml` with postgresql::

	version: '3'

	services:
	  db:
		image: postgres
	  web:
		build: .
		command: python manage.py runserver 0.0.0.0:8000
		volumes:
		  - .:/code
		ports:
		  - "8000:8000"
		depends_on:
		  - db

- `docker-compose.yml` without postgresql::

	version: '3'

	services:
	  web:
		build: .
		command: python manage.py runserver 0.0.0.0:8000
		volumes:
		  - .:/code
		ports:
		  - "8000:8000"

source: https://docs.docker.com/compose/django/

Rails
`````
- `Dockerfile`::

	FROM ruby:2.5
	RUN apt-get update -qq && apt-get install -y nodejs postgresql-client
	RUN mkdir /myapp
	WORKDIR /myapp
	COPY Gemfile /myapp/Gemfile
	COPY Gemfile.lock /myapp/Gemfile.lock
	RUN bundle install
	COPY . /myapp

	# Add a script to be executed every time the container starts.
	COPY entrypoint.sh /usr/bin/
	RUN chmod +x /usr/bin/entrypoint.sh
	ENTRYPOINT ["entrypoint.sh"]
	EXPOSE 3000

	# Start the main process.
	CMD ["rails", "server", "-b", "0.0.0.0"]

- The entrypoint script, `entrypoint.sh` is used to fix a Rails-specific issue that prevents the server from restarting when a certain `server.pid` file pre-exists. This script will be executed every time the container gets started. `entrypoint.sh`::

	#!/bin/bash
	set -e

	# Remove a potentially pre-existing server.pid for Rails.
	rm -f /myapp/tmp/pids/server.pid

	# Then exec the container's main process (what's set as CMD in the Dockerfile).
	exec "$@"

- `docker-compose.yml` with postgresql::

	version: '3'
	services:
	  db:
		image: postgres
		volumes:
		  - ./tmp/db:/var/lib/postgresql/data
	  web:
		build: .
		command: bash -c "rm -f tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
		volumes:
		  - .:/myapp
		ports:
		  - "3000:3000"
		depends_on:
		  - db

source: https://docs.docker.com/compose/rails/

NodeJS
``````
- `Dockerfile`::

	FROM node:7.7.2-alpine
	WORKDIR /usr/app
	COPY package.json .
	RUN npm install
	COPY . .

- `docker-compose.yml` with postgresql::

	version: '2'
	services:
	  web:
		build: .
		command: npm run dev
		volumes:
		  - .:/usr/app/
		  - /usr/app/node_modules
		ports:
		  - "3000:3000"
		depends_on:
		  - postgres
		environment:
		  DATABASE_URL: postgres://todoapp@postgres/todos
	  postgres:
		image: postgres:9.6.2-alpine
		environment:
		  POSTGRES_USER: todoapp
		  POSTGRES_DB: todos

- `docker-compose.yml` without postgresql::

	version: '2'
	services:
	  web:
		build: .
		command: npm run dev
		volumes:
		  - .:/usr/app/
		  - /usr/app/node_modules
		ports:
		  - "3000:3000"


source: https://rollout.io/blog/using-docker-compose-for-nodejs-development/


load a pgsql dump file to db
----------------------------
to load a pgsql dump file to db::

    sudo docker exec postgres psql -U postgres my_db_name < dump.sql

source: https://stackoverflow.com/a/50663127

Source
------
.. [1] `How to get bash or ssh into a running container in background mode? <https://askubuntu.com/a/507009/502875>`_
