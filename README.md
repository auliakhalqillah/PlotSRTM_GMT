# Plot Shuttle Radar Topography Mission (SRTM) Data Using Generic Mapping Tools (GMT) 6


The SRTM data (land data) and Bathymetry data (Ocean data) are combined to produce a good map by using Generic Mapping Tools (GMT) version 6. The SRTM and Bathymetry data are downloaded separately where:

- The SRTM data can be downloaded in http://dwtkns.com/srtm/ and 
- Bathymetry data can be downloaded in https://maps.ngdc.noaa.gov/viewers/wcs-client/. 

All process in this tutorial is operated in Ubuntu Operating Sytem (14.04) 

<img width=50 height=50 src="https://cdn0.iconfinder.com/data/icons/flat-round-system/512/ubuntu-512.png"> <img width=100 height=50 src="https://www.generic-mapping-tools.org/_static/gmt-logo.png">

# Preparation
## Install  Geospatial Data Abstraction Library (GDAL) for Ubuntu
Type the following command in your terminal:
```
sudo add-apt-repository ppa:ubuntugis/ppa && sudo apt-get update
sudo apt-get update
sudo apt-get install gdal-bin
sudo apt-get install libgdal-dev
```
## Install  Geospatial Data Abstraction Library (GDAL) for Mac OS
To install GDAL for Mac OS, you can download the GDAL on http://www.kyngchaos.com/software/frameworks/ and select the GDAL version depends on your Mac OS version. The installation process just click on the downloaded file and follow the steps.

# Generate Map
1. Download the SRTM data on http://dwtkns.com/srtm/. Select a region that you want, in this tutorial Sumatra Island is selected (blue arrow in Figure 1). Just click on the box that you want, and click `Download GeoTIFF button`.

![Figure 1](https://github.com/auliakhalqillah/PlotSRTM_GMT/blob/main/srtm1.png)

Now, we have some files SRTM data for Sumatra Island there are

- srtm_56_11.zip, 
- srtm_56_12.zip,
- srtm_56_13.zip, 
- srtm_57_12.zip, 
- srtm_57_13.zip, 
- srtm_57_14.zip, 
- srtm_58_13.zip and 
- srtm_58_14.zip. 

By default, all of these data are stored in Downloads folder. So, move all of these data to another folder, let say I create a new folder __mapGMT__ in Documents folder and I move these data to the __mapGMT__ folder.

2. Extract the data manually and will produces new folder for each data.
3. Create a new folder. Name it as __SRTM__ for example.
4. For each folder that has been extracted, copy the `Tif` file to __SRTM__ folder. 
5. To merge all `Tif` files, we use `gdalwrap` command. Open your terminal and go to the SRTM folder that you created before. For an example, I will go to the __SRTM__ folder by typing the following command:

```
$ cd /Documents/mapGMT/SRTM
:~/Documents/mapGMT/SRTM$ ls -lrt
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_56_11.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_56_12.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_57_12.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_56_13.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_57_13.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_58_13.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_57_14.tif
-rw-rw-r-- 1 aulia aulia 72096675 Sep 20  2008 srtm_58_14.tif

:~/Documents/mapGMT/SRTM$ gdalwarp *.tif sumatra.tif
```

It will produces `sumatra.tif` file that has been merged.

6. Convert to GRD file using script [srtm2grd.scr](https://github.com/auliakhalqillah/PlotSRTM_GMT/blob/main/srtm2grd.scr) by typing the following command in your terminal
```
:~/Documents/mapGMT$ bash srtm2grd.scr
```
and wait the process. Once the process is done, you will get output file: 

- __sumatra.grd__, 
- __sumatra_resamp.grd__, 
- __sumatra_grad.grad__,
- __sumatra_topo.cpt__

7. Plot the map using script [plot_srtm.scr](https://github.com/auliakhalqillah/PlotSRTM_GMT/blob/main/plot_srtm.scr) by typing following command in youor terminal
```
$ bash plot_srtm.scr
```
Finally, the final result as shown in figure bellow

![fig2](https://github.com/auliakhalqillah/PlotSRTM_GMT/blob/main/srtm_result.png)
