.. v1.0 rev1 h5cube specification

h5cube Specification v1.0 rev1
==============================

.. todo:: General intro

Table of Contents
-----------------

... TOC ...


Dataset Descriptions
--------------------

.. _spec_1_0__rev1-VERSION:

**[VERSION]**

    :math:`\dsetarr{Integer}{2,\!}`

    |h5cube| specification version met by the file, where the first
    and second elements are the major and minor version numbers,
    respectively:

        :math:`\mtt{vx.y} \rightarrow (\mtt x, \mtt y)`

    This dataset MAY be absent for specification v1.0 **only**\ .


.. _spec_1_0__rev1-COMMENT1:

**[COMMENT1]**

    :math:`\dsettype{String}`

    First comment line of the |CUBE| file. Corresponds to
    |COMMENT1|.


.. _spec_1_0__rev1-COMMENT2:

**[COMMENT2]**

    :math:`\dsettype{String}`

    Second comment linen of the |CUBE| file. Corresponds to
    |COMMENT2|.


.. _spec_1_0__rev1-NATOMS:

**[NATOMS]**

    :math:`\dsettype{Integer}`

    Corresponds directly to |NATOMS|, where the absolute value equals
    :math:`N_A`, the number of atoms in the system. The value here may
    be negative, with the same semantic implications as in the case of
    |NATOMS|. See **!!ADDLINKS!!** for more details.

    .. todo:: Add links to [NUM_DSETS] and [DSET_IDS] once written.


.. _spec_1_0__rev1-ORIGIN:

**[ORIGIN]**

    :math:`\dsetarr{Float}{3,\!}`

    Vector pointing from the origin of the system geometry frame to the
    reference point :math:`\left(x_0, y_0, z_0\right)` of the vectors
    spanning the |CUBE| voxel grid. Corresponds directly to |ORIGIN|.


.. _spec_1_0__rev1-XAXIS:

**[XAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    Corresponds directly to |XAXIS|. The first element is the number of
    voxels along the :math:`X`-axis of the volumetric grid,
    :math:`N_X`, and MUST be an integer, despite the
    :math:`\dsettype{Float}` type of the dataset. The remaining three
    elements are the vector :math:`\vec X` defining
    the voxel :math:`X`-axis. See |XAXIS| for more information about
    the semantics of these values.


.. _spec_1_0__rev1-YAXIS:

**[YAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-ZAXIS:

**[ZAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-GEOM:

**[GEOM]**

    :math:`\dsetarr{Float}{FIX THIS!!}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-NUM_DSETS:

**[NUM_DSETS]**

    :math:`\dsettype{Integer}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-DSET_IDS:

**[DSET_IDS]**

    :math:`\dsetarr{Integer}{FIX THIS!!}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-SIGNS:

**[SIGNS]**

    :math:`\dsetarr{Integer}{FIX THIS!!}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-LOGDATA:

**[LOGDATA]**

    :math:`\dsetarr{Float}{FIX THIS!!}`

    .. todo:: Complete this!

