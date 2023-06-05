# Predicting Povery Using Satellite Imagery
Using satellite imagery and pre-trained computer vision models to predict poverty on Bangladesh, based on the 2016 paper "Combining satellite imagery and machine learning to predict poverty". This project uses 5 different pre-trained computer vision models to extract features from satellite images, then uses these features to predict poverty.

Data:

The data used for this project include the ground truth poverty data for clusters of houses in Bangladesh. These clusters are from the DHS website that surveys poverty data in various countries. The poverty data and coordinates of these clusters can all be found on the DHS website. 

The satellite images for fine-tuning the computer vision models are from the Google Static Maps API. The training satellite image data is only on Bangladesh, but the testing data is from major cities across the entire indian subcontinent. To download coordinates of major cities in the Indian subcontinent use the website simplemaps.com to download them in CSV format.  

To download a map for the nightlight data, use the VNL_v2_npp_2021_global_vcmslcfg_c202203152300.average file from https://eogdata.mines.edu/products/vnl/.

There are a total of 5 jupyter notebooks.

Processing_survey_data:

    The purpose of this notebook is to process the DHS poverty data and cluster coordinate data into CSV files that will be used for training different
    models. The clusters are the points where I have known poverty data. 

Processing_Images:

    This notebook is to process all the nightlight data and to download all the images, to put all the images into the correct folders and create the
    annotations files that will be used to to create the dataloader used to train the CNN models. To download the images you require an API key and
    to process the images you require GDAL and rasterio, which are notoriously difficult libraries to install. 

Model:

    The model notebook is used to train all the models on the necessary data. I create a custom dataset and dataloader using the annotations file
    from the previous notebook and train 5 different models. The weights for each model are later saved and can be loaded for the next notebook.

Feature_Extraction:

    This notebook is to extract the features from the satellite images that will be used to train the linear model. It creates aggregated image features 
    per cluster and saves them into a directory. There is a directory for each model as I use 3 different models, and within each directory there is a 
    directory for each cluster.

Linear_model:

    The linear model notebook trains a ridge regression model on first raw nightlight data and then on the aggregated features. The linear model is the
    predictor of poverty and predicts the poverty for a given cluster based on either how much nightlight there is (the baseline) or the aggregated image
    features for that cluster. 


