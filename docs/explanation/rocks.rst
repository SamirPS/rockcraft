.. _rocks_explanation:

ROCKs
=====

ROCKs are container images based on Ubuntu designed to meet 
cloud-native software's security, stability, and reliability requirements.

ROCKs were created to address two primary needs. Firstly, it tackles 
the current issues with container image security, as many popular 
container images often have known vulnerabilities. 
Secondly, it aims to provide a smaller container image based on 
Ubuntu to reduce the resource footprint on the host. 

These container images comply with the `Open Container
Initiative`_ (OCI) `image format specification <OCI_image_spec_>`_. 
They can be stored in container registries (e.g. DockerHub, ECR, ACR, Zot,..) 
and used with any OCI-Compliant tools (e.g. Docker, Podman, Kubernetes,...).
For example:

.. code:: bash

   docker run <rock> ...


Interoperability between ROCKs and other containers also extends to the way
that container images are built. This enables the use of ROCKs as bases for
existing build recipes, such as Dockerfiles, for further customisation and
development. 

The ROCKs ecosystem comprises

.. figure:: /_static/rockcraft_diagram.jpg
   :width: 75%
   :align: center
   :alt: ROCKs ecosystem


Chisel
------

Chisel is a software tool for extracting well-defined portions (also known as slices) of Debian packages 
into a filesystem. To learn more about Chisel see: :ref:`chisel_explanation` 

Pebble
------

In ROCKS, Pebble is the default entrypoint (an executable that runs when the container is initiated) in ROCKS, 
ensuring consistent container inspection and permit to have multiple entrypoints without the need to create other files.
To learn more about Pebble see: :ref:`pebble_explanation_page`

Rockcraft
---------

Rockcraft is a tool designed to build ROCKs using a declarative syntax (yaml). It leverages the logic of plugins, parts, 
and concepts that exist in Snapcraft and Charmcraft. 
Developers familiar with the creation and publication of snaps and charms will be able to utilise existing knowledge to create ROCKS.
To learn why you need to use Rockcraft see: :ref:`why_use_rockcraft`