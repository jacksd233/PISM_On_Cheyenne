## This file tells how to build prerequisites and pism on Cheyenne
``` Last Modified by Weiwen Ji on Mar.8 2019 weiwen_ji@fas.harvard.edu```

###   ===============   Load and Install Prerequisities   ===============

`Mar.12 2019`  (http://pism-docs.org/sphinx/installation/pism.html?highlight=precise)
    
   Add options to get reproducible model results:
   
    `export CFLAGS="-fp-model precise"`
    `export CXXFLAGS="-fp-model precise".` 
    
### Begin Installation    
     
      . # Install gsl-2.5
          Download: https://www.gnu.org/software/gsl/
        # Configure and build
          ./configure --prefix=/home/yourname/gsl
          make 
          make check 
          make install
          make clean
     
    1). # Install fftw3-mpi
          Download: http://www.fftw.org/download.html
        # Configure
          ./configure --prefix=.. --enable-shared --enable-static --enable-mpi 
          make -j 8
          make install
          make clean

    2). # Install udunits2
          Download: ftp://ftp.unidata.ucar.edu/pub/udunits/
        # Configure and make
          ./configure --prefix=/glade/u/home/jweiwen/wji_apps/udunits2 CC=mpicc
          make check
          make install
          make clean
          
    3). # Install PETSc
         # Download
          git clone -b maint https://gitlab.com/petsc/petsc.git petsc
         # Configure
   ~~CC=mpicc CXX=mpicxx ./config/configure.py --with-shared-libraries --with-debugging=0 --with-fc=0 --with-clanguage=c~~
    

`Mar.11 2019`
        Just use `./configure --with-debugging=0` to configure PETSc
 
`Mar.14 2019`

        PETSc built with batch. (https://www.mcs.anl.gov/petsc/documentation/installation.html)
        
        ./config/configure.py \
           --with-fc=0 --with-batch --with-valgrind=1 --with-mpiexec="mpirun" \
           --with-shared-libraries=1 -known-mpi-shared-libraries=1 \
           --with-64-bit-indices=1 --known-64-bit-blas-indices
        the above configure run will create a binary conftest 
        
        ./configure --with-batch --with-fc=0 \
          --known-64-bit-blas-indices --with-64-bit-indices=1 -known-mpi-shared-libraries=1
          
        Mar.15:
        ./config/configure.py \
            --with-fc=0 \
            --with-64-bit-indices=1 \
            --known-64-bit-blas-indices \
            --known-mpi-shared-libraries=1 \
            --with-debugging=0 \
            --with-valgrind=1 \
            --with-batch=1  \
            --with-shared-libraries=1 \
            --with-mpiexec="mpirun" \
            --download-f2cblaslapack=1
        
        
        Submit ./conftest-arch-linux2-c-debug to 1 processor of your batch system or system you are cross-compiling for; this will generate the file reconfigure-arch-linux2-c-debug.py 
        
        Run ./reconfigure-arch-linux2-c-debug.py (to complete the configure process).

   make PETSc
   
          qsub -I -l select=1:ncpus=8:mpiprocs=8 -l walltime=10:00:00 -q regular -A UHAR0005
          make PETSC_DIR=$PETSC_DIR PETSC_ARCH=$PETSC_ARCH all
          make PETSC_DIR=$PETSC_DIR PETSC_ARCH=$PETSC_ARCH check
         
###   ===============   Build PISM   ===============

```
   # Download  
   git clone git://github.com/pism/pism.git pism-stable
   mkdir ~/pism-stable/build
   cd ~/pism-stable/build
   
   7/3/2019
   Add "if (POLICY CMP0074)
          cmake_policy(SET CMP0074 NEW) # CMake 3.12
        endif ()"
   in CMakeList.txt  
   
   PISM_INSTALL_PREFIX=~/pism CC=mpicc CXX=mpicxx cmake .. -DPETSC_EXECUTABLE_RUNS=ON
   PISM_INSTALL_PREFIX=~/pism CC=mpiicc CXX=mpiicpc cmake .. -DPETSC_EXECUTABLE_RUNS=ON
   # May have some failed tests

Apr.29 
   # Turn on Proj4
   make edit_cache
   Turn on 'Pism_USE_PROJ4' Press "c" "c" "g"
   make

   make install -j 8
   
   do 
   make
   make install
   everytime changes something in the source code

 ```
 

