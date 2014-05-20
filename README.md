LAMMPS-NETCDF
=============

The files in this directory are a user-contributed package for LAMMPS.

The person who created these files is Lars Pastewka at
Fraunhofer IWM (lars.pastewka@iwm.fraunhofer.de).
Contact him directly if you have questions.

Lars Pastewka
Fraunhofer-Institut f�r Werkstoffmechanik IWM
W�hlerstra�e 11, 79108 Freiburg
e-mail: lars.pastewka@iwm.fraunhofer.de

PACKAGE DESCRIPTION:
--------------------

This is a LAMMPS (http://lammps.sandia.gov/) dump style for output into a NetCDF
database. The database format follows the AMBER NetCDF trajectory convention
(http://ambermd.org/netcdf/nctraj.html), but includes extensions to this
convention.

NetCDF files can be directly visualized with the following tools:
* Ovito (http://www.ovito.org/)
* VMD (http://www.ks.uiuc.edu/Research/vmd/)
* AtomEye (using a patched version from http://www.libatoms.org/)

Syntax:

> dump ID group-ID nc N file args
> dump_modify ID keyword values

with

args = list of atom attributes  
keyword = append or double or global
* append yes: append output to existing NetCDF file
* append yes at frame: append out to existing NetCDF file and start writing to
    frame given; if negative frame is counted from the end of file.
* double yes|no: output data as double instead of float
* global = list of global (not per atom, but per frame) quantities
    can be variables, compute or fix data prefixed with v_, c_ and f_,
    respectively.

The list of atom attributes is identical to the 'custom' dump style.

Example:

> dump 1 all nc 100 traj.nc type x y z vx vy vz
> dump_modify 1 append yes at -1 global c_thermo_pe c_thermo_temp c_thermo_press

INSTALLATION:
-------------

In your LAMMPS src directory type:

> git clone https://github.com/pastewka/lammps-netcdf.git USER-DUMP-NC
> make yes-user-dump-nc

Note that LAMMPS will need to be linked to NetCDF. This will require a
modification of your favorite makefile. Please add

> EXTRA_INC += `nc-config --cflags`
> EXTRA_LIB += `nc-config --libs`

to the respective EXTRA_INC, EXTRA_LIB section of the makefile.

Other notes:
------------

This is package is known to work with LAMMPS 13May14.