.. Exposition of CUBE file format

Gaussian CUBE File Format
=========================

Disclaimer
----------

The CUBE file format as described here is **NOT** an official specification, sanctioned
by Gaussian, Inc. It is instead this author's best effort to provide a complete
description of the contents of the majority of CUBE files in circulation, as represented
by the small subset encountered by this author. **FILES FORMATTED TO THIS SPECIFICATION
MAY NOT BE COMPATIBLE WITH ALL SOFTWARE SUPPORTING CUBE FILE INPUT.**

Overview
--------

The CUBE file format is described on the Gaussian webpage as part of the
documentation of the ``cubegen`` utility [Gau16]_. As noted there, **all data**
in CUBE files MUST be stored in atomic units (electrons and Bohrs, and units derived
from these).

The format specification on the webpage of the VMD visualization program [UIUC16]_
provides a cleaner layout of one possible arrangement of the needed contents. In particular,
the Gaussian specification is ambiguous about whitespace requirements, so parsing of CUBE
files SHOULD accommodate some variation in the format, including (i) variable
amounts/types of whitespace between the values on
a given line, and (ii) the presence of leading and/or trailing whitespace on a given line.

The CUBE file format as laid out below uses tagged fields (``{FIELD (type)}``) to indicate
the types of the various data elements and where they are located in the file.
Descriptions of the fields are provided below the field layout.  Lowercase algebraic symbols
:math:`\left(x\right.`, :math:`y`, :math:`\left. z\right)` indicate coordinates in the frame
of the molecular geometry, whereas uppercase algebraic symbols
:math:`\left(X\right.`, :math:`Y`, :math:`\left. Z\right)` indicate coordinates in the
voxel grid defined by ``{XAXIS}``, ``{YAXIS}``, and ``{ZAXIS}``.

All fields except for
``{DSET_IDS}``  and ``{NVAL}`` MUST be present in all files.

``{DSET_IDS}`` MUST be present if
``{NATOMS}`` is negative; it MUST NOT be present if ``{NATOMS}`` is positive.

``{NVAL}`` may be omitted if its value would be equal to one; it MUST be absent or
have a value of one if ``{NATOMS}`` is negative.

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

Field Contents
--------------

    :ref:`{COMMENT1} and {COMMENT2} <cubeformat-COMMENTS>` |br|
    :ref:`{NATOMS} <cubeformat-NATOMS>` |br|
    :ref:`{ORIGIN} <cubeformat-ORIGIN>` |br|
    :ref:`{NVAL} <cubeformat-NVAL>` |br|
    :ref:`{XAXIS} <cubeformat-XAXIS>` |br|
    :ref:`{YAXIS} <cubeformat-YAXIS>` |br|
    :ref:`{ZAXIS} <cubeformat-ZAXIS>` |br|
    :ref:`{GEOM} <cubeformat-GEOM>` |br|
    :ref:`{DSET_IDS} <cubeformat-DSET_IDS>` |br|
    :ref:`{DATA} <cubeformat-DATA>`


Field Descriptions
------------------

.. _cubeformat-COMMENTS:

**{COMMENT1 (str)}** and **{COMMENT2 (str)}**

    Two lines of text at the head of the file. Per VMD [UIUC16]_, by convention ``{COMMENT1}``
    is typically the title of the system and ``{COMMENT2}`` is a description of the
    property/content stored in the file, but they MAY be anything.

.. _cubeformat-NATOMS:

**{NATOMS (int)}**

    This first field on the third line indicates the number of atoms present in the system.
    A negative value here indicates the CUBE file MUST contain the ``{DSET_IDS}`` line(s); a
    positive value indicates the file MUST NOT contain this/these lines.

    The absolute value of ``{NATOMS}`` defines the number of rows of molecular geometry data
    that MUST be present in ``{GEOM}``.

    The CUBE specification is silent as to whether a zero value is permitted for ``{NATOMS}``;
    most applications likely **do not** support CUBE files with no atoms.

.. _cubeformat-ORIGIN:

**{ORIGIN (3x float)}**

    This set of three fields defines the displacement vector from the geometric origin of
    the system to the reference point :math:`\left(x_0, y_0, z_0\right)` for the
    spanning vectors defined in ``{XAXIS}``, ``{YAXIS}``, and ``{ZAXIS}``.

.. _cubeformat-NVAL:

**{NVAL (int)}**

    If ``{NATOMS}`` is positive, this field indicates how many data values are recorded
    at each point in the voxel grid; it MAY be omitted, in which case a value of one
    is assumed.

    If ``{NATOMS}`` is negative, this field MUST be either absent or have a value of
    one.

.. _cubeformat-XAXIS:

**{XAXIS (int) (3x float)}**

    The first field on this line is an integer indicating the number of voxels
    :math:`N_X` present
    along the :math:`X`-axis of the volumetric region represented by the CUBE file. This
    value SHOULD always be positive; whereas the *input* to the ``cubegen`` [Gau16]_
    utility allows a negative value here as a flag for the units of the axis dimensions,
    in a CUBE file distance units MUST **always** be in Bohrs, and thus the 'units flag'
    function of a negative sign is superfluous.

    The second through fourth values on this line are the components of the vector
    :math:`\vec X`
    defining the voxel :math:`X`-axis.  They SHOULD all be positive. As noted in the
    Gaussian documentation [Gau16]_, the voxel axes need not be orthogonal
    nor aligned with the geometry axes. However, many tools only support
    voxel axes that are aligned with the geometry axes.  In this case, the first
    ``float`` value :math:`\left(X_x\right)` will be positive and the other two
    :math:`\left(X_y\right.` and :math:`\left.X_z\right)` will be identically zero.

.. _cubeformat-YAXIS:

**{YAXIS (int) (3x float)}**

    This line defines the :math:`Y`-axis of the volumetric region of the CUBE file,
    in nearly identical fashion as for ``{XAXIS}``.  The key differences are that the
    first integer field :math:`N_Y` MUST always be positive, and that for voxel axes
    aligned with the geometry axes, the second ``float`` field
    :math:`\left(Y_y\right)` will be positive and the first and third ``float``
    fields :math:`\left(Y_x\right.` and :math:`\left.Y_z\right)` will be
    identically zero.

.. _cubeformat-ZAXIS:

**{ZAXIS (int) (3x float)}**

    This line defines the :math:`Z`-axis of the volumetric region of the CUBE file,
    in nearly identical fashion as for ``{YAXIS}``.  The key difference is that for
    voxel axes aligned with the geometry axes, the third ``float`` field
    :math:`\left(Z_z\right)` will be positive and the first and second ``float``
    fields :math:`\left(Z_x\right.` and :math:`\left.Z_y\right)` will be
    identically zero.

.. _cubeformat-GEOM:

**{GEOM (int) (float) (3x float)}**

    *This field MUST have multiple rows, equal to the absolute value of*
    ``{NATOMS}``

    Each row of this field provides atom identity and position information for an
    atom in the molecular system of the CUBE file:

     * ``(int)`` - Atomic number of atom :math:`a`

     * ``(float)`` - Nuclear charge of atom :math:`a` (will deviate from the atomic
       number when an ECP is used)

     * ``(3x float)`` - Position of the atom in the geometric frame of
       reference :math:`\left(x_a, y_a, z_a\right)`

.. _cubeformat-DSET_IDS:

**{DSET_IDS (#x int)}**

    *This field is only present if* ``{NATOMS}`` *is negative*

    This field comprises one or more rows of integers, with a total of :math:`m+1`
    values present. The first value MUST be equal to :math:`m`, to indicate the
    length of the list; each remaining value may be any integer. There SHOULD NOT
    be any repeated integers between the second and final elements of the list,
    inclusive.

.. _cubeformat-DATA:

**{DATA (#x scinot)}**

    This field encompasses the remainder of the CUBE file.  Typical formatted CUBE output
    has up to six values on each line, in whitespace-separated scientific notation.

    If ``{NATOMS}`` is positive, a total of :math:`N_X N_Y N_Z*` ``{NVAL}`` values should
    be present, flattened as follows (in the below Python pseudocode the for-loop
    variables are iterated starting from zero)::

        for i in range(NX):
            for j in range(NY):
                for k in range(NZ):
                    for l in range({NVAL}):

                        write({DATA}[i, j, k, l])
                        if (k*{NVAL} + l) mod 6 == 5:
                            write('\n')

                write('\n')

    If ``{NATOMS}`` is negative and :math:`m` datasets are present (see
    :ref:`{DSET_IDS} <cubeformat-DSET_IDS>` above), a total of
    :math:`N_X N_Y N_Z m` values should be present, flattened as follows::

        for i in range(NX):
            for j in range(NY):
                for k in range(NZ):
                    for l in range(m):

                        write({DATA}[i, j, k, l])
                        if (k*{NVAL} + l) mod 6 == 5:
                            write('\n')

                write('\n')

    Regardless of the value of ``{NATOMS}``, as illustrated above a newline is typically
    inserted after the block of data corresponding to each :math:`\left(X_i, Y_j\right)`
    pair is written.

