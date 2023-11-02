# simnet

Python Package for the creation and analysis of similarity networks.

<!-- Project Organization
--------------------

    .
    ├── AUTHORS.md
    ├── LICENSE
    ├── README.md
    ├── notebooks
    └── src/simnet
        ├── clustering
        ├── datasets
        ├── graph
        ├── plotting
        ├── similarity
        └── utils 
-->


## Installation

The source code for this project can be installed using pip. 
```
pip install .
```
To remove the package simply use 
```
pip uninstall simnet
```

### Developer Mode
To install in developer mode (have changes in source code update without reinstallation) add `-e` flag
```
pip install -e .
```
Note: removing the package is slightly more complicated and a different command is needed to uninstall 
```
python setup.py develop -u
```

### Graph Tool
There is one dependency that cannot be installed through pip - `Graph-Tool`. This is a result of it's underlying `c++` dependencies.
The simplest method for python users is to make use of a conda environment, install this package using the commands above and install `graph-tool` using `conda-forge`
```
conda install -c conda-forge graph-tool
```
Note: this will not work on Windows. Alternative (conda independent) solutions can be found on the [Graph Tool Website](https://git.skewed.de/count0/graph-tool/-/wikis/installation-instructions#installing-via-conda)

# Using `simnetpy`
```Python
import simnet as sn

# create mixed guassian data with 100 nodes, 2 dimensions and 3 equally sized clusters.
N = 100
sizes=np.array([34,33,33])
d = 2
dataset = sn.datasets.mixed_multi_guassian(len(sizes), d, N, sizes=sizes)

# calculate pairwise similarity
S = sn.pairwise_sim(dataset.X, method='euclidean', norm=True)

# Create igraph Igraph from matrix
gg = phd.network_from_sim_mat(S, method='knn', K=5)

# print graph stats
print(g.graph_stats())

# cluster
ylabels = sn.clustering.leiden_clustering(gg, nsamples=20)

# cluster quality
cqual = clustering.cluster_quality(gg, ylabels)
print(cqual)
```

