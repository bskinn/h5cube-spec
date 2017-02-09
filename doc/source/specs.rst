.. Contents page for the various h5cube spec versions

h5cube File Specifications
==========================

This page collates all existing versions of the ``h5cube`` file specification
for convenient access.  The versioning scheme used here follows the
spirit of
`Semantic Versioning <http://semver.org>`__:
:math:`\newcommand{mtt}[1]{\texttt{#1}}`

 * Specification version numbers will be of the form v\ :math:`\mtt{x.y.z}`,
   where :math:`\mtt x`, :math:`\mtt{y}`, and :math:`\mtt{z}` indicate
   `major`, `minor`, and `patch` categories of changes. If :math:`\mtt z`
   is not present, it implicitly holds a value of zero.

 * An increment in the `patch` version level indicates minor editorial fix(es),
   such as correcting typos or introducing clarification(s) that do not
   affect the semantic content of the specification.

 * An increment in the `minor` version level indicates that new field(s) or other
   semantic content have been added to the specification, but existing
   fields/content are unchanged.

 * An increment in the `major` version level indicates that existing
   field(s)/content has been removed/changed. New field(s)/content may also
   have been added.

Based upon the above, it is expected that applications built against the
specific version v\ :math:`\mtt{X.Y.Z}` should be compatible with the
following versions v\ :math:`\mtt{x.y.z}`:

 * :math:`\mtt x = \mtt X`, :math:`\mtt y = \mtt Y`,
   :math:`\mtt z \geq \mtt Z`

 * :math:`\mtt x = \mtt X`, :math:`\mtt y > \mtt Y`, any :math:`\mtt z`

Applications *may or may not* be compatible with versions
:math:`\mtt x > \mtt X`, depending on the particular changes introduced
with that `major` version increment.


Specification Versions
----------------------


.. toctree::
    :maxdepth: 1

    v1.0 <specs/v1_0>



