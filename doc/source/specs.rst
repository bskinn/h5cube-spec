.. Contents page for the various h5cube spec versions

h5cube File Specifications
==========================

This page collates all existing versions of the ``h5cube`` file specification
for convenient access.  The versioning scheme used here follows the
spirit of
`Semantic Versioning <http://semver.org>`__ but in a revised syntax:
:math:`\newcommand{mtt}[1]{\texttt{#1}}`

 * Specification version numbers will be of the form :math:`\mtt{vx.y rev#}`,
   where :math:`\mtt x` and :math:`\mtt{y}` indicate
   `major` and `minor` categories of changes, and :math:`\mtt{#}` is a `revision number`.

 * An increment in the `revision number` indicates minor editorial fix(es),
   such as correcting typos or introducing clarification(s) that do not
   affect the semantic content of the specification.

 * An increment in the `minor` version level indicates that new field(s) or other
   semantic content have been added to the specification, but existing
   fields/content are unchanged.

 * An increment in the `major` version level indicates that existing
   field(s)/content have been removed/changed. New field(s)/content may also
   have been added.

Based upon the above, it is expected that applications built against the
specific version :math:`\mtt{vX.Y}` should be compatible with the
versions :math:`\mtt{vx.y}` where :math:`x = X` and :math:`y \geq Y`.
Applications *may or may not* be compatible with versions
:math:`\mtt x > \mtt X`, depending on the particular changes introduced
with that `major` version increment.

The HDF5 dataset names defined by these specifications are formatted in
fixed-font, with surrounding square brackets (e.g., ``[GEOM]``).  This
distinguishes them from the fields in the
:doc:`CUBE file specification </cubeformat>`, which use curly braces
(e.g., ``{GEOM}``).  All of the dataset names are strings, and thus
to access the ``[GEOM]`` dataset in Python, use code like the following::

    >>> import h5py as h5
    >>> hf = h5.File('file.h5cube')
    >>> hf['GEOM'].value
    array([ ... ])

.. todo:: Description of the syntax/formatting of the dataset descriptions
          residing in the subpages here. In particular, a brief overview of
          the HDF5 datatypes and the 'lumped' approach taken in the
          spec layouts. (Fig. 6-4, Tbl. 6-1)


Specification Versions
----------------------


.. toctree::
    :maxdepth: 2

    v1.0 <specs/v1_0>



