################## BASE IMAGE ######################

FROM jupyter/base-notebook:python-3.8.8

################## METADATA ######################

LABEL base_image="jupyter/base-notebook:python-3.8.8"
LABEL version="1"
LABEL about.maintainer=""
LABEL about.summary=""

################## SETUP ######################
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root
RUN apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get clean all && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    conda update -n base conda && \
    conda install -c conda-forge -c bioconda fa2 ipykernel c-compiler && \
    conda install R && \
    pip --no-cache-dir install scanpy psutil leidenalg && \
    conda clean --all

RUN Rscript -e "install.packages(repos = 'http://cran.us.r-project.org', c('rmarkdown', 'tidyverse', 'BiocManager', 'Seurat'), clean = TRUE, quiet = TRUE);" && \
    Rscript -e "install.packages(repos = 'http://cran.us.r-project.org', c('IRkernel'), clean = TRUE, quiet = TRUE);" && \
    Rscript -e "BiocManager::install(version = '3.13')" && \
    Rscript -e "IRkernel::installspec(name = 'rkernel', displayname = 'R Kernel')" && \
    # jupyter labextension install @techrah/text-shortcuts && \
    # fix conda related permissions while running root
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# two options for settings up additional environments/packages at build time.
#COPY environment.yml /home/jovyan/
#RUN conda env create -f environment.yml
#or
#COPY requirements.txt /home/jovyan/
#RUN pip install -r reuirements.txt && \
#    pip cache purge

USER jovyan
WORKDIR "${HOME}"

# add a folder
#ADD analysis /home/jovyan/

ENV JUPYTER_ENABLE_LAB=1
EXPOSE 8888

# comment for standalone image execution and not running with docker-compose
# password = scrnaseq
CMD ["start-notebook.sh", "--ServerApp.root_dir=/home/jovyan/analysis/", "--ServerApp.token=''", "--ServerApp.password='sha1:a4a5da289ac7:74fa573adba6a53e954e66ec23332ec0ec479322'"]
#ENTRYPOINT?