.. _chisel_explanation:

Chisel
======

Chisel_ is a software tool for extracting well-defined portions (aka slices) of
Debian packages into a filesystem.

Using the analogy of a tool to carve and cut stone, Chisel is used in
Rockcraft to sculpt minimal collections of files that only include what is
needed for the ROCK to function properly.

See :ref:`how_to_use_chisel` for information about using the tool.


Slice definitions
-----------------

A slice is a yaml file permiting chisel to slice the package accordingly to your inputs. Here an exemple:

.. code-block:: yaml

   # (req) Name of the package.
   # The slice definition file should be named accordingly (eg. "openssl.yaml")

   package: B

   # (req) List of slices
   slices:

      # (req) Name of the slice
      slice2:

         # (opt) Optional list of slices that this slice depends on
         essential:
            - A_slice1

         # (req) The list of files, from the package, that this slice will install
         contents:
               /path/to/content:
               /path/to/another/multiple*/content/**:
               /path/to/moved/content: {copy: /bin/original}
               /path/to/link: {symlink: /bin/mybin}
               /path/to/new/dir: {make: true}
               /path/to/file/with/text: {text: "Some text"}
               /path/to/mutable/file/with/default/text: {text: FIXME, mutable: true}
               /path/to/temporary/content: {until: mutate}

         # (opt) Mutation scripts, to allow for the reproduction of maintainer scripts,
         # based on Starlark (https://github.com/canonical/starlark)
         mutate: |
               foo = content.read("/path/to/temporary/content")
               content.write("/path/to/mutable/file/with/default/text", foo)

To find more examples or if you want to contribute your own, check `here <https://github.com/canonical/chisel-releases>`_.

Package slices
--------------

Since Debian packages are simply archives that can be inspected, navigated
and deconstructed, it is possible to define slices of packages that contain
minimal, complementary, loosely-coupled sets of files based on package
metadata and content. Such **package slices** are subsets of Debian packages,
with their own content and set of dependencies to other internal and external
slices.

The use of package slices provides Rockcraft with the ability to build minimal
container images from the wider set of Ubuntu packages.

.. figure:: /_static/package-slices.svg
   :width: 75%
   :align: center
   :alt: Debian package slices with dependencies

This image illustrates the simple case where, at a package level, package *B*
depends on package *A*. However, there might be files in *A* that *B* doesn't
actually need, but which are provided for convenience or completeness.
By identifying the files in *A* that are actually needed by *B*, we can divide
*A* into slices that serve this purpose. In this example, the files in the
package slice, *A_slice3*, are not needed for *B* to function. To make package
*B* usable in the same way, it can also be divided into slices.

With these slice definitions in place, Chisel is able to extract a
highly-customised and specialised slice of the Ubuntu distribution, which one
could see as a block of stone from which we can carve and extract only the
small and relevant parts that we need to run our applications, thus keeping
ROCKs small and less exposed to vulnerabilities.

