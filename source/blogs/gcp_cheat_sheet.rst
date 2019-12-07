Google Cloud Platform Cheat Sheet
=================================
A quick reference to Google Cloud Platform.

Created on: 2019-12-05

.. warning:: under heavy construction and not well organized



install Google Cloud SDK or gcloud
----------------------------------
For Ubuntu we can use `apt` [1]_::

    echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
    sudo apt-get install apt-transport-https ca-certificates gnupg
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -
    sudo apt-get update && sudo apt-get install google-cloud-sdk

Or we can use Docker [2]_::

    docker pull gcr.io/google.com/cloudsdktool/cloud-sdk:latest

To run like normal tool instead of using docker run, make an alias like::

    alias gcloud_docker='docker run gcr.io/google.com/cloudsdktool/cloud-sdk:latest gcloud $@'

See here for more `Installation options <https://cloud.google.com/sdk/install#installation_options>`_.

start using the gcloud tool
---------------------------
to start using the gcloud tool::

    gcloud init

Now follow alone the instructions to finish the setup.


uninstall Google Cloud SDK or gcloud
------------------------------------
to uninstall Google Cloud SDK or gcloud::

    sudo apt remove --purge google-cloud-sdk
    sudo rm -rf $(gcloud info --format='value(config.paths.global_config_dir)';gcloud info --format='value(installation.sdk_root)')

    sudo rm /etc/apt/sources.list.d/google-cloud-sdk.list
    sudo rm /usr/share/keyrings/cloud.google.gpg
 




Google Compute Engine (GCE)
---------------------------

connect with ssh
````````````````
to connect with ssh first add ssh key with `gcloud` [3]_::

    gcloud compute --project "$PROJECT" ssh --zone "$ZONE" "$INSTANCE-NAME"

after that we can login with::

    ssh $PUBLIC-IP

If we forget this command, we don't need to worry as it is available in the drop down list located beside the `SSH` button on the `VM instances <https://console.cloud.google.com/compute/instances>`_ page.






Google Container Registry (GCR)
-------------------------------

push a docker image
```````````````````
to push a docker image, we need to tag an image [4]_::

    docker tag $SOURCE_IMAGE $HOSTNAME/$PROJECT-ID/$IMAGE:$TAG

$HOSTNAME could be:

- gcr.io
- us.gcr.io
- eu.gcr.io
- asia.gcr.io

choose the one closest to you. Now push the image::

    docker push $SOURCE_IMAGE $HOSTNAME/$PROJECT-ID/$IMAGE:$TAG


pull a docker image
```````````````````
to pull a docker image we need to configure our docker auth first [5]_::

    gcloud auth configure-docker


then the pull is done usually [6]_::

    docker pull $SOURCE_IMAGE $HOSTNAME/$PROJECT-ID/$IMAGE:$TAG

OR::

    docker pull $SOURCE_IMAGE $HOSTNAME/$PROJECT-ID/$IMAGE@$IMAGE_DIGEST




Source
------
.. [1] `Quickstart for Debian and Ubuntu <https://cloud.google.com/sdk/docs/quickstart-debian-ubuntu>`_
.. [2] `Installing the Cloud SDK Docker image <https://cloud.google.com/sdk/docs/downloads-docker>`_
.. [3] `Connecting to instances: Connecting to Linux instances <https://cloud.google.com/compute/docs/instances/connecting-to-instance#gcetools>`_
.. [4] `Pushing and pulling images: Pushing an image to a registry <https://cloud.google.com/container-registry/docs/pushing-and-pulling#pushing_an_image_to_a_registry>`_
.. [5] `Authentication methods: Authentication methods <https://cloud.google.com/container-registry/docs/advanced-authentication#gcloud_as_a_docker_credential_helper>`_
.. [6] `Pushing and pulling images: Pulling images from a registry <https://cloud.google.com/container-registry/docs/pushing-and-pulling#pulling_images_from_a_registry>`_



