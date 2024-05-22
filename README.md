# IW-Network-Extraction
This repo contains the accompanying code for the manuscript published in Nature Water (Liljedahl, A.K., Witharana, C., and Manos, E., 2024. The Capillaries of the Arctic Tundra. Nature Water xxxxxxx).
   
Given a folder containing polygon shapefiles of IWPs detected from Maxar satellite imagery using a Mask RCNN-based deep learning pipeline (one IWP shapefile for each Maxar satellite image), the code follows a series of basic geospatial operations performed upon the polygon geometries:
   
**(1)** Adopting the methodology from _Ulrich, Mathias, et al. "Quantifying wedge‐ice volumes in Yedoma and thermokarst basin deposits." Permafrost and Periglacial Processes 25.3 (2014): 151-161_, we apply a buffer that represents widths at the top of ice wedges around each IWP. A buffer width of 5 meters was chosen, since this allowed buffers of adjacent polygons to overlap. Realistically this is needed, since the same ice-wedge would be repsonsible for forming two very close IWPs. With a buffer width too small, this step would create two buffers that do not touch, indicating the presence of two ice-wedge polgyons between adjacent polygons. These buffers are then converted to raster format in order to perform skeletonization, which is an image processing technique.
   
**(2)** The buffer along the outside of the ice-wedge polygons is skeletonized. This step finds the centerline of the buffers, representing the network of ice-wedges that form the IWPs in a landscape.
   
**(3)** Because the IWP detection model was run on individual Maxar satellite image scenes that have a small degree of overlap, the extracted ice-wedge centerline layers are clipped to remove duplicate lines.

**(4)** The length of all the ice-wedge centerlines extracted from each IWP polygon shapefile is calculated and summed.

## Environment setup
To setup the required environment, you must have the licensed ArcGIS Pro software on your local PC, then clone the ArcGIS Pro Python environment. Directions on this can be found here https://pro.arcgis.com/en/pro-app/3.1/arcpy/get-started/clone-an-environment.htm. Once the environment is cloned, make sure the two following packages are additionally installed. 

```
Name                          Version
scikit-image                  0.17.2
rasterio                      1.3.9
geopandas                     0.14.3
```
