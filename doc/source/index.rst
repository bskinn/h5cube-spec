.. h5cube Format Specification documentation master file, created by
    sphinx-quickstart on Tue Dec  6 21:10:22 2016.
    You can adapt this file completely to your liking, but it should at least
    contain the root `toctree` directive.

h5cube File Specification
=========================

Gaussian |CUBE| files are a common format for storing molecular geometric and
volumetric field data from quantum/computational chemical calculations. The data
in these files is stored as plain text, and thus their compressibility by
standard tools such as ``gzip`` and ``bzip2`` is limited, even in cases where
the numerical structure of the dataset itself might be well suited for
greater compression by other means.

It is the purpose of this document to define a file specification for storing
the data contained in Gaussian |CUBE| files in the binary
`HDF5 <https://support.hdfgroup.org/HDF5/>`__ |extlink| format. HDF5
was chosen due to its acceptance across numerous disciplines as a standardized,
cross-platform data storage format, and for the free, cross-platform compression
algorithms integrated into it
(see `here <https://support.hdfgroup.org/hdf5-quest.html#gcomp>`__ |extlink|).
In circumstances where 'semi-lossy' compression (e.g., truncation of precision
and/or data thresholding) is
acceptable, particularly large reductions in file size are feasible.
Documentation at the companion Python project ``h5cube``
(`ReadTheDocs <http://h5cube.readthedocs.io/en/stable/>`__ |extlink|\|
`GitHub <https://github.com/bskinn/h5cube>`__ |extlink|) will eventually
illustrate representative compression factors achievable in the |h5cube|
file format; preliminary data can be found at this
`Google Spreadsheet <https://docs.google.com/spreadsheets/d/1AajEYpacgq48X72_HuarVLVA517ZY4htaEWf1tLY5Cc/edit#gid=0>`__
|extlink|.

Definition of an explicit specification for the |h5cube| format is
anticipated to facilitate direct, cross-platform binary read and write of
|CUBE| data.  Particular advantages should be observed by applications aware
of the HDF5 format and of this specification when reading data,
gained from rapid retrieval of individual data points or subsets directly
from |h5cube| files without the need to load the full dataset.  Even in
instances where the full dataset must be loaded into memory, the disk
usage will still be significantly reduced in most cases, since it should
be unnecessary to recreate an intermediate uncompressed |CUBE| file.

The Gaussian |CUBE| file format itself  is also delineated
:doc:`here <cubeformat>`, using a "field"-style syntax for convenient
cross-reference from the various version(s) of the |h5cube| specification.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
:rfc:`2119`.  The specification versioning follows in the spirit of
`Semantic Versioning <http://semver.org>`__; see the
:doc:`root specifications page <specs>` for more information.

Contents:

.. toctree::
    :maxdepth: 2
    :titlesonly:

    cubeformat
    h5cube Specifications <specs>
    references



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

