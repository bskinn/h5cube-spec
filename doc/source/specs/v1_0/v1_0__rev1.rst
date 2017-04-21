.. v1.0 rev1 h5cube specification

h5cube Specification v1.0 rev1
==============================

.. todo:: General intro

Field Contents
--------------

... TOC ...


Field Descriptions
------------------

.. _spec_1_0_rev1-VERSION:

**[VERSION]**

    :math:`\dsetarr{Integer}{2,\!}`

    |h5cube| specification version met by the file, where the first
    and second elements are the major and minor version numbers,
    respectively:

        :math:`\mtt{vx.y} \rightarrow (\mtt x, \mtt y)`

    This dataset MAY be absent for specification v1.0 **only**\ .


.. _spec_1_0_rev1-COMMENT1:

**[COMMENT1]**

    :math:`\dsettype{String}`

    First comment line of the |CUBE| file. Corresponds to
    |COMMENT1|.


.. _spec_1_0_rev1-COMMENT2:

**[COMMENT2]**

    :math:`\dsettype{String}`

    Second comment linen of the |CUBE| file. Corresponds to
    |COMMENT2|.

.. _spec_1_0_rev1-NATOMS:

**[NATOMS]**

    :math:`\dsettype{Integer}`

    Corresponds directly to |NATOMS|, where the absolute value indicates the
    number of atoms in the system. The value here may be negative, with
    the same semantic implications as with |NATOMS|. See **!!ADDLINKS!!**
    for more details.

    .. todo:: Add links to [NUM_DSETS] and [DSET_IDS] once written.



