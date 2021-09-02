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
    apt-get clean all && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    conda update conda -n base && \
    conda clean --all && \
    # fix conda related permissions while running root
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"
# two options for settings up additional environments/packages at build time.
#COPY environment.yml /home/jovyan/
#RUN conda env create -f enhancerscanner.yml
#COPY requirements.txt /home/jovyan/
#RUN pip install -r reuirements.txt && \
#    pip cache purge

USER jovyan
WORKDIR "${HOME}"

# add a folder
#ADD analysis /home/jovyan/

ENV JUPYTER_ENABLE_LAB=1
EXPOSE 8888

# password = scrnaseq
CMD ["start-notebook.sh", "--ServerApp.root_dir=/home/jovyan/", "--ServerApp.token=''", "--ServerApp.password='sha1:a4a5da289ac7:74fa573adba6a53e954e66ec23332ec0ec479322'"]