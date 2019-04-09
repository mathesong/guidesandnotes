Aims
====

This is my guide for how to get set up with DigitalOcean cloud
computing.

Starting up a docklet
=====================

``` r
docklet_create(region="nyc1", image="docker-18-04")

d <- droplets()[[1]]

docklet_rstudio(d, user="username", password="password", 
                verbose=TRUE, img="rocker/tidyverse")
```

Exchanging files
================

Checking what’s on the computer
-------------------------------

``` r
d %>% droplet_ssh("ls")
```

Uploading files
---------------

Files are uploaded to the computer, and not into the docker container
directly.

``` r
tmp <- tempfile()
saveRDS(mtcars, tmp)
d %>% droplet_upload(tmp, ".")
```

Downloading files
-----------------

Files must first be extracted from the docker container, and then can be
downloaded. First we need to find the name of the docker container.

``` r
d %>% droplet_ssh("docker container ls")
```

The last item on that list is the name

Next we remove files from the docker container

``` r
d %>% droplet_ssh("docker cp vigilant_driscoll:/home/test/test123.csv /root/test123.csv")
```

And then we can download the file

``` r
droplet_download(d, "/root/test123.csv", local = "C:/Users/mathe/Dropbox")
```
