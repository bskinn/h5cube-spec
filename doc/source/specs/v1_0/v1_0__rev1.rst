.. v1.0 rev1 h5cube specification

h5cube Specification v1.0 rev1
==============================

.. todo:: General intro

Table of Contents
-----------------

    |_VERSION| |br|
    |_COMMENT1| |br|
    ...


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
    |NATOMS|. See :ref:`[NUM_DSETS] <spec_1_0__rev1-NUM_DSETS>` and
    :ref:`[DSET_IDS] <spec_1_0__rev1-DSET_IDS>` for more details.

    This value MUST be nonzero.


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
    :math:`N_X`, and MUST be a positive integer value, despite the
    :math:`\dsettype{Float}` type of the dataset. The remaining three
    elements are the vector :math:`\vec X` defining
    the voxel :math:`X`-axis, and SHOULD all be non-negative.
    See |XAXIS| for more information about
    the semantics of these values.


.. _spec_1_0__rev1-YAXIS:

**[YAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    Corresponds directly to |YAXIS|. The first element is the number of
    voxels along the :math:`Y`-axis of the volumetric grid,
    :math:`N_Y`, and MUST be a positive integer value, despite the
    :math:`\dsettype{Float}` type of the dataset. The remaining three
    elements are the vector :math:`\vec Y` defining the voxel
    :math:`Y`-axis, and SHOULD all be non-negative.
    See |YAXIS| for more information about the semantics of these values.


.. _spec_1_0__rev1-ZAXIS:

**[ZAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    Corresponds directly to |ZAXIS|. The first element is the number of
    voxels along the :math:`Z`-axis of the volumetric grid,
    :math:`N_Z`, and MUST be a positive integer value, despite the
    :math:`\dsettype{Float}` type of the dataset. The remaining three
    elements are the vector :math:`\vec Z` defining the voxel
    :math:`Z`-axis, and SHOULD all be non-negative.
    See |ZAXIS| for more information about the semantics of these values.


.. _spec_1_0__rev1-GEOM:

**[GEOM]**

    :math:`\dsetarr{Float}{N_A,5}`

    Corresponds directly to |GEOM|. The first element of each of the
    :math:`N_A` lines (see
    :ref:`[NATOMS] <spec_1_0__rev1-NATOMS>`) indicates the atomic number
    of atom *a*, and MUST be an :math:`\dsettype{Integer}` value. The second
    element of each line indicates the nuclear charge of atom *a*, and will
    generally be (i) equal to the atomic number and (ii) an
    :math:`\dsettype{Integer}` value.  This value *will* deviate from the
    atomic number when an ECP is used on atom *a*.

    The remaining three :math:`\dsettype{Float}` elements of each line
    provide the coordinates :math:`(x_a, y_a, z_a)` of atom *a* in the
    geometric frame of reference.


.. _spec_1_0__rev1-NUM_DSETS:

**[NUM_DSETS]**

    :math:`\dsettype{Integer}`

    Corresponds to the first value in |DSET_IDS|, indicating the number
    :math:`m` of dataset identifiers provided in the remainder of |DSET_IDS|.
    This value :math:`m` also specifies the required size of
    :ref:`[DSET_IDS] <spec_1_0__rev1-DSET_IDS>`.


.. _spec_1_0__rev1-DSET_IDS:

**[DSET_IDS]**

    :math:`\dsetarr{Integer}{m,\!}`

    An array of :math:`m` values indicating the identifiers associated with
    the multiple data values provided at each voxel in
    :ref:`[SIGNS] <spec_1_0__rev1-SIGNS>`
    and :ref:`[LOGDATA] <spec_1_0__rev1-LOGDATA>`.

    As noted in |DSET_IDS|, each of these values SHOULD be unique within
    the array, and SHOULD be non-negative. Otherwise, they can be any
    :math:`\dsettype{Integer}` value.


.. _spec_1_0__rev1-SIGNS:

**[SIGNS]**

    |_NATOMS| :math:`>0 \rightarrow \dsetarr{Integer}{N_X,N_Y,N_Z}`

    .. todo:: Complete this!


.. _spec_1_0__rev1-LOGDATA:

**[LOGDATA]**

    :math:`\dsetarr{Float}{FIX THIS!!}`

    .. todo:: Complete this!



.. |_VERSION| replace:: :ref:`[VERSION] <spec_1_0__rev1-VERSION>`
.. |_COMMENT1| replace:: :ref:`[COMMENT1] <spec_1_0__rev1-COMMENT1>`
