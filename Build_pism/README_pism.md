## This file tells how to build prerequisites and pism on Cheyenne
``` Last Modified by Weiwen Ji on Mar.8 2019 weiwen_ji@fas.harvard.edu```

###   ===============   Load and Install Prerequisities   ===============
       
    1). # Install fftw3-mpi
          Download: http://www.fftw.org/download.html
        # Configure
          ./configure --prefix=.. -enable-shared --enable-static --enable-mpi 
          make -j 8
          make install

    2). # Install udunits2
          Download: ftp://ftp.unidata.ucar.edu/pub/udunits/
        # Configure and make
          ./configure --prefix=/glade/u/home/jweiwen/wji_apps/udunits2 CC=mpicc
          make check
          make install
          make clean
          
     3). # Install PETSc
         # Download
         git clone -b maint https://bitbucket.org/petsc/petsc petsc
         # Configure
         CC=mpicc CXX=mpicxx ./config/configure.py --with-shared-libraries --with-debugging=0 --with-fc=0 --with-clanguage=c

Mar.11 2019 Just use ./configure to configure PETSc         

         # make
         qsub -I -l select=1:ncpus=8:mpiprocs=8 -l walltime=10:00:00 -q regular -A UHAR0005
         make PETSC_DIR=$PETSC_DIR PETSC_ARCH=$PETSC_ARCH all
         make PETSC_DIR=$PETSC_DIR PETSC_ARCH=$PETSC_ARCH check
         
###   ===============   Build PISM   ===============

```
   # Download  
   git clone git://github.com/pism/pism.git pism-stable
   mkdir ~/pism-stable/build
   cd ~/pism-stable/build
   PISM_INSTALL_PREFIX=~/pism CC=mpicc CXX=mpicxx cmake .. -DPETSC_EXECUTABLE_RUNS=ON
   # May have some failed tests
   make install -j 8
 ```
