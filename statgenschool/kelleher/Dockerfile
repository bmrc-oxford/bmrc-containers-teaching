FROM jupyter/r-notebook:2022-06-13
LABEL app="Python"
LABEL description="Statistical Genomics Summer School Thursday image"
LABEL maintainer="Adam Huffman"
LABEL version="0.8"

# Set user and working directory
USER root
WORKDIR /tmp


# Replace `latest` with an image tag from to ensure reproducible builds:
# https://hub.docker.com/r/jupyter/minimal-notebook/tags/
# Inspect the Dockerfile at:
# https://github.com/jupyter/docker-stacks/tree/HEAD/minimal-notebook/Dockerfile


RUN apt-get update && apt-get -yqq install \
        libgsl0-dev libatlas-base-dev make g++ zlib1g-dev cmake git file

# install additional package...

RUN pip install --no-cache-dir \
demes==0.2.3 \
demesdraw==0.4.0 \
jupyterquiz==2.6.2 \
matplotlib==3.5.2 \
msprime==1.2.0 \
nbgitpuller==1.1.0 \
numpy==1.24.3 \
pandas==2.0.1 \
rpy2==3.5.12 \
scipy==1.10.1 \
seaborn==0.12.2 \
tqdm==4.65.0 \
tsdate==0.1.5 \
tsinfer==0.3.1 \
tskit==0.5.5 \
tszip==0.2.2

# Relate

RUN cd /usr/local/src && \
    git clone https://github.com/MyersGroup/relate.git && \
    cd relate && cd build && cmake .. && make
# Install R package pammtools
RUN Rscript -e 'install.packages("pammtools", repos="https://www.stats.bris.ac.uk/R")' && \
    Rscript -e 'install.packages("geodist", repos="https://www.stats.bris.ac.uk/R")' && \
    Rscript -e 'install.packages("cowplot", repos="https://www.stats.bris.ac.uk/R")'

# Install R package relater
RUN Rscript -e 'remotes::install_github("leospeidel/relater")'

# set the default command of the image,
# if the parent image will not launch a jupyterhub singleuser server.
# The JupyterHub "Docker stacks" do not need to be overridden.
# Set either here or in `singleuser.cmd` in your values.yaml
# CMD ["jupyterhub-singleuser"]

# Set user, home and working directory
USER jovyan
ENV HOME /home/jovyan
WORKDIR /home/jovyan

