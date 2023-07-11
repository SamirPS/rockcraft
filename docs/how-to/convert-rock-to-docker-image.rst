.. _how_to_convert_rock_to_docker_image:

How to convert your ROCK to a docker image
------------------------------------------

You have built your ROCK by following one of our tutorial or by yourself
and want to convert your ``.rock`` file to a docker image ?

To convert your image, we will use `Skopeo <https://github.com/containers/skopeo>`_ (which is already installed if you have rockcraft).

To convert ``<rock_name>.rock`` to a docker image on your machine simply do: 

.. code-block:: bash

    sudo /snap/rockcraft/current/bin/skopeo --insecure-policy copy oci-archive:<rock_name>.rock docker-daemon:<rock_name>:latest


Let's break down the command to understand what it's does: 

``/snap/rockcraft/current/bin/skopeo`` This refers to the path of the skopeo binary inside rockcraft

``--insecure-policy``: This flag tells skopeo to not run policies checks during the operation.

``copy``: This skopeo subcommand permit copy container images from one location to another.

``oci-archive:<rock_name>.rock``: This is the source location of the container image. the ``oci-archive`` specifies that the image is an OCI (Open Container Initiative) 
archive format.

``docker-daemon:<rock_name>:latest``: This is the destination location for the container image. 
It specifies that the image should be copied to a local Docker daemon and with the name <rock_name> and the tag latest.

So now do:

.. code-block:: bash

  $ docker images <rock_name>:latest

    REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
    <rock_name>  latest    <IMAGE_ID>   <CREATE_TIME>  <SIZE>

