.. v1.0 rev1 h5cube specification

h5cube Specification v1.0 rev1
==============================


Datasets
--------

    |_VERSION| |br|
    |_COMMENT1| |br|
    |_COMMENT2| |br|
    |_NATOMS| |br|
    |_ORIGIN| |br|
    |_XAXIS| |br|
    |_YAXIS| |br|
    |_ZAXIS| |br|
    |_GEOM| |br|
    |_NUM_DSETS| |br|
    |_DSET_IDS| |br|
    |_SIGNS| |br|
    |_LOGDATA| |br|


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

    |String_t|

    First comment line of the |CUBE| file. Corresponds to
    |COMMENT1|.


.. _spec_1_0__rev1-COMMENT2:

**[COMMENT2]**

    |String_t|

    Second comment line of the |CUBE| file. Corresponds to
    |COMMENT2|.


.. _spec_1_0__rev1-NATOMS:

**[NATOMS]**

    |Integer_t|

    Corresponds directly to |NATOMS|, where the absolute value equals
    :math:`N_A`, the number of atoms in the system. The value here may
    be negative, with the same semantic implications as in the case of
    |NATOMS|. See |_NUM_DSETS| and |_DSET_IDS| for more details.

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
    |Float_t| type of the dataset. The remaining three
    elements are the vector :math:`\vec X` defining
    the voxel :math:`X`-axis.
    See |XAXIS| for more information about
    the semantics of these values.


.. _spec_1_0__rev1-YAXIS:

**[YAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    Corresponds directly to |YAXIS|. The first element is the number of
    voxels along the :math:`Y`-axis of the volumetric grid,
    :math:`N_Y`, and MUST be a positive integer value, despite the
    |Float_t| type of the dataset. The remaining three
    elements are the vector :math:`\vec Y` defining the voxel
    :math:`Y`-axis.
    See |YAXIS| for more information about the semantics of these values.


.. _spec_1_0__rev1-ZAXIS:

**[ZAXIS]**

    :math:`\dsetarr{Float}{4,\!}`

    Corresponds directly to |ZAXIS|. The first element is the number of
    voxels along the :math:`Z`-axis of the volumetric grid,
    :math:`N_Z`, and MUST be a positive integer value, despite the
    |Float_t| type of the dataset. The remaining three
    elements are the vector :math:`\vec Z` defining the voxel
    :math:`Z`-axis.
    See |ZAXIS| for more information about the semantics of these values.


.. _spec_1_0__rev1-GEOM:

**[GEOM]**

    :math:`\dsetarr{Float}{N_A,5}`

    Corresponds directly to |GEOM|. The first element of each of the
    :math:`N_A` lines (see |_NATOMS|) indicates the atomic number
    of atom *a*, and MUST be an |Integer_t| value. The second
    element of each line indicates the nuclear charge of atom *a*, and will
    generally be (i) equal to the atomic number and (ii) an integer
    quantity.  This value *will* deviate from the
    atomic number when an ECP [WP_PP]_ is used on atom *a*.

    The remaining three |Float_t| elements of each line
    provide the coordinates :math:`(x_a, y_a, z_a)` of atom *a* in the
    geometric frame of reference.


.. _spec_1_0__rev1-NUM_DSETS:

**[NUM_DSETS]**

    |Integer_t|

    Corresponds to the first value in |DSET_IDS|, indicating the number
    :math:`m` of dataset identifiers provided in the remainder of |DSET_IDS|.
    This value :math:`m` also specifies the required size of |_DSET_IDS|.


.. _spec_1_0__rev1-DSET_IDS:

**[DSET_IDS]**

    :math:`\dsetarr{Integer}{m,\!}`

    An array of :math:`m` values indicating the identifiers associated with
    the multiple data values provided at each voxel in
    |_SIGNS| and |_LOGDATA|.

    As noted in |DSET_IDS|, each of these values SHOULD be unique within
    the array, and SHOULD be non-negative. Otherwise, they can be any
    |Integer_t| value.


.. _spec_1_0__rev1-SIGNS:

**[SIGNS]**

    |_NATOMS| :math:`\dsetarrmap{>0}{Integer}{N_X,N_Y,N_Z}` |br|
    |_NATOMS| :math:`\dsetarrmap{<0}{Integer}{N_X,N_Y,N_Z,m}`

    This dataset combines with |_LOGDATA| to define the value of the
    volumetric data at each voxel :math:`(X,Y,Z)`.  This dataset contains
    the arithmetic signs of the data values, as per the standard
    mathematical *signum* :math:`(\sgn)` function [WP_Sign]_. Thus, if
    |_NATOMS| :math:`>0`:

        |_SIGNS|\ :math:`_{X,Y,Z} = \sgn{\left[\Phi\!\left(X,Y,Z\right)\right]}`

    and if |_NATOMS| :math:`<0`:

        |_SIGNS|\ :math:`_{X,Y,Z,i} = \sgn{\left[\Phi_i\!\left(X,Y,Z\right)\right]}`

    where :math:`\Phi_i` is the :math:`i^\text{th}` dataset included in the
    |CUBE| file.


.. _spec_1_0__rev1-LOGDATA:

**[LOGDATA]**

    |_NATOMS| :math:`\dsetarrmap{>0}{Float}{N_X,N_Y,N_Z}` |br|
    |_NATOMS| :math:`\dsetarrmap{<0}{Float}{N_X,N_Y,N_Z,m}`

    This dataset combines with |_SIGNS| to define the value of the
    volumetric data at each voxel :math:`(X,Y,Z)`. This dataset contains
    the common logarithms [WP_log10]_ of the data values. Thus, if
    |_NATOMS| :math:`>0`:

        |_LOGDATA|\ :math:`_{X,Y,Z} = \log_{10}{\left[\Phi\!\left(X,Y,Z\right)\right]}`

    and if |_NATOMS| :math:`<0`:

        |_LOGDATA|\ :math:`_{X,Y,Z,i} = \log_{10}{\left[\Phi_i\!\left(X,Y,Z\right)\right]}`

    where :math:`\Phi_i` is the :math:`i^\text{th}` dataset included in the
    |CUBE| file.



.. |_VERSION| replace:: :ref:`[VERSION] <spec_1_0__rev1-VERSION>`
.. |_COMMENT1| replace:: :ref:`[COMMENT1] <spec_1_0__rev1-COMMENT1>`
.. |_COMMENT2| replace:: :ref:`[COMMENT2] <spec_1_0__rev1-COMMENT2>`
.. |_NATOMS| replace:: :ref:`[NATOMS] <spec_1_0__rev1-NATOMS>`
.. |_ORIGIN| replace:: :ref:`[ORIGIN] <spec_1_0__rev1-ORIGIN>`
.. |_XAXIS| replace:: :ref:`[XAXIS] <spec_1_0__rev1-XAXIS>`
.. |_YAXIS| replace:: :ref:`[YAXIS] <spec_1_0__rev1-YAXIS>`
.. |_ZAXIS| replace:: :ref:`[ZAXIS] <spec_1_0__rev1-ZAXIS>`
.. |_GEOM| replace:: :ref:`[GEOM] <spec_1_0__rev1-GEOM>`
.. |_NUM_DSETS| replace:: :ref:`[NUM_DSETS] <spec_1_0__rev1-NUM_DSETS>`
.. |_DSET_IDS| replace:: :ref:`[DSET_IDS] <spec_1_0__rev1-DSET_IDS>`
.. |_SIGNS| replace:: :ref:`[SIGNS] <spec_1_0__rev1-SIGNS>`
.. |_LOGDATA| replace:: :ref:`[LOGDATA] <spec_1_0__rev1-LOGDATA>`


