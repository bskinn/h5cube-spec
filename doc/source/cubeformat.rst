.. Exposition of CUBE file format

Gaussian CUBE File Format
=========================

Overview
--------

The CUBE file format is delineated on the Gaussian webpage as part of the
description of the ``cubegen`` utility [Gau14]_. As noted there, **all data**
in CUBE files MUST be stored in atomic units (electrons and Bohrs, and units derived
from these).

The format specification on the webpage of the VMD visualization program [UIUC16]_
provides a cleaner layout of one possible arrangement of the needed contents. In particular,
the Gaussian specification is ambiguous about whitespace requirements, so parsing of CUBE
files SHOULD accommodate the possibility of variability in the exact format of
any given CUBE file, including (i) variable amounts/types of whitespace between the values on
a given line, and (ii) the presence of leading and/or trailing whitespace on a given line.

The CUBE file format as laid out below uses tagged fields (``{FIELD (type)}``) to indicate
the types of the various data elements and where they are located in the file.
Descriptions of the fields are provided below the field layout.  Lowercase algebraic symbols
:math:`\left(x\right.`, :math:`y`, :math:`\left. z\right)` indicate coordinates in the frame
of the molecular geometry, whereas uppercase algebraic symbols
:math:`\left(X\right.`, :math:`Y`, :math:`\left. Z\right)` indicate coordinates in the
voxel grid defined by ``{XAXIS}``, ``{YAXIS}``, and ``{ZAXIS}``.

All fields except for
``{DSET_IDS}`` MUST be present in all files. ``{DSET_IDS}`` MUST be present if
``{NATOMS}`` is negative; it MUST NOT be present if ``{NATOMS}`` is positive.

Field Layout
------------

::

    {COMMENT1 (str)}
    {COMMENT2 (str)}
    {NATOMS (int)} {ORIGIN (3x float)}
    {XAXIS (int) (3x float)}
    {YAXIS (int) (3x float)}
    {ZAXIS (int) (3x float)}
    {GEOM (int) (float) (3x float)}
          .
          .
    {DSET_IDS (#x int)}
          .
          .
    {DATA (#x exp)}
          .
          .

Field Contents
--------------

    :ref:`{COMMENT1} and {COMMENT2} <cubeformat-COMMENTS>` |br|
    :ref:`{NATOMS} <cubeformat-NATOMS>` |br|
    :ref:`{ORIGIN} <cubeformat-ORIGIN>` |br|
    :ref:`{XAXIS} <cubeformat-XAXIS>` |br|
    :ref:`{YAXIS} <cubeformat-YAXIS>` |br|
    :ref:`{ZAXIS} <cubeformat-ZAXIS>` |br|
    :ref:`{GEOM} <cubeformat-GEOM>` |br|
    [...]


Field Descriptions
------------------

.. _cubeformat-COMMENTS:

**{COMMENT1 (str)}** and **{COMMENT2 (str)}**

    Two lines of text at the head of the file. Per VMD [UIUC16]_, by convention these are
    typically (1) the title of the system and (2) a description of the property/content stored
    in the file, but they MAY be anything.

.. _cubeformat-NATOMS:

**{NATOMS (int)}**

    This first field on the third line indicates the number of atoms present in the system.
    A negative value here indicates the CUBE file MUST contain the ``{DSET_IDS}`` line(s); a
    positive value indicates the file MUST NOT contain this/these lines.

    The absolute value of ``{NATOMS}`` defines the number of rows of molecular geometry data
    that MUST be present in ``{GEOM}``.

.. _cubeformat-ORIGIN:

**{ORIGIN (3x float)}**

    This set of three fields defines the displacement vector from the geometric origin of
    the system to the reference point :math:`\left(x_0, y_0, z_0\right)` for the
    spanning vectors defined in ``{XAXIS}``, ``{YAXIS}``, and ``{ZAXIS}``.

.. _cubeformat-XAXIS:

**{XAXIS (int) (3x float)}**

    The first field on this line is an integer indicating the number of voxels present
    along the :math:`X`-axis of the volumetric region represented by the CUBE file. This
    value SHOULD always be positive; whereas the *input* to the ``cubegen`` [Gau14]_
    utility allows a negative value here as a flag for the units of the axis dimensions,
    in a CUBE file distance units SHOULD **always** be in Bohrs, and thus the 'units flag'
    function of a negative sign is superfluous.

    The second through fourth values on this line are the components of the vector
    defining the voxel :math:`X`-axis.  They SHOULD all be positive. As noted in the
    Gaussian documentation [Gau14]_, the voxel axes need not be orthogonal to each
    other nor aligned with the geometry axes. However, many tools only support
    voxel axes that are aligned with the geometry axes.  In this case, the first
    ``float`` value will be positive and the other two will be identically zero.

.. _cubeformat-YAXIS:

**{YAXIS (int) (3x float)}**

    This line defines the :math:`Y`-axis of the volumetric region of the CUBE file,
    in nearly identical fashion as for ``{XAXIS}``.  The key differences are that the
    first integer field MUST always be positive, and that for voxel axes
    aligned with the geometry axes, the second ``float`` field will be positive and
    the first and third ``float`` fields will be identically zero.

.. _cubeformat-ZAXIS:

**{ZAXIS (int) (3x float)}**

    This line defines the :math:`Z`-axis of the volumetric region of the CUBE file,
    in nearly identical fashion as for ``{YAXIS}``.  The key difference is that for
    voxel axes aligned with the geometry axes, the third ``float`` field will be
    positive and the first and second ``float`` fields will be identically zero.

.. _cubeformat-GEOM:

**{GEOM (int) (float) (3x float)}**

    *This field will have multiple rows, equal to the absolute value of*
    ``{NATOMS}``

    [...]

