.. h5cube Format Specification documentation master file, created by
    sphinx-quickstart on Tue Dec  6 21:10:22 2016.
    You can adapt this file completely to your liking, but it should at least
    contain the root `toctree` directive.

h5cube File Specification
=========================

Gaussian CUBE files are a common format for storing molecular geometric and
volumetric field data from quantum/computational chemical calculations. The data
in these files is stored as plain text, and thus their compressibility by
standard tools such as ``gzip`` and ``bzip2`` is limited, even in cases where
the numerical structure of the dataset itself might be well suited for
greater compression by other means.

It is the purpose of this document to define a file specification for storing
the data contained in Gaussian CUBE files in the binary
`HDF5 <https://support.hdfgroup.org/HDF5/>`__ |extlink| format. [More specifically, this
specification aims to facilitate storing such data in a fashion that
is amenable to the enhanced compression methods available in the HDF5 format
(see `here <https://support.hdfgroup.org/hdf5-quest.html#gcomp>`__ |extlink|, especially
in circumstances where 'semi-lossy'
compression is acceptable. (eventually link to h5cube docs & the high comp factors
achievable with truncation and thresholding)]

[Facilitate interoperable read/write of CUBE data to this binary format.]

[Particular potential advantage is enabling read of individual points or data subsets by software aware of the
specification, streamlining use of the data if the full dataset is not needed]

[Mention CUBE file format is laid out here, and that the various version(s) of the specification
refer back to that format as laid out here using the particular syntax defined there.]

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
:rfc:`2119`.

Contents:

.. toctree::
    :maxdepth: 2

    cubeformat
    h5cube Specifications <specs>
    references



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

