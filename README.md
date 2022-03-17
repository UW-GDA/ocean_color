# Project Title: ocean_color


Name(s) of team member 1: Bao Nguyen Quoc

Name(s) of team member 1: Manjaree Binjolkar


## Summary: 
Using ocean surface color data to identify the area that algae tends to grow.
We would like to look into the area on the ocean surface that has a good condition for algae to grow. Algae requires nutrients such as nitrogen, phosphorus, trace elements, and warm temperature to thrive. By using the Landsat data, we can track chlorophyll A, an indicator for algae growth. From this project, we hope to identify the good location in the ocean that has nutrient and good temperature where we can grow kelp for carbon capture. 


## Some introductory background information: 
Carbon dioxide emission is one of the main reason that cause climate change. Capturing carbon dioxide by kelp is becoming one of the method to lower greenhouse gas and fight climate change. Ocean surface is vast and unexploited for carbon capture purpose. We would like to identify which part of the ocean is suitable for biological growth and thus can allow us to grow kelp. For this purpose, algae could be used as a good indicator because the growth condition of algae is similar to kelp. Algae likes to growth at the high temperature with high nitrate concentration (most important nutrient). The basic principle behind the remote sensing of ocean color from space is this: the more phytoplankton in the water, the greener it is.  In looking at the large-scale distributions of algae in the ocean, we can see how closely they are related to areas where nutrients are being supplied to the surface waters. Therefore, we will use the data set from Argo for nitrate, NOAA for temperature and chlorophyll. We aim to plot the changes of these variable over the seasons and investigate the correlation between these variable.

## Problem statement, question(s) and/or objective(s): 
### Problem statement
Ocean is a big open surface and its properties changes with time within the year, depending on the ocean current, the amount of heat received from the sun (which is influenced by globe’s tilt). Therefore, the suitable area for growing kelp might have seasonal change accordingly. As a result, we will need to look into time series to make a precise prediction.
### Research question
Which variable is more important to algae growth (temperature or nutrient)? 

What is the limitation factor for algae growth? 

What is the distribution of nutrient and temperature across the ocean and how it corresponds to algae?

## Datasets you will use:
We first attempted to work with google earth data, but we couldn't manage to download them.
Google Earth link:

Ocean color: https://developers.google.com/earth-engine/datasets/catalog/JAXA_GCOM-C_L3_OCEAN_CHLA_V2?hl=en

Temperature: https://developers.google.com/earth-engine/datasets/catalog/NOAA_CDR_OISST_V2_1 

We then decided to work with ERA5 data which offers Xarray data type, we only extract and work with the data from 2020 for speed and limited time:

Sea surface temperature: https://cds.climate.copernicus.eu/cdsapp#!/dataset/reanalysis-era5-single-levels-monthly-means?tab=overview

Surface air temperature: https://cds.climate.copernicus.eu/cdsapp#!/dataset/ecv-for-climate-change?tab=overview

Ocean colour: https://cds.climate.copernicus.eu/cdsapp#!/dataset/satellite-ocean-colour?tab=overview

For the Sea surface and air temperature, we can easily retrieve the monthly average data for year 2020.
However for the ocean colour, we had to download the data at noon for the first day of each month in 2020. We then combine those 12 Xarray files into 1 file and extracted only chlorophyllA data. Data was then exported into a Xarray file that is stored in Zenodo.

Data on Zenodo: https://zenodo.org/record/6348109#.Yi2AvBDMK3I

We attempted to download nitrate data from Biogeochemical Argo, but we were not able to download them. We used the argopy library to fetch the nitrate data however it doesn't have any variables that give us nitrate values, this is because the data is not well processed and compiled. We then tried to get data using the Euro-Argo fleet monitoring tool, we collected the nirtate data for all the floats (inactive and active). The floats activity status is based on current year but we decided to focus on the year 2020, it could be that some of these floats were working in 2020. The main issue was that this approach led to a lot of net cdf files, combining them was a diffficult task since we had to manually add a new time dimension and keep track of it across different floats, within each float there were different cycle numbers. The floats are the devices that float around in the ocean and collect the data, cycle number is the number of times they changed/started a new path/trajector. We decided to work with smaller datasets for nitrate data - near the Gulf of Mexico and Antartica. The motivation behind selecting these two regions was the 

Biogeochemical Argo: https://biogeochemical-argo.org/data-access.php

## Tools/packages you use (with links): 
Rasterio: https://rasterio.readthedocs.io/en/latest/

Xarray: https://docs.xarray.dev/en/stable/

Pandas: https://pandas.pydata.org

Numpy: https://numpy.org

Cartopy: https://github.com/SciTools/cartopy

Geopandas: https://geopandas.org/en/stable/about.html

Matplotlib: https://matplotlib.org


## Planned methodology/approach: 
Our approach is to find any visible changes (raster images - Rasterio, Xarray) over the years for alage growth, temperature and nutrients and use regression analysis (Numpy, Scipy, Pandas) to find out the most important factor, maybe try to predict the changes for this year. Initially we will zoom in the coast of Washington state, run our code and then expand to the whole world.

## Outcomes: 
Generate the time series for temperature and nutrients that correspond to the growth of algae (chlorophyll variable). Find the most important factor affecting algae growth using regression analysis.
Following is the time series for the chlorophyll a which is representative for algae growth.

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Time_series_chlorophyll_a_coastline_added.png)

We were not able to make each subplot bigger when using the coastline so it's hard to see the trend, so we had to present the chlorophyll a without the coast line as bellow:

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Time_series_chlorophyll_a.png)

We can see algae were abundant in the Anartica for 6 months from November to April, while Arctic has high concentration of alage from May to October of 2020 algae and totally lacked of algae during spring and winter.


Since Arctic has a high concentration of algae, we'll zoom in this area to study the affect of temperature on the algae's growth. To simplify the analysis, we used the mean value of chlorophyll a, temperature, and solar radiation in each region of globe as following:

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Mean_chlorophyll_a.svg)

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Mean_sea_surface_temperature.svg)

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Mean_surface_air_temperature%20(1).svg)

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Mean_solar_radiation.svg)


We found a weak correlation between algae and sea surface temperature for arctic.

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Artic_Chlorophyll_surface_temp.svg)

However, we found a strong correlation between air temperature and algae, which is a bit confusing because how algae lived in water was impacted by the air temperature.

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Corr_air_chlorA.svg)

We then think the air temperature was driven by the sun, which is why we looked into the solar radiation as belows:

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Solar_radiation.svg)

The location when solar radiation was strong within the year is coincide with the location where algae was blooming.
We further found that the solar radiation has a strong correlation with air temperature at arctic, which makes sense as the solar radiation is the source to heat up the air.

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Solar_vs_temperature%20(2).svg)

However, we saw a very low correlation between solar radiation and chlorophyll a.

![alt text](https://github.com/UW-GDA/ocean_color/blob/main/Images/Correlation_Solar_chlorA.svg)

This made us think there's probably a lag between solar radiation and algae's growth, probably when the sun shine to Arctic the air temperature take time to warm up and thus the iceberg will start melting and clear up the path for solar radiation to penetrate through water. Another potential explaination is that when the glacier melt, it might feed the nutrient for the algae to grow which is called as glacier silt effect. Either of these hypothesis could be checked with looking into the glacier data and Biological Argo which can be considered as a future research.

## Any other relevant information, images/tables, references, etc.
API to get the datasets: https://github.com/google/earthengine-api

https://archimer.ifremer.fr/doc/00645/75674/76575.pdf

https://euroargodev.github.io/argoonlineschool/Lessons/L03_UsingArgoData/Chapter24_ArgoDatabyFloat_ArgoPy.html

https://stackoverflow.com/questions/30946476/combine-multiple-netcdf-files-into-timeseries-multidimensional-array-python

https://argo.ucsd.edu/science/argo-and-the-modeling-community/

http://opendap.ccst.inpe.br/Observations/ARGO/tmp/netCDF4-0.9.8/docs/netCDF4.MFDataset-class.html

http://www.ifremer.fr/erddap/info/index.html?page=1&itemsPerPage=1000

http://www.ifremer.fr/erddap/tabledap/ArgoFloats.graph

## References
Argo (2020). Argo float data and metadata from Global Data Assembly Centre (Argo GDAC) – Snapshot of Argo GDAC of August 2020. SEANOE. https://doi.org/10.17882/42182#76230

Richard W. Reynolds, Viva F. Banzon, and NOAA CDR Program (2008): NOAA Optimum Interpolation 1/4 Degree Daily Sea Surface Temperature (OISST) Analysis, Version 2. [indicate subset used]. NOAA National Centers for Environmental Information. doi:10.7289/V5SQ8XB5

Murakami, H. (Jan. 2020). ATBD of GCOM-C chlorophyll-a concentration algorithm (Version 2). Retrieved from https://suzaku.eorc.jaxa.jp/GCOM_C/data/ATBD/ver2/V2ATBD_O3AB_Chla_Murakami.pdf


