---
layout: page
title: Projects
---

# Human Density Prediction
This project aims at predicting human density combining Landsat-8 satellite images and Machine Learning.
## Landsat-8 satellites images
Images are taken directly from [U.S. Geological Survey website](http://earthexplorer.usgs.gov/).
One can query images with criteria like :
* cloud covering
* date range
* day or night

Here after, a screenshot of France query

![France Landsat-8 query](/assets/images/human_density_prediction/france-selection.png){:class="img-responsive"}

and the 70 resulting datasets (thumbnails) projected, queried with minimum possible cloud covering (<20%), day acquisition and between May and September 2013.

![France Landsat-8 datasets](/assets/images/human_density_prediction/covering-selection.png){:class="img-responsive"}

## Vegetal indice extraction

Each dataset is composed of 11 bands (1 pixel = 30x30 meters). 
*NDVI* (*Normalized Difference Vegetal Indice*) is a combination of band 4 (red) and band 5 (red-edge) that make vegetation in evidence according to (values span from -1 and 1) :

* *NDVI* < 0 : water, snow, ice, cloud
* *NDVI* = 0 : ground without vegetation
* *NDVI* > 0 : ground with vegetation

We then expect high values (rich vegetation) to explain low density areas, while low values (poor vegetation) should explain high densities. Below, RGB and *NDVI* images for different densities:

#### Paris - 21153 habs/km²
![Paris - RGB](/assets/images/human_density_prediction/07_rgb_Paris.png){:height="240px" width="240px"}{:class="img-responsive"}
![Paris - NDVI](/assets/images/human_density_prediction/07_ndvi_Paris_colormap.png){:height="250px" width="310px"}{:class="img-responsive"}

#### Lyon - 10117 habs/km²
![Lyon - RGB](/assets/images/human_density_prediction/07_rgb_Lyon.png){:height="240px" width="240px"}{:class="img-responsive"}
![Lyon - NDVI](/assets/images/human_density_prediction/07_ndvi_Lyon_colormap.png){:height="250px" width="310px"}{:class="img-responsive"}

#### Amiens - 2698 habs/km²
![Amiens - RGB](/assets/images/human_density_prediction/07_rgb_Amiens.png){:height="240px" width="240px"}{:class="img-responsive"}
![Amiens - NDVI](/assets/images/human_density_prediction/07_ndvi_Amiens_colormap.png){:height="250px" width="310px"}{:class="img-responsive"}

#### Abbeville- 914 habs/km²
![Abbeville - RGB](/assets/images/human_density_prediction/07_rgb_Abbeville.png){:height="240px" width="240px"}{:class="img-responsive"}
![Abbeville - NDVI](/assets/images/human_density_prediction/07_ndvi_Abbeville_colormap.png){:height="250px" width="310px"}{:class="img-responsive"}

Histogram of *NDVI* (1024 bins) is then finally taken as city descriptor. Superposition of various histograms shows clearly a relation between
*NDVI* behavior and density :

![NDVI histograms](/assets/images/human_density_prediction/ndvi_categorie.png){:class="img-responsive"}

## Importing Labels

Precise densities can be taken from French official institute census ([INSEE](http://www.insee.fr/fr/ppp/bases-de-donnees/recensement/populations-legales/pages2015/zip/HIST_POP_COM_RP13.zip)). This census is from 2013, which perfectly matches our Landsat-8 datasets. 
We categorize densities in order to deal with a classification problems (6 categories)

- category 1 : density between 0 and 500 habs/km²
- category 2 : density between 500 and 2000 habs/km²
- category 3 : density between 2000 and 5000 habs/km²
- category 4 : density between 5000 and 10000 habs/km²
- category 5 : density between 10000 and 13000 habs/km²
- category 6 : density greater than 13000 habs/km²

## Machine Learning

We can now go through supervised learning. 
France data has been used for training/validation.
Belgium, Netherlands and Switzerland have been used for testing model generalization.

### Neural Network - Training/Validation - France

#### ground truth
![NN - France - gt](/assets/images/human_density_prediction/France/nn/density_ground_truth.png){:class="img-responsive"}
#### prediction
![NN - France - pred](/assets/images/human_density_prediction/France/nn/density_classification.png){:class="img-responsive"}

### Neural Network - Testing - Belgium

#### ground truth
![NN - Belgium - gt](/assets/images/human_density_prediction/Belgique/nn/density_ground_truth.png){:class="img-responsive"}
#### prediction
![NN - Belgium - pred](/assets/images/human_density_prediction/Belgique/nn/density_classification.png){:class="img-responsive"}

### Neural Network - Testing The Netherlands

#### ground truth
![NN - The Netherlands - gt](/assets/images/human_density_prediction/Pays-Bas/nn/density_ground_truth.png){:class="img-responsive"}
#### prediction
![NN - The Netherlands - pred](/assets/images/human_density_prediction/Pays-Bas/nn/density_classification.png){:class="img-responsive"}

### Neural Network - Testing Switzerland

#### ground truth
![NN - Switzerland - gt](/assets/images/human_density_prediction/Suisse/nn/density_ground_truth.png){:class="img-responsive"}
#### prediction
![NN - Switzerland - pred](/assets/images/human_density_prediction/Suisse/nn/density_classification.png){:class="img-responsive"}



