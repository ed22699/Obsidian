---
tags:
  - data_ingress
---

- Binary format
- File system-like access
- is a format for serialising data
- **core concepts**:
	- *Datasets*: array-like collections of data
	- *Groups*: folder-like structures that contains datasets and other groups
	- *Metadata*: add information that pertains to all datasets
- lets you store huge amounts of numerical data, and easily manipulate that data from numpy
- Thousands of datasets can be stored in a single file, categorised and tagged however you want
- unlike numpy arrays, they support a variety of transparent storage features such as compression, error-detections, and chunked I/O
### Example script
```python
import h5py
import numpy as np

# Create a HDF5 file
f = h5py.File("mytestfile.hdf5", "w")

# Add a new dataset to the file: integer array of lengh 100
dset = f.create_dataset("mydataset", (100,), dtype="i")

# Assign values to the dataset
dset[...] = np.arange(100)

# Add a group called subgroup, with a dataset underneath
dset2 = f.create_dataset("subgroup/dataset_two", (10,), dtype="i")

# Store metadata in the HDF5 file object
dset.attrs["author"] = "nt"
dset.attrs["date"] = "24/01/2018"
```
- basically you can see HDF5 as a file system within a file, where files are datasets and folders are groups. However, the HDF Group doesn't seem to like this comparison. The major differences are as follows:
	- An HDF5 file is *portable*: the entire structure is contained in the file and doesn't depend on the underlying file system. However it does depend on the HDF5 library
	- HDF5 datasets have a *rigid structure*: they are all homogeneous (hyper)rectangular numerical arrays, whereas files in a file system can be anything
	- You can *add metadata to groups*, whereas file systems don't support this