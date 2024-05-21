# AlmaLinux-9

##Test the AlmaLinux-9 code##

I downloaded the software AlmaLinux-9 on the laptop and tested the code for
the Siesta-4.1b code.
As the successor of CentOS 7, the installation was all right with 10 GB of
AlmaLinux-9.4-x86_64-dvd.iso, that was finished in 15 minutes for reboot.

At the beginning, I opened the gfotran by # gfortran -V, which was all right.
I also did # pip -V.

Then, I downloaded the Siesta-4.1b and did % tar -zxvf siesta-4.1b.tar.gz.
Before the Siesta code, it was necessary to install OpenBLAS and Scalapack.
For OpenBLAS, it was straight forward after a while.
For Scalapack, however, my installation went wrong as # make -i,
since the AlmaLinux-9 showed unnecessary errors without success.
So, for the being, the import of ./lib/libscalapack.a was made from 
the CentOS 7 code.

The arch.make file is the following:  
  .SUFFIXES:  
  .SUFFIXES: .f .F .o .c .a .f90 .F90  
  SIESTA_ARCH = gfortran-MPI  

  CC = mpicc  
  FPP = $(FC) -E -P -x c
  FC = mpifort  

  MPI_INTERFACE = libmpi_f90.a  
  MPI_INCLUDE = .   

  FFLAGS = -O2 -fPIC -ftree-vectorize -march=native -fallow-argument-mismatch  
 #FFLAGS = -O2 -fexpensive-optimizations -ftree-vectorize -fprefetch-loop-arrays -march=native -fPIC -fopenmp  
  FC_SERIAL = gfortran  

  AR = ar  
  RANLIB = ranlib  
  SYS = nag  

  SP_KIND = 4  
  DP_KIND = 8  
  KINDS =  $(SP_KIND) $(DP_KIND)   
  
  FPPFLAGS = -DMPI   
  LDFLAGS  =  
  INCFLAGS =  
  INSDIR = /opt  
  COMP_LIBS =     # libsiestaLAPACK.a libsiestaBLAS.a  
  LDFLAGS += -L$(INSDIR)/openblas/lib -Wl,-rpath=$(INSDIR)/openblas/lib  
  LIBS = -lgomp -L/opt/openblas/lib -lopenblas  
  LIBS += -L/opt/scalapack/lib -lscalapack  





