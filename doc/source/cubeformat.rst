.. Exposition of CUBE file format

Gaussian CUBE File Format
=========================

Disclaimer
----------

The |CUBE| file format as described here is **NOT** an official specification,
sanctioned by Gaussian, Inc. It is instead a best effort to define
the contents of a representative subset of |CUBE| files in circulation.
**FILES FORMATTED TO THIS SPECIFICATION
MAY NOT BE COMPATIBLE WITH ALL SOFTWARE SUPPORTING** |CUBE| **FILE INPUT.**

Overview
--------

The |CUBE| file format is described on the Gaussian webpage as part of the
documentation of the ``cubegen`` utility [Gau16]_. As noted there, **all data**
in |CUBE| files MUST be stored in atomic units (electrons and Bohrs, and units derived
from these).

The format specification on the webpage of the VMD visualization program [UIUC16]_
provides a cleaner layout of one possible arrangement of |CUBE| file contents. In particular,
the Gaussian specification is ambiguous about whitespace requirements, so parsing of |CUBE|
files SHOULD accommodate some variation in the format, including (i) variable
amounts/types of whitespace between the values on
a given line, and (ii) the presence of leading and/or trailing whitespace on a given line.

The |CUBE| file format as laid out below uses tagged fields (``{FIELD (type)}``) to indicate
the types of the various data elements and where they are located in the file.
Descriptions of the fields are provided below the
:ref:`field layout <cubeformat-FieldLayout>`.  Lowercase algebraic symbols
:math:`\left(x\right.`, :math:`y`, :math:`\left. z\right)` indicate coordinates in the frame
of the molecular geometry, whereas uppercase algebraic symbols
:math:`\left(X\right.`, :math:`Y`, :math:`\left. Z\right)` indicate coordinates in the
voxel grid defined by |XAXIS|, |YAXIS|, and |ZAXIS|.

All fields except for
|DSET_IDS|  and |NVAL| MUST be present in all files.

|DSET_IDS| MUST be present if
|NATOMS| is negative; it MUST NOT be present if |NATOMS| is positive.

|NVAL| MAY be omitted if its value would be equal to one; it MUST be absent or
have a value of one if |NATOMS| is negative.

.. _cubeformat-FieldLayout:

Field Layout
------------

::

    {COMMENT1 (str)}
    {COMMENT2 (str)}
    {NATOMS (int)} {ORIGIN (3x float)} {NVAL (int)}
    {XAXIS (int) (3x float)}
    {YAXIS (int) (3x float)}
    {ZAXIS (int) (3x float)}
    {GEOM (int) (float) (3x float)}
          .
          .
    {DSET_IDS (#x int)}
          .
          .
    {DATA (#x scinot)}
          .
          .

Table of Contents
-----------------

    |COMMENT1| and |COMMENT2| |br|
    |NATOMS| |br|
    |ORIGIN| |br|
    |NVAL|  |br|
    |XAXIS| |br|
    |YAXIS| |br|
    |ZAXIS| |br|
    |GEOM|  |br|
    |DSET_IDS| |br|
    |DATA|


Field Descriptions
------------------

.. _cubeformat-COMMENTS:

**{COMMENT1 (str)}** and **{COMMENT2 (str)}**

    Two lines of text at the head of the file. Per VMD [UIUC16]_, by convention |COMMENT1|
    is typically the title of the system and |COMMENT2| is a description of the
    property/content stored in the file, but they MAY be anything. For robustness, both of
    these fields SHOULD NOT be zero-length.  As well, while there is no defined maximum length
    for either of these fields, both SHOULD NOT exceed 80 characters in length.


.. _cubeformat-NATOMS:

**{NATOMS (int)}**

    The absolute value of this first field on the third line indicates
    the number of atoms :math:`N_A` present in the system.
    A negative value indicates the |CUBE| file MUST contain the
    |DSET_IDS| line(s); a positive value indicates the file
    MUST NOT contain this/these lines.

    The value of :math:`N_A` also specifies the number of rows of
    molecular geometry data that MUST be present in |GEOM|.

    The |CUBE| specification is silent as to whether a zero value is
    permitted for |NATOMS|; regardless, it is probable that
    many applications **do not** support |CUBE| files with no atoms.
    Accordingly, this specification hereby declares that |NATOMS| MUST be
    nonzero.


.. _cubeformat-ORIGIN:

**{ORIGIN (3x float)}**

    This set of three fields defines the displacement vector from the geometric origin of
    the system :math:`\left(0,0,0\right)` to the reference point
    :math:`\left(x_0, y_0, z_0\right)` for the
    spanning vectors defined in |XAXIS|, |YAXIS|, and |ZAXIS|.


.. _cubeformat-NVAL:

**{NVAL (int)}**

    If |NATOMS| is positive, this field indicates the number of data
    values :math:`N_V` that are recorded
    at each point in the voxel grid; it MAY be omitted, in which case
    a value of one is assumed.

    If |NATOMS| is negative, this field MUST be either absent or have
    a value of one.


.. _cubeformat-XAXIS:

**{XAXIS (int) (3x float)}**

    The first field on this line is an integer indicating the number of voxels
    :math:`N_X` present
    along the :math:`X`-axis of the volumetric region represented by the |CUBE| file. This
    value SHOULD always be positive; whereas the *input* to the ``cubegen`` [Gau16]_
    utility allows a negative value here as a flag for the units of the axis dimensions,
    in a |CUBE| file distance units MUST **always** be in Bohrs, and thus the 'units flag'
    function of a negative sign is superfluous. It is prudent to design applications to
    handle gracefully a negative value here, however.

    The second through fourth values on this line are the components of the vector
    :math:`\vec X`
    defining the voxel :math:`X`-axis.  They SHOULD all be non-negative; proper
    loading/interpretation/calculation behavior is
    not guaranteed if negative values are supplied. As noted in the
    Gaussian documentation [Gau16]_, the voxel axes need neither be orthogonal
    nor aligned with the geometry axes. However, many tools only support
    voxel axes that **are** aligned with the geometry axes (and thus are also orthogonal).
    In this case, the first
    ``float`` value :math:`\left(X_x\right)` will be positive and the other two
    :math:`\left(X_y\right.` and :math:`\left.X_z\right)` will be identically zero.


.. _cubeformat-YAXIS:

**{YAXIS (int) (3x float)}**

    This line defines the :math:`Y`-axis of the volumetric region of the |CUBE| file,
    in nearly identical fashion as for |XAXIS|.  The key differences are: (1) the
    first integer field :math:`N_Y` MUST always be positive; and (2) in the situation
    where the voxel axes
    aligned with the geometry axes, the second ``float`` field
    :math:`\left(Y_y\right)` will be positive and the first and third ``float``
    fields :math:`\left(Y_x\right.` and :math:`\left.Y_z\right)` will be
    identically zero.


.. _cubeformat-ZAXIS:

**{ZAXIS (int) (3x float)}**

    This line defines the :math:`Z`-axis of the volumetric region of the |CUBE| file,
    in nearly identical fashion as for |YAXIS|.  The key difference is that in
    the situation where the voxel axes are aligned with the geometry axes,
    the third ``float`` field
    :math:`\left(Z_z\right)` will be positive and the first and second ``float``
    fields :math:`\left(Z_x\right.` and :math:`\left.Z_y\right)` will be
    identically zero.


.. _cubeformat-GEOM:

**{GEOM (int) (float) (3x float)}**

    *This field MUST have* :math:`N_A` *rows of the below composition.*

    Each row of this field provides atom identity and position information for an
    atom in the molecular system of the |CUBE| file:

     * ``(int)`` - Atomic number of atom :math:`a`

     * ``(float)`` - Nuclear charge of atom :math:`a` (will deviate from the atomic
       number when an ECP is used)

     * ``(3x float)`` - Position of the atom in the geometric frame of
       reference :math:`\left(x_a, y_a, z_a\right)`


.. _cubeformat-DSET_IDS:

**{DSET_IDS (#x int)}**

    *This field is only present if* |NATOMS| *is negative*

    This field comprises one or more rows of integers, representing identifiers
    associated with multiple |DATA| values at each voxel, with a total of
    :math:`m+1` values present. The most common meaning of these identifiers
    is orbital indices, in |CUBE| files containing wavefunction data.
    The first value MUST be positive and equal to :math:`m`, to indicate the
    length of the rest of the list. Each of these :math:`m` values may be
    any integer, with the constraint that all values SHOULD be unique.
    Further, all :math:`m` values SHOULD be non-negative, as unpredictable
    behavior may result in some applications if negative integers are provided.


.. _cubeformat-DATA:

**{DATA (#x scinot)}**

    This field encompasses the remainder of the |CUBE| file.  Typical formatted |CUBE| output
    has up to six values on each line, in whitespace-separated scientific notation.
    Non-numeric data values are **not** supported and MUST NOT be present.

    If |NATOMS| is positive, a total of :math:`N_X N_Y N_Z N_V` values should
    be present, flattened as follows (in the below Python pseudocode the for-loop
    variables are iterated starting from zero)::

        for i in range(NX):
            for j in range(NY):
                for k in range(NZ):
                    for l in range(NV):

                        write(data_array[i, j, k, l])
                        if (k*NV + l) mod 6 == 5:
                            write('\n')

                write('\n')

    If |NATOMS| is negative and :math:`m` datasets are present (see
    |DSET_IDS| above), a total of
    :math:`N_X N_Y N_Z m` values should be present, flattened as follows::

        for i in range(NX):
            for j in range(NY):
                for k in range(NZ):
                    for l in range(m):

                        write(data_array[i, j, k, l])
                        if (k*m + l) mod 6 == 5:
                            write('\n')

                write('\n')

    The sequence of the data values along the last (``l``) dimension of the data array
    for each ``i, j, k`` MUST match
    the sequence of the identifiers provided in |DSET_IDS| in order for the dataset
    to be interpreted properly.

    Regardless of the sign of |NATOMS|, as illustrated above a newline is typically
    inserted after the block of data corresponding to each :math:`\left(X_i, Y_j\right)`
    pair.


