# Aims

This is my guide for how to start up rstudio within a docker container
locally.

# Download the docker image

    docker pull mathesong/tidyverse-torsten

# Run the docker image

    docker run -e PASSWORD=12345 --name rstudio -p 8787:8787 -v C:/Users/mathe/Repositories/Multilevel_TCM:/home/rstudio/Multilevel_TCM mathesong/tidyverse-torsten

Also, maybe, if needing to download stuff in the console, might need the
following

    docker run -d -p 8787:8787 -e ROOT=TRUE mathesong/tidyverse-torsten

And then stuff can be downloaded using

    system("sudo apt-get install -y libgsl0-dev")

# Open up the Rstudio session

Open a browser, and enter the following:

    http://localhost:8787/

… and then enter the username `rstudio` and the password you wrote
above.

# Close the Rstudio image

Find the name of the container - it should be rstudio if you set its
name to be that.

    docker container ls

Then kill it

    docker kill rstudio
