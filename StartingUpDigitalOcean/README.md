# Aims

This is my guide for how to get set up with DigitalOcean cloud
computing.

# Setting up SSH

Follow instructions over
[here](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

# Starting up a docklet

Packages

``` r
# devtools::install_github("sckott/analogsea")
library(analogsea)
```

And the docklet. Remove the size argument for a cheaper (\~5 times) but
less powerful machine.

``` r
d <- docklet_create(region="ams3", image="docker-18-04", size="s-4vcpu-8gb",
                    name = "My_Lovely_Droplet")

Sys.sleep(5)
d <- as.droplet(d$name)

docklet_rstudio(d, user="username", password="password", 
                verbose=TRUE, img="rocker/tidyverse", 
                keyfile = "C;/Users/mathe/.ssh/id_rsa")
```

# Exchanging files

## Checking what’s on the computer

``` r
d %>% droplet_ssh("ls")
```

## Uploading files

Files are uploaded to the computer, and not into the docker container
directly.

``` r
tmp <- tempfile()
saveRDS(mtcars, tmp)
d %>% droplet_upload(tmp, ".")
```

## Downloading files

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

## Spaces

I think the way that uploading and downloading is supposed to work is
actually to use spaces, using the following commands:

``` r
space_object_get()
space_object_put()
```
