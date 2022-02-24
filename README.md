# Project Title: ocean_color


Name(s) of team member 1: Bao Nguyen Quoc

Name(s) of team member 1: Manjaree Binjolkar


## Summary: 
Using ocean surface color data to identify the area that algae tends to grow.
We would like to look into the area on the ocean surface that has a good condition for algae to grow. Algae requires nutrients such as nitrogen, phosphorus, trace elements, and warm temperature to thrive. By using the Landsat data, we can track chlorophyll A, an indicator for algae growth. From this project, we hope to identify the good location in the ocean that has nutrient and good temperature where we can grow kelp for carbon capture. 


## Some introductory background information: 
Carbon dioxide emission is one of the main reason that cause climate change. Capturing carbon dioxide by kelp is becoming one of the method to lower greenhouse gas and fight climate change. Ocean surface is vast and unexploited for carbon capture purpose. We would like to identify which part of the ocean is suitable for biological growth and thus can allow us to grow kelp. For this purpose, algae could be used as a good indicator because the growth condition of algae is similar to kelp. Algae likes to growth at the high temperature with high nitrate concentration. Therefore, we will use the data set from Argo for nitrate, NOAA for temperature and chlorophyll. We aim to plot the changes of these variable over the seasons and investigate the correlation between these variable.

## Problem statement, question(s) and/or objective(s): 
Which variable is more important to algae growth (temperature or nutrient)? What is the limitation factor for algae growth? What is the distribution of nutrient and temperature across the ocean and how it corresponds to algae?

## Datasets you will use:
Temperature: https://developers.google.com/earth-engine/datasets/catalog/NOAA_CDR_OISST_V2_1 

Ocean color: https://developers.google.com/earth-engine/datasets/catalog/JAXA_GCOM-C_L3_OCEAN_CHLA_V2?hl=en

Biological Argo: https://biogeochemical-argo.org/data-access.php

## Tools/packages you’ll use (with links): 
Rasterio: https://rasterio.readthedocs.io/en/latest/

Xarray: https://docs.xarray.dev/en/stable/

Scipy: https://scipy-cookbook.readthedocs.io

Pandas: https://pandas.pydata.org

Numpy: https://numpy.org

## Planned methodology/approach: 
Our approach is to find any visible changes (raster images - Rasterio, Xarray) over the years for alage growth, temperature and nutrients and use regression analysis (Numpy, Scipy, Pandas) to find out the most important factor, maybe try to predict the changes for this year. Initially we will zoom in the coast of Washington state, run our code and then expand to the whole world.

## Expected outcomes: 
Generate the time series for temperature and nutrients that correspond to the growth of algae (chlorophyll variable). Find the most important factor affecting algae growth using regression analysis.

## Any other relevant information, images/tables, references, etc.

## References
