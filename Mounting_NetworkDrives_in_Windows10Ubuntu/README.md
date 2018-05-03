Aims
====

Mount network drives in Windows 10 Ubuntu. The syntax is quite finnicky, and relies on slightly different methods from standard Linux

Command
=======

This is for mounting the Nobel server at KI.

    sudo mount -t drvfs '\\nobel.karolinska.se\imageanalysis' /mnt/nobel
    cd /mnt/nobel/kipet/atlas_images/human/vff/Granville

Notes for the mounting:

-   drvfs is the file system for the crossover between Windows 10 and Ubuntu
-   The Windows drive must have backslashes and be in quotation marks
-   The Linux drive must have forward slashes
