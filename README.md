# ERDDAP Playground #

This repository contains all files required to set up a simple ERDDAP service using docker based on [Axiom's docker-erddap image](https://hub.docker.com/r/axiom/docker-erddap). It includes a dummy dataset based on a NetCDF file, so users can take a look and replicate it. 

### Requirements ###

1. Install [Docker engine](https://docs.docker.com/engine/install/)
2. Install [Docker compose](https://docs.docker.com/compose/install/)

### Setup ###
1. clone this repository: ```$ git clone https://github.com/emso-eric/erddap-playground``` 
2. Enter the folder and run docker: ```$ cd erddap-playground```  
3. Start ERDDAP container: ```$ docker compose up https://github.com/emso-eric/erddap-playground```  

Voilà! ERDDAP should be up and running at [http://localhost:8080/erddap](http://localhost:8080/erddap)

## Project Organization ##

This project is organized as follows:

```bash
├── conf                 # Folder to store configuration files
│   ├── datasets.xml     # Datasets configuration and HTML customization
│   ├── setup.xml        # ERDDAP Server configuration
│   └── custom_logo.png  # example logo
|
├── datasets             # Folder where our datasets will be stored
│   ├── DummyData        # Example dataset path  
│       └── dummydata.nc # example NetCDF file with EMSO metadata
│   
│── erddapData           # ERDDAP internal stuff
│   ...
│   └── logs             # ERDDAP's logs, worth taking a look
|       └── log.txt      # ERDDAP's latest log
```

The ```conf``` folder contains the ``setup.xml`` and ``datasets.xml``configuration files. For further details consult the official [setup](https://coastwatch.pfeg.noaa.gov/erddap/download/setup.html) and [datasets.xml](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html) documentation.  

## Adding new datasets ##

To add anew dataset, create a new folder within ``datasets`` and drop your files there (there can be as many subdirectories as needed). Then, in your ```datasets.xml``` file you can copy&paste the dummy dataset and do the following changes:

1. change the ```datasetID``` attribute
```<fileDir>>/dataset/NewDataset</fileDir>```
2. change the ```<fileDir>``` to the path where your data is stored. Remember that the datasets folder is mounted at ```/datasets```  
3. Adapt the rest of the dataset of the metadata attributes.
4. Adapt the ```dataVariables``` as needed and select the proper [dataTypes](https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html#dataTypes) for every variable. ```<sourceName>``` is the name in the NetCDFs and ```<destinationName>``` is the name exposed by ERDDAP. Coordinates variables like TIME, LATITUDE, LONGITUDE and DEPTH variables should be left as in the example.

## Contact Info ##
**Author**: Enoc Martínez  
**Affiliation**: Universitat Politècnica de Catalunya   
**Contact**: enoc.martinez@upc.edu