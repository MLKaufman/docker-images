# docker-images


Collection of docker images I am currently working on and tweaking.  
<HR>  

## Purpose  
Mostly as examples and templates for creating images for performing datascience, bioinformatics, and in particular single cell RNA-sequencing.  

<HR>

## Usage  
Clone the repository.  
Navigate to the folder that contains the image you wish to build.  
Either build the image using the ```Dockerfile``` or build/run using the ```dockercompose.yml``` file with preconfigured run settings.
```
docker build . -t <tag_name>
docker run <tag_name>
```
or  
```
docker compose up
```
<HR>

## Image Recipes  
### <b> jupyter-base </b>  
Basic image that sets up a running Jupyter lab server instance.
* Python
* Jupyterlab

### <b> jupyter-scrnaseq </b>  
Work in progress. Intended to be a complete package for scRNAseq analysis in the jupyter environment.  
* Python/R
* Jupyterlab
* scanpy
* seurat
* rnavelocity/slingshot/tradeseq?

### <b> rstudio-base </b>  
Basic image that runs a rstudio server that can be accessed in the browser. Based off of the Rocker images.  
* R
* Rstudio-server

### <b> rstudio-scrnaseq </b>  
Work in progress. Intended to be a complete package for scRNAseq analysis in the rstudio environment.  
* Python/R
* Rstudio-server
* scanpy
* seurat
* rnavelocity/slingshot/tradeseq?