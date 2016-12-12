.. Exposition of CUBE file format

Gaussian CUBE File Format
=========================

The CUBE file format is delineated on the Gaussian webpage as part of the
description of the ``cubegen`` utility [Gau14]_. As noted there, **all data**
in CUBE files is to be stored in atomic units (electrons and Bohrs).

The format specification on the webpage of the VMD visualization program [UIUC16]_
provides a cleaner layout of one possible arrangement of the needed contents. In particular,
the Gaussian specification is ambiguous about whitespace requirements, so parsing of CUBE
files has to accommodate the possibility of variability in the exact format of
any given CUBE file.

The CUBE file format as laid out below uses tagged fields (``{FIELD (type)}``) to indicate
the types of the various data elements and where they are located in the file.
Descriptions of the fields are provided below the format layout.

::

    {COMMENT1 (str)}
    {COMMENT2 (str)}
    {NATOMS (int)} {ORIGIN (3x float)}
    {XAXIS (int) (3x float)}
    {YAXIS (int) (3x float)}
    {ZAXIS (int) (3x float)}
    {GEOM (int) (float) (3x float)}
    {DSET_IDS (int) (#x int)}
    {DATA (#x exp)}

**{COMMENT1 (str)}** and **{COMMENT2 (str)}**

Two lines of text at the head of the file. Per VMD [UIUC16]_, by convention these are
typically (1) the title of the system and (2) a description of the property/content stored
in the file.

**{NATOMS (int)}**

The third line ...

