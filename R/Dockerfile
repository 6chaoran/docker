FROM r-base

RUN apt-get update && \
    apt-get install -y cmake build-essential gcc g++ git wget \
    #lightgbm
    libxml2-dev libssl-dev libgit2-dev libcurl4-openssl-dev \
    #RPostgreSQL
    libpq-dev  

RUN Rscript -e "install.packages(c('testthat','roxygen2','devtools','data.table','dplyr','RPostgreSQL'))"

RUN git clone https://github.com/Microsoft/LightGBM && \
    cd LightGBM && \
    Rscript build_r.R && \
    # clean
    apt-get autoremove -y && apt-get clean && \
    rm -rf /usr/local/src/*

COPY . /usr/local/src/myscripts/
WORKDIR /usr/local/src/myscripts/

RUN Rscript -e "pkgs <- readLines('requirement.txt'); for(p in pkgs){if(! require(p,character.only = T)) install.packages(p)}"
