GAlib – Graph Analysis library in Python / NumPy
================================================

GAlib is a library for the analysis of graphs and complex networks in Python/NumPy. The library is very easy to install, use, modify and extend.

It's main features are...

- extensive use of NumPy to boost performance over pure Python code,
- networks are represented by their adjacency matrices (rank-2 ndarrays),
- transparent and flexible,
- includes "*Utility Scripts*" useful also for non-(Python)-programmers,
- open-source license,

... and some limitations:

- limited management of large networks due to NumPy dependence,
- no graph visualization tools.


INSTALLATION
------------

GAlib does not require installation but requires to have NumPy installed. In order to use some accelerated functions that were too slow, the package Numba is an optional requirement. The library can be downloaded from its GitHub repository:

https://github.com/gorkazl/pyGAlib

At the bottom of the right-hand menu click on the "*Download ZIP*" button. Unzip the file and copy the modules into the standard "*Site-Packages*" folder of your current Python distribution. GAlib is composed of three files: *galib.py*, *gamodels.py* and *gatools.py*. The optional module *galib_numba.py* includes faster functions thanks to use of the Numba package. Import the modules as usual to start using them, e.g.: ::

>>> from galib import*
>>> from gamodels import*
>>> from gatools import*

For more details see the User Guide in the */Docs* folder.


HOW TO FIND FURTHER DOCUMENTATION
---------------------------------

While working in an interactive session and having imported the modules, use the ``help()`` function to obtain information of the library files: ::

>>> help(modulename)

This will show a list of functions included in the module. For further details regarding each function, type: ::

>>> help(functionname)

For IPython users, the help command is replaced by a question mark after the module's or function's name, e.g.: ::

>>> modulename?
>>> functionname?


CONTACT INFORMATION
-------------------

GAlib will have soon its own webpage and domain. For the moment, contact me at < galib@Zamora-Lopez.xyz > for any questions, bug reports, etc.


FUTURE DEVELOPMENTS
-------------------

The current version includes core functionalities for graph analysis. Future releases will include:

* accelaration of slowest functions using the Numba package,
* further measures for weighted and/or directed networks,
* further classical (textbook) graph models,
* extended data conversions between graph formats,
* support for sparse matrices to increase the size of networks handled, and
* ... any extensions/functions you want to include.

**Third party collaborations to extend GAlib are highly welcome!**


HISTORY OF CHANGES
------------------

May 3\ :sup:`rd`, 2017
^^^^^^^^^^^^^^^^^^^^^^
- Today I have added a new module to the library: *galib_extra.py*. This module does not provide core functionalities for the analysis of complex networks. The module is intended to host code and measures I have either developed as the result of my research, or third-party measures and functionalities which I have adapted myself into Python. These functions and measures are all related to complex network analysis and network dynamics but cannot be strictly regarded as typical graph analysis. It includes functions to compute the *Functional Complexity* and the *Topological Similarity* measures we have recently published: Zamora-Lopez et al. “*Functional complexity emerging from anatomical constraints in the brain: the significance of network modularity and rich-clubs*” Sci. Reps. 6:38424 (2016) [DOI: 10.1038/srep38424], and Bettinardi et al “*How structure sculpts function: Unveiling the contribution of anatomical connectivity to the brain’s spontaneous correlation structure*” Chaos 27, 047409 (2017) [DOI: 10.1063/1.4980099].


August 6\ :sup:`th`, 2016
^^^^^^^^^^^^^^^^^^^^^^^^^
- Function ``gamodels.RandomGraph()`` improved. Method to choose source and target nodes to connect changed. Originally I would use the official ``random.choice()`` function to select nodes from the list of nodes. Now it uses ``N * numpy.random.rand()`` to choose the index. The latter was slower years ago but with newer Numpy versions, it has become a faster option. This change also allows better use of Numba. Faster generation functions coming soon!

September 14\ :sup:`th`, 2015
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
- Function ``gatools.AllBipartitions()`` improved and extended. (i) Internal dependence with function ``gatools.AllCombinations()`` removed, (ii) function is now faster, and (iii) optional parameter *’comblength’* has been introduced in case that only the bipartitions of given length are desired.

August 24\ :sup:`th`, 2015
^^^^^^^^^^^^^^^^^^^^^^^^^^
- Solved a bug in function ``galib.RichClub()`` that affected only the calculations with the option *’average’*.


August 1\ :sup:`st`, 2015
^^^^^^^^^^^^^^^^^^^^^^^^^
- Pulled and merged into master branch changes by Schmigu (see update on June 14\ :sup:`th`).
- The function ``ModularInhomogeneousGraph()`` was added to *gamodels.py* module to generate random modular networks in which the size and/or the density of each module can be specified.
- Example in ``gatools.ExtractSubmatrix()`` corrected. The example used a 3x3 array when a 4x4 array was required.


June 14\ :sup:`th`, 2015
^^^^^^^^^^^^^^^^^^^^^^^^
- started adding unit-tests
- removed ``gatools.ArrayCompare()`` since the function was broken. The functionality is covered by ``numpy.array_equal()``
- fixed bug in ``gatools.Quartiles()``

April 13\ :sup:`th`, 2015
^^^^^^^^^^^^^^^^^^^^^^^^^

Function to compute the Fisher-corrected mean correlation values, ``MeanCorrelation()``, has been added to *gatools.py* module.

December 23\ :sup:`rd`, 2014
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Following publication of Klimm et al. “*Individual node’s contribution to the mesoscale of complex networks*” New J. Phys. 16:125006 (2014), functions to compute the roles of nodes have been included into the main library *galib.py*. Individual functions for each of the four new measures  are available:

- ``GlobalHubness()``, ``LocalHubness()``, ``NodeParticipation()``, ``NodeDispersion()``.
- Function name ``ParticipationIndex()`` changed to ``NodePArticipation()``.
- Additionally, the function ``NodeRoles()`` returns all the four measures at once.
- Functions to compute the *participation matrix* and the *participation vectors* of every node have been included.


February 24\ :sup:`th`, 2014
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Since the official release on September 10\ :sup:`th` 2013, I have performed several changes, some of them thanks to the feedback from a few colleagues. Thanks in particular to Miguel Lechón and to Nikos Kouvaris. Here the list of changes:

- Issues with recurrent imports solved. Only absolute imports are allowed in the modules.
- ``Degree()`` function in *galib*.py module modified to exploit properties of boolean ndarrays.
- Functions to compute roles of nodes in modular networks included to *galib.py*.
- ``BarabasiAlbert()`` function in *gamodels.py* is now always initialized with a fully connected subgraph of ``m+1`` nodes. Otherwise some hubs remained disconnected.
- ``Reciprocity()`` function in *galib.py* is now faster using boolean ndarrays. The parameter ``weighted`` has been omitted for useless and confusing.
- ``RewireNetwork()`` in *gamodels.py* has been corrected. In the very particular case of undirected graphs with assymetric link weights, weigths were not conserved. Now all nodes conserve their input intensity also in that case.
- A new module has been included: *galib_numba.py*. This is intended for the slowest functions of GAlib to be accelerated using the Numba package. Users with Numba installed can call those faster functions independently of the main galib import. For the moment I only included my main priority, a fast function for the Floyd-Warshall algorithm, ``FloydWarshall_Numba()``.



