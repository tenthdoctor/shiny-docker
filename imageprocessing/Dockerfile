FROM openanalytics/r-base

MAINTAINER Tobias Verbeke "tobias.verbeke@openanalytics.eu"

# system libraries of general use
RUN apt-get update && apt-get install -y \
    sudo \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev \
    libxt-dev \
    libssl-dev \
    libssh2-1-dev \
    libssl1.0.0

# system library dependency for the euler app
RUN apt-get update && apt-get install -y \
    libmpfr-dev

# basic shiny functionality
RUN R -e "install.packages(c('shiny', 'rmarkdown'), repos='https://cloud.r-project.org/')"

# install dependencies of the euler app
RUN apt-get install -y libtiff-dev fftw-dev libjpeg-dev
RUN R -e "install.packages('Rmpfr', repos='https://cloud.r-project.org/')"

RUN apt-get install -y libfftw3-3 libfftw3-dev libtiff5-dev
RUN R -e "install.packages(c('tiff','fftwtools'), repos='https://cloud.r-project.org/')"
RUN R -e "install.packages(\"BiocManager\")"
RUN R -e "BiocManager::install(\"EBImage\")"

# copy the app to the image
RUN mkdir /root/euler
RUN echo "copying code"
COPY euler /root/euler

COPY Rprofile.site /usr/lib/R/etc/

EXPOSE 3838

CMD ["R", "-e", "shiny::runApp('/root/euler')"]
