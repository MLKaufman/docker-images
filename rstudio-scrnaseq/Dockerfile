FROM rocker/rstudio:4.1.0

LABEL image.authors=""

RUN apt-get clean all && \
	apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y \
		libhdf5-dev \
		libcurl4-gnutls-dev \
		libssl-dev \
		libxml2-dev \
		libpng-dev \
		libxt-dev \
		zlib1g-dev \
		libbz2-dev \
		liblzma-dev \
		libglpk40 \
		libgit2-28 \
	&& apt-get clean all && \
	apt-get purge && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN Rscript -e "install.packages(c('rmarkdown', 'tidyverse', 'workflowr', 'BiocManager', 'Seurat'));"
RUN Rscript -e "BiocManager::install(version = '3.13')"

#option to copy user settings from local rstudio into the container
#COPY user-settings /home/rstudio/.rstudio/monitored/user-settings/user-settings
#COPY .Rprofile /home/rstudio/