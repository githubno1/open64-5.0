# Building the compiler
If you choose to build the compiler suite from the source tar ball,  follow the steps outlined below.

Prerequisites

 

In order to compile Open64 successfully, you should meet the following requirements:

1. Linux based OS
Currently, Open64 is intensively tested on Linux on IA64/X86_64/IA32.

2. IA32/x86_64/IA64 based machine
In this release, Open64 is supported and tested for the Itanium 2 and IA32/x86_64 architectures. Itanium 1 and generic IA32 is also supported, but not tested carefully.

3. GNU Make
You should use a up to date version of Make. The system default versions on most recently Linux distributions have been tested and work with our Makefile.

4. GCC (GNU Compiler Collection)
In order to compile the Open64 source code, you need GCC 4.0.x - 4.4.x. Support for GCC 2.x has been dropped since release 1.0. If you don't have any of the suggested GCC versions above, we recommend that you to install GCC 4.3.x.


Obtain the source code

 

To compile Open64 you need to obtain the source code first. There are two ways:

1. Obtain the Source Code as Archive
You can download the source code from Sourceforge.net and extract the source code and the prebuild binaries/libraries

    tar xjvf open64-<version>-<release>.src.tar.bz2

 

The whole source hierarchy will be in directory rooted at open64-<version>.

2. Obtain the Source Code from our Subversion Repository
You can also obtain the latest version of our source code from the sub-version repository. To get the latest version issue the following command:

    svn export https://svn.open64.net/svnroot/open64/branches/open64-<version> open64-<version>


This will copy the open64 <version> source code to the directory open64.

 

Configure and make

 

The open64 build process has been changed to use the autoconf tool that many other opensource products use.  In the old build process, it was necessary to set variables on the make command to control the build; MACHINE_TYPE, BUILD_OPTIMIZE, and TOOLROOT arguments were passed to the make command to control what type of open64 compiler to build.

In the new build process, these arguments are passed to the configure script (using a different syntax) and then the 'make all' and 'make install' commands are run without any arguments.


Here is a mapping for some of the old make options to configure options:

       

Makefile setting
	

configure option

MACHINE_TYPE=i386
	

--target=i386-unknown-linux-gnu(**)

MACHINE_TYPE=ia64
	

--target=ia64-unknown-linux-gnu

BUILD_OPTIMIZE=DEBUG     
	

--with-build-optimize=DEBUG

BUILD_COMPILER=GNU
	

--with-build-compiler=GNU

TOOLROOT=/opt/open64
	

--prefix=/opt/open64



  (**) If you are building on an 386/x86_64 system, the target will default to building a 32 bit compiler with 32 and 64 bit libraries and you do not have to use this option.

Other differences between the old and new build are that 'make' or 'make all' now builds both the compiler and the libraries.  It is no longer neccessary to run 'make all' to build the compiler and then 'make lib' to build the libraries.

Additionally, the libraries that need to be compiled with the open64 compiler will be built using the compiler that was just created during the make process.  A seperate open64 compiler is not needed to build these libraries.

To build open64 create a directory (obj) somewhere not underneath the open64 directory containing the source files.  Switch to that directory and execute the commands:

    <path-to-open64-dir>/open64-<version>/configure
    make all

 

If you want to build a debuggable compiler you can add the "--with-build-optimize=debug" argument to the configure command.

If you know where you want to install the compiler you build, add "--prefix=<path>" to the configure command and after running make to build the compiler you can run "make install" to install the compiler in the path specified by the --prefix argument.  The default prefix is /usr/local.

1. Building the compiler on x86_64
By default, on x86_64 machines, the compiler will be built in 32 bit mode and libraries will be built in 32 and 64 bit modes to support compilation in either mode.  You can build 64 bit executables by specifying "--build=x86_64-unknown-linux-gnu" on the configure command.

2. some tips on Ubuntu machines
If you are building the compiler on Ubuntu machine, you need to install the following tools first:

    awk, csh, bash, gmake, flex and bison,

On some Ubuntu distributions, you need to change the symbol link '/bin/sh' to '/bin/bash' to make the scripts work.


If you met the following error:
  ##./table INTERNAL ERROR: Unexpected line: Abort
  ##sh: line 1: 27052 Segmentation fault      ./table <OPTIONS.P
you need to make sure the awk is linked to mawk on your ubuntu machine

3. libraries
Libraries used to be built seperately from the compiler, but now the libraries as well as the compiler are built as part of the default make target.  The libraries are built using the newly built compiler 

 

Environment variables

 

Open64 used to use the environment variable TOOLROOT to specify the installation location and to help the compiler find libraries and binaries.  TOOLROOT should no longer be used and the installation location should be specified via the --prefix argument to configure.

Warning!!!
If you have TOOLROOT set it could still affect where open64 looks for libraries and executables.

 

Installation

 

Once you have done "make all" to make the compiler, "make install" will copy it to the location specified by the --prefix argument to configure. If --prefix was not used the default install location is in /usr/local.

 

Other targets

 

People interested in building the compiler for other ports than IA-32/x86_64/IA-64 should contact the vendors listed below directly:

CUDA
	

NVIDIA Inc.

LOONGSON     
	

Institute of Computing Technology at the Chinese Academy of Sciences

MIPS
	

Institute of Computing Technology at the Chinese Academy of Sciences

PowerPC
	

Tsinghua University

SL
	

SimpLight Nanoelectronics Inc.
