################## BASE IMAGE ######################

FROM jupyter/base-notebook:python-3.8.8

################## METADATA ######################

LABEL base_image="jupyter/base-notebook:python-3.8.8"
LABEL version="1"
LABEL about.maintainer=""
LABEL about.summary=""

################## SETUP ######################
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    && apt-get clean all && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    conda update conda -n base && \
    conda clean --all

#COPY environment.yml /home/jovyan/
#RUN conda env create -f enhancerscanner.yml

#COPY requirements.txt /home/jovyan/
#RUN pip install -r reuirements.txt && \
#    pip cache purge

RUN fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER jovyan
WORKDIR "${HOME}"

ADD analysis /home/jovyan/
ENV JUPYTER_ENABLE_LAB=1
EXPOSE 8888
CMD ["start-notebook.sh", "--ServerApp.root_dir=/analysis", "--ServerApp.token=''", "--ServerApp.password='sha1:b34f1c21e588:f9306c6a131f2fbac72014cae509b993c0da5df3'"]