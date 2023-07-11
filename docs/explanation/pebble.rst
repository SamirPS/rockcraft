.. _pebble_explanation_page:

Pebble
======

When creating container images using Dockerfile, several issues can be met. 
For instance, if the entrypoint relies on the application mode (such as nginx and nginx-debug), 
creating a bash script that parses the first argument provided during container deployment will be necessary. 
This script will configure and launch NGINX accordingly. 

Additionally, each image runs with specific application arguments, 
making it challenging to perform an inspection inside the image consistently. 
Pebble solves this problem by providing a comprehensive set of commands for starting, 
stopping, and viewing service status. It also includes features like auto-restart 
for continuous operation and dependency management for proper sequencing of services. 
Pebble streamlines service management as a single binary that operates as both a background 
service and a client. 

In ROCKS, Pebble services are defined with properties such as name, command, startup behaviour, 
dependencies,... Moreover, Pebble is the default entrypoint 
(an executable that runs when the container is initiated) in ROCKS, ensuring consistent container 
inspection and permit to have multiple entrypoints without the need to create other files. 


Create a service
----------------

See :ref:`how_to_convert_pebble` for information about converting a Docker entrypoint to
a pebble service. Also check the `top-level field
<https://canonical-rockcraft.readthedocs-hosted.com/en/latest/reference/
rockcraft.yaml/#format-specification>`_ to understand the parameters and field needed to
create a service.


