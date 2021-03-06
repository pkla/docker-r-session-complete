# docker-r-session-complete

Dockerfiles for R and Python sessions and jobs to be used RStudio Server Pro,
Launcher, and Kubernetes.

## How to Use These Docker Images

The Docker images built from these Dockerfiles are intended to be used for R and
Jupyter sessions and jobs with RStudio Server Pro (RSP), Launcher, and
Kubernetes.

Note: These Docker images are not equipped or intended to be used to run RStudio
Server Pro within a Docker container. Visit the
[rstudio/rstudio-docker-products](https://github.com/rstudio/rstudio-docker-products)
repository for images built for that purpose.

For more information about RStudio Server Pro and Launcher, refer to the
[Launcher Overview](https://solutions.rstudio.com/launcher/overview/) on the
RStudio Solutions website.

For more information about how to use these images with RStudio Server Pro and
Launcher, refer to the RStudio support article on [Using Docker images with
RStudio Server Pro, Launcher, and
Kubernetes](https://support.rstudio.com/hc/en-us/articles/360019253393-Using-Docker-images-with-RStudio-Server-Pro-Launcher-and-Kubernetes).

## Docker Images on Docker Hub

Built images are available from the
[rstudio/r-session-complete](https://hub.docker.com/r/rstudio/r-session-complete)
repository on Docker Hub.

## Docker Image Layers

These images include the following layers:

* Base OS
* RSP session components
* System packages required for R, R packages, and RStudio Professional Drivers
* One version of R
* R packages (devtools, tidyverse, shiny, and rmarkdown)
* One version of Python
* Jupyter Notebooks, JupyterLab, and RSP/RSC notebook extensions
* Python packages
* RStudio Professional Drivers

## Release Process for Docker Images

When builds on master are passing and you are ready to release a new version of
the image on Docker Hub, you can tag a release on master using the following
steps:

1. Update versions of RSP session components in Dockerfiles in a PR.
2. Update versions of R, Python, Pro Drivers, and other components as needed.
3. Merge PR when the build passes.
4. Run the following commands on the `master` branch, editing the version string
   as needed (where `1.3.XXXX-X` is the RSP version):

   ```
   export VERSION=1.3.XXXX-X
   git commit -am "Release for image version ${VERSION}" --allow-empty
   git tag -a ${VERSION} -m "${VERSION}"
   git push origin ${VERSION}
   git push
   ```

   Note: Add the `-preview` suffix to the version string for tagged images that
   correspond to preview release versions of RSP. Images related to preview
   builds are intended for testing purposes, subject to being removed, do not
   fall under our support agreement, and are not recommended for use in
   production.

5. The new images will get built on Travis CI and get pushed to the
   [rstudio/r-session-complete](https://hub.docker.com/r/rstudio/r-session-complete)
   repository on Docker Hub.
