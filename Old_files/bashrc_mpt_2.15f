# .bashrc
 alias ls='ls --color'
 alias ll='ls -all --color'
 
 module load intel/16.0.3
 module load mkl/11.3.3
 module load netcdf/4.5.0
 export LD_LIBRARY_PATH="/glade/u/apps/ch/opt/netcdf/4.5.0/intel/16.0.3/lib:$LD_LIBRARY_PATH"
 
 module load cmake/3.9.1
 
 
 export PETSC_DIR="/glade/u/home/jweiwen/wji_apps/petsc"
 #export PETSC_ARCH="arch-linux2-cxx-opt"
 export PETSC_ARCH="linux-intel-opt"
 export PATH="$PETSC_DIR/$PETSC_ARCH/bin:$PATH"
 export LD_LIBRARY_PATH="$PETSC_DIR/$PETSC_ARCH/lib:$LD_LIBRARY_PATH"
 
 module load udunits/2.2.20
 
 #UDUNITS
 export UDUNITS="/glade/u/apps/ch/opt/udunits/2.2.20/gnu/4.8.2"
 export PATH="$UDUNITS/bin:$PATH"
 export UDUNITS_INC="$UDUNITS/include"
 export LD_LIBRARY_PATH="$UDUNITS/lib:$LD_LIBRARY_PATH"
 
 # For the error of "ut_read_xml() failed" 
 export UDUNITS2_XML_PATH="$UDUNITS/share/udunits/udunits2.xml"
 
 #gsl
 module load gsl/2.4
 
 module load fftw3-mpi/3.3.6-pl2
 
 
 export PISM_DIR="/glade/u/home/jweiwen/pism"
 export PATH="$PISM_DIR/bin:$PATH"
 export LD_LIBRARY_PATH="$PISM_DIR/lib:$LD_LIBRARY_PATH"
 
 module load proj/4.9.3
 
 # NCO and Python Packages
 module load nco/4.7.4
 
 module load python/2.7.13
 module load numpy/1.13.3
 module load netcdf4-python/1.2.7
 module load scipy/0.19.1
 
 
 
 module load ncview/2.1.7
 
 module load ffmpeg/3.3.4
 
 module load ncl/6.4.0
 export NCARG_COLORMAPS=/glade/u/home/jweiwen/NCL_Colormaps:$NCARG_ROOT/lib/ncarg/colormaps
