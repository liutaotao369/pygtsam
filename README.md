# pygtsam
Python wrappers for [GTSAM 3](https://research.cc.gatech.edu/borg/download?destination=node%2F299). 

This previously lived [here](https://github.com/spillai/conda-recipes-slam/tree/master/pygtsam/pygtsam) but it made sense to move it a separate repo. 

## Build Instructions
GTSAM 3.2.1 (https://research.cc.gatech.edu/borg/sites/edu.borg/files/downloads/gtsam-3.2.1.zip)
 - There is a bug with Factor removal in GTSAM 3.2.1, see: https://bitbucket.org/gtborg/gtsam/pull-requests/272/fix-recalculate-batch-step-when-variables/diff
 - replace ..../gtsam-3.2.1/gtsam/nonlinear/ISAM2.cpp with https://github.com/spillai/pygtsam/blob/dev/fixedlag/factor_removal_fix/ISAM2.cpp; this is critical to enable fixed-lag smoothing
 - replace ..../gtsam-3.2.1/gtsam/nonlinear/ISAM2.h with https://github.com/spillai/pygtsam/blob/dev/fixedlag/factor_removal_fix/ISAM2.h; this allows us to enable/disable factor ID reuse after factor removal
 - note: you may have issues with C++ Boost, especially with ver. 1.58 or greater; you may have to build ver. 1.57 from source at: https://sourceforge.net/projects/boost/files/boost/1.57.0/, using instructions at: http://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html; the required Boost libraries are: python,serialization,system,filesystem,thread,program_options,date_time,regex,timer,chrono
 - build from source 
   - cd gtsam-3.2.1; mkdir build; cd build
   - cmake -DCMAKE_INSTALL_PREFIX=..../gtsam-3.2.1/ -DGTSAM_WITH_EIGEN_MKL=OFF -DGTSAM_WITH_EIGEN_MKL_OPENMP=OFF -DGTSAM_BUILD_EXAMPLES_ALWAYS=OFF -DGTSAM_BUILD_TESTS=OFF ..
   - make install
 - export LIBRARY and INCLUDE paths to add include and lib directories of CMAKE_INSTALL_PREFIX
 
Eigen 3 (sudo apt-get install libeigen3-dev)

Boost-Python (sudo apt-get install libboost-python-dev)

SuiteSparse (sudo apt-get install libsuitesparse-dev)

Google GLOG (sudo apt-get install libgoogle-glog-dev)

pygtsam
 - git clone https://github.com/spillai/pygtsam.git
 - build from source
   - cd pygtsam; mkdir build; cd build
   - cmake -DCMAKE_INSTALL_PREFIX=..../gtsam-3.2.1 -DCMAKE_PREFIX_PATH=..../gtsam-3.2.1/lib/cmake/GTSAM ..
   - make install
 - export PYTHONPATH to add lib directory of CMAKE_INSTALL_PREFIX

## Contribute
Feel free to contribute new factors and python-based applications for GTSAM on this branch, I'm sure [Frank Dellaert](http://www.cc.gatech.edu/~dellaert/FrankDellaert/Frank_Dellaert/Frank_Dellaert.html) will be ecstatic that more people are using factor graphs. 
