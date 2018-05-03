Aims
====

This notebook will go through the process of setting up gradient nonlinearity correction. This is useful for the PET Group because the MR images which come from MR Odenplan are not corrected for nonlinearities.

Preparation of Linux environment
================================

The nonlinearity correction requires FreeSurfer as well as MATLAB. This was performed within the Ubuntu within Windows 10 extension.

Gradient Nonlin Correction scripts
----------------------------------

I unzipped the folder of scripts into /usr/local/freesurfer/gradient\_nonlin\_unwarp. The scripts can be found here \[LINK TO BE UPDATED IF/WHEN I GET PERMISSION\].

MATLAB Preparation
------------------

MATLAB requires a little bit of extra love and attention within the Windows 10 Ubuntu module. Follow the other guide to install it.

Gradient Correction scripts
===========================

I unzipped the folder of scripts into /usr/local/freesurfer/gradient\_nonlin\_unwarp. The scripts can be found here \[LINK TO BE UPDATED IF/WHEN I GET PERMISSION\].

chmodding
---------

I then made the correction scripts executable

    export PATH=$PATH:/usr/local/freesurfer/gradient_nonlin_unwarp
    source ~/.profile

    sudo chmod +x gradient_nonlin_unwarp.sh

    cd ..
    gradient_nonlin_unwarp.sh

Moving stuff around to get everything to work
=============================================

Things need to be in specific places for stuff to work, and this is the most critical piece of information for this guide.

Gradient Correction m files
---------------------------

The m files from the downloaded folder need to be moved into /usr/local/freesurfer/dev/matlab . This requires sudo permissions.

Gradient Coefficient files
--------------------------

The coeff file apparently contains proprietary information. I was sent the coeff file for the Siemens Avanto system. I do not know if I am allowed to share this file outside of our group without consent from the physicist at Siemens, but contact me if you would like it, and I can speak to them.

The .coeff file needs to be moved into /usr/local/freesurfer/dev/matlab/gradient\_coil\_files . Also, it needs a special name: coeff\_{systemname}.grad. When specifying the coilname later, this should be specified as the full name, and the gradient correction MATLAB script will use regex to pull out the system name (and requires it be of this form to do that).

Use
===

Terminal
--------

The use of the script is as follows:

    gradient_nonlin_unwarp.sh 001_ND.nii 001_GD.nii coeff_avanto.grad --nobiascor --shiftmap

R wrapper
---------

I have written a wrapper around this, which is kept in the R package [kipettools](https://github.com/mathesong/kipettools). This can be run on a BIDS dataset to make all the necessary corrections prior to its release. This can be run with the following command:

``` r
kipettools::gradnonlincorr("sub-01_T1w", coeff_file='coeff_avanto.grad', outpath_checks = 'checkFile_folder')
```
