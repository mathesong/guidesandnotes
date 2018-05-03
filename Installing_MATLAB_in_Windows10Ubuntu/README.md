Aims
====

Install MATLAB in Windows 10 Ubuntu so that Linux-based software with MATLAB-based components can be run from Windows.

Installation
============

This was done before I started writing the guide. This part needs to be completed when I next do it.

Mounting the ISO
----------------

**To be completed...**

Installing from the ISO
-----------------------

**To be completed...**

MATLAB Setup
============

While MATLAB installs without issue in the Windows 10 Ubuntu environment, opening it is another story. It has issues with the BLAS libraries. I found a support page here: <https://se.mathworks.com/matlabcentral/answers/308911-can-i-install-matlab-in-bash-on-ubuntu-on-windows> , and the advice from the user recommending the stuff with execstack worked a charm.

First one needs to install execstack

    sudo apt-get install prelink

Then navigate to the MATLAB directory (/usr/local/MATLAB/R2014b/bin) and run the execstack commands:

    sudo execstack -c glnxa64/libmwblas.so
    sudo execstack -c glnxa64/libmwlapack.so
    sudo execstack -s glnxa64/MATLAB

And then MATLAB works!
