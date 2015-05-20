--- 
title: "Reference Systems"
layout: post
category: Know the Basics
tags: [intro, projection, CRS]
---

{% include JB/setup %}

#### Pre-requisites:

- Setup
- Basics Overview
- Vectors and Rasters

#### Objectives:

- Understand purpose of using a projection on a map
- Recognize a few projection types
- Reproject vector data in QGIS

#### Exercise: [Understanding vector projections in QGIS](#vector-projection-exercise)

<!--
#### Data:

iRods access: <br>&nbsp;&nbsp;&nbsp;``/iplant/home/shard/aegis/Spatial-bootcamp/basics/reference-systems``

- [California state boundary (shapefile)](http://de.iplantcollaborative.org/dl/d/9FA8430E-6FDD-4579-BAD9-C33D33BFDA12/california_boundary.zip)
-->

----

## Coordinates

Data becomes spatial when it is assigned a location or coordinates. These coordinates allow us to reliably locate, transform and manipulate the data based on its location. In mathematics, coordinates are commonly represented using X and Y values on a chart.

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/Cartesian_CS.svg" width="256" alt="Cartesian coordinate system (comma)" src="{{BASE_PATH}}{{ASSET_PATH}}/images/Cartesian_CS.svg"/><br>ref: [^1]

Spatial data uses X and Y coordinates as well, however the spatial coordinates are related to a place on the earth. The X and Y values in this case often refer to <b>Latitude</b> and <b>Longitude</b>.

## Latitude and Longitude

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/Latitude_lines.svg" width="512px" alt="Latitude lines" class="center" src="{{BASE_PATH}}{{ASSET_PATH}}/images/Latitude_lines.svg"/><br>ref: [^2]

<br>

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/Longitude_lines.svg" width="512px" alt="Longitude lines" src="{{BASE_PATH}}{{ASSET_PATH}}/images/Longitude_lines.svg"/><br>ref: [^3]

<br>
----

## Projections <a name="projections"></a>

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/earthCRS.png" alt="By Djexplo (Own work) [CC0], via Wikimedia Commons - Earth Coordinate Reference System" src="{{BASE_PATH}}{{ASSET_PATH}}/images/earthCRS.png" /><br>ref: [^4]

Projections characterize spatial data by setting coordinate reference systems for each data set.

Each projection is defined on top of a geographic coordinate system or spheroid based off of two ellipsoids, major and minor axes. These geographic coordinates systems deliver the coordinates in degrees and account for the fact that the earth is not a perfect sphere.
 will convert the 3d spheroid of the earth into a 2-dimensional representation. Each projection type utilitizes a different technique to project the earth\'s image onto a plane. 

### Distortion

Since projections attempt to represent the 3-dimensional globe on a 2-dimensional plane, they will all suffer from some level of distortion. It is important to choose a projection which preserves the elements you are interested in studying.

----

## Coordinate Reference Systems

 A *Coordinate Reference System* is built on top of a *coordinate system*. A *coordinate system* is a set of mathematical rules for specifying how coordinates are to be assigned to each point, also known as a *projection*. A *coordinate reference system* is a coordinate system that is related to the real world by a datum, this can also be known as a *geographic coordinate system* or *spatial reference system*.

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/coordinate-grid.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/coordinate-grid.png" /><br>ref: [^5]

Projections are another name for projected coordinate systems. These projected coordinate systems compose a family of Coordinate Reference Systems. 

Projected coordinate systems are based off of Geodetic Coordinate Systems. These Geodetic coordinate systems are ellipsoidal models aimed at representing the aspherical nature of the earth.

----

## Earth as a Geoid

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/geoid.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/geoid.png" /><br>ref: [^6]

Although we normally see the earth represented as a sphere, its shape is actually more irregular. The earth has an equatorial bulge and various other undulations due to tectonics, volcanics and the earth's rotation. 

The changes in the surface mass are the subject matter of Geodesy. Geodesists use differences in the vertical direction of gravity along with crustal, tidal, and polar motion to determine exact measurements of the Geoid. Geometric computations can become unwieldy processes due to the complicated nature of the Geoid surface. In order approximate the geoid while making geometric calculation feasible, reference ellipsoids were calculated.

----

## Reference Ellipsoid

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/geoid-measure.gif" src="{{BASE_PATH}}{{ASSET_PATH}}/images/geoid-measure.gif" /><br>ref: [^7]

Reference ellipsoids have evolved over the years, moving from regional approximations to more precise global systems.

Regional ellipsoids like the North American Datum of 1927 which minimized distortion for the contiguous United States at the expense of more distant regions.

The modern reference ellipsoid, **WGS 84** was developed using satellite measurements and past Geodetic System parameters, and has been the reference ellipsoid used by the Global Positioning System. 

Most modern projections will use WGS 84 as the underlying reference ellipsoid, but it is important to check that your projection is defined correctly if you are dealing with old datasets. 

----

## Central Meridian

Greenwich is the standard central meridian used in global projections. This point is given the value of 0&#176; Longitude and serves as the origin the Global Positioning System. This delineation also leaves decides the use of Greenwich Mean Time as the standard time.

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/greenwich-meridian.jpg" src="{{BASE_PATH}}{{ASSET_PATH}}/images/greenwich-meridian.jpg" /><br>ref: [^8]

The Greenwich meridian has a monument dedicated to it in several cities.

## Projection Properties

**Conformal**

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/conformal_conic.svg.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/conformal_conic.svg.png"/><br>ref: [^9]

Also known as *fidelity of shape*, these projections preserve shape. This means that scale distortion must be the same in all directions and each parallel must cross every meridian at right angles. These projections are important for navigational and large-scale mapping[^17]
Examples include Mercator, and Lambert Conformal Conic.

**Equal Area**

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/True_size_of_Africa.jpg" src="{{BASE_PATH}}{{ASSET_PATH}}/images/True_size_of_Africa.jpg"/><br>ref: [^10]

Preserves the area relationships between regions. This maintain the proper ratio of area between regions. An example of this is the Mollweide projection. These projections are useful for statistical comparisons.

**Equidistant**

Preserves the proportional distances between any two points from their spherical distances.

----

## Geometric Projection Types

**Conic**

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/World_borders_lambert.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/World_borders_lambert.png"/><br>ref: [^11]

<br>

Conic projections are created by projecting part of a sphere onto a cone. Conic projections tend to be useful for representing data in temperate climates due to their location. Conic projections are not useful for representing global phenomena due to their construction.

**Azimuthal**

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/Azimuthal_Equidistant.jpg" src="{{BASE_PATH}}{{ASSET_PATH}}/images/Azimuthal_Equidistant.jpg"/><br>ref: [^12]

<br>
Azimuthal projections are created by flattening a side of the sphere from a reference point. Azimuthal projections are useful for mapping polar data.

**Cylindrical**

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/cylindrical_projection.jpg" src="{{BASE_PATH}}{{ASSET_PATH}}/images/cylindrical_projection.jpg"/><br>ref: [^13]

<br>

Cylindrical projections are created by projection a sphere onto a cylinder. Cylindrical projections suffer the least distortion along the line that it intersects the sphere, which is often around the Equator. This makes cylindrical projections useful for mapping tropical data. Examples include Mercator and Universal Transverse Mercator. 


**Polyhedral**

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/Polyhedral_projection.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/Polyhedral_projection.png"/><br>ref: [^14]

<img data-featherlight="//upload.wikimedia.org/wikipedia/commons/b/bb/Dymaxion_2003_animation_small1.gif" width="256" alt="Dymaxion 2003 animation small1" src="//upload.wikimedia.org/wikipedia/commons/b/bb/Dymaxion_2003_animation_small1.gif"/><br>ref: [^15]

<br>

Polyhedral projections, also known as interrupted projections seek to minimize global distortion by tearing the sphere at specific areas. A common method for creating polyhedral projections is to coerce the sphere into a 3-dimensional geometric object such as a cube which is the then unraveled. Some examples include Dymaxion and Waterman's butterfly.

<br>

----
<!--
## Checking the projection

It is important to check the projection of your data to make sure they share the same projection prior to performing any spatial analysis. 

The example below utlizes the <a href="http://www.gdal.org/" target="_blanK">Geospatial Data Abstraction Library</a> within the command-line. GDAL is an excellent tool for spatial operations.

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/gdalinfo.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/gdalinfo.png" alt="Using GDAL to check projections"/>
-->
<a href="http://spatialreference.org" target="new">SpatialReference.org</a> is an extremely useful resource that houses definitions for all official projections in a variety of formats. This is a great place to find proj4 strings. 

<a href="https://trac.osgeo.org/proj/" target="_blank">PROJ.4</a> is a cartographic projection library written in <a href="http://en.wikipedia.org/wiki/C_%28programming_language%29" target="_blank">C (programming language)</a>, used for converting projections.

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/spatialreference.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/spatialreference.png"/>

Since there are a few thousand different projections, with their own area of interest, it is likely that you will come upon datasets with different projection in your project. The easiest way to resolve projection disputes is to decide on the projection for your project before gathering data and save the proj4 string assigned to the projection. This string will allow you to project your datasets to the proper coordinate reference system.<br><br>

<table style="margin: 0px 25px;">
<tr>
<td><h5>EPSG:4326 (WGS84)</h5><br>
<pre><code>+proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs</code></pre></td>
</tr>
<tr>
</tr>
<td><h5>Custom proj4</h5>
<pre><code>+proj=lcc +lat_1=45.89893890000052 +lat_2=47.69601440000037 +lat_0=46.8 +lon_0=2.33722917 +x_0=600000 +y_0=200000 +a=6378249.145 +b=6356514.96582849 +pm=2.337229167 +units=m +no_defs</code></pre></td>
</tr>
</table>

<br>

<a name="vector-projection-exercise"></a>

_NOTE: When reprojecting a raster, you should also resample your raster to ensure that the cells have the same width and height. The cells will distort in the new projection and most GIS software will refuse to read a raster with irregular cells._

----

<h3>Projection Exercise</h3>

There are several methods to reproject data. Two methods are explained below; a temporary change of projection within a QGIS project, or reprojecting the vector and saving it to the file.

This brings up an excellent point; always check your projection! Always! 

Projection errors are very common and are often misunderstood. It make take some time before fully nderstanding. Practice makes perfect.

This next exercise will explain projections and reprojections in QGIS. Very important!

<h4>1. Changing project projection</h4>

<ol>
<li>Open a new project and import vector california_boundary.shp through iRods:<br><br>
&nbsp;&nbsp;&nbsp;<code>/iplant/home/shared/aegis/Spatial-bootcamp/basics/raster/california_boundary.shp</code><br><br>
Or download here, unzip, and <strong>Add Vector Layer</strong> <img src="{{BASE_PATH}}{{ASSET_PATH}}/images/add-vector.png"/>:<br> <a href="http://de.iplantcollaborative.org/dl/d/9FA8430E-6FDD-4579-BAD9-C33D33BFDA12/california_boundary.zip">california_boundary.zip</a><br><br>
Your workspace should look similar to the one below:<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-1.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-1.png" alt="Spatial Data Bootcamp: QGIS - import vector"/>
</li>
<li>Configure projection
<ol>
<li>There are several methods to configuring projections: set layer projections, set project projection (with on-the-fly projection), and reprojecting layers. There are also several methods to reprojecting layers which is covered later in this section.<br><br> </li>
<li>To view the current map projection, look towards the bottom right of the QGIS GUI:<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-2.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-2.png" alt="Spatial Data Bootcamp: QGIS - map projection"/><br><br>You can also click this button to open the <strong>Project Properties</strong> CRS settings.<br><br>This current map projection is EPSG:4326. As it was discussed above, EPSG:4326 refers to World Geodetic System established in 1984, last revised in 2004 (as of May 2015) <sup id="fnref:1"><a class="footnote" href="#fn:1">1</a></sup>. This is a common reference system in web mapping and is also used with the GPS.<br><br></li>
</ol>
</li>
<li>To change the project projection <em>Menu Bar > Project > Project Properties > CRS</em><br><br>You're able to change the project projection to a predefined coordinate reference system (QGIS terms: CRS) or define your own. It's most probable that you'll be using a predefined CRS. You must enable 'on-the-fly' CRS transformation to change the project projection; this reprojects all subsequently imported layers to this defined CRS. CRSs will make or break your research. This will be discussed in later lessons.<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-3.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-3.png" alt="Spatail Data Bootcamp: QGIS - coordinate reference systems"/></li>
<li>Let's change the Projected Coordinate System and see how our data obscures each time. Search for EPSG:3378, just type '3378' in the <em><strong>filter</strong></em> and reproject our data.<br><br><strong>Reminder:</strong> click <em>Apply</em> then <em>OK</em> to confirm changes each time.<br><br>If your data disapears from the map canvas: <em>Right-click layer (layer list) > Zoom to layer</em>.<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-5.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-5.png" alt="Spatial Data Bootcamp: QGIS - California with EPSG:3378"/><br><br>Reproject our data to EPSG:3311. What differences do you notice? Do you think you can compare (perform spatial functions) two different data sets, one with each projection?<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-6.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-6.png" alt="Spatial Data Bootcamp: QGIS - California with EPSG:3311"/>
</li>
<li>Canvas/map units
<ol>
<li>If we have space, we have distances. Check your <em><strong>Canvas Units</strong></em> to check our unit of measure: <em>Menu Bar > Project Properties > General > Canvas Units</em>.<br><br>If you're still using the ESPG:3311 projection, then you will be using <strong>Meters</strong> as your unit of measure. This is critical- you have two data sets, one with a projection in meters and the other in feet, do you think there will be any issues while performing a spatial function?<br><br>There are several ways to go about <em>wrangling</em> your data, some which will be covered in <strong>Data Collection</strong> and <strong>Data Wrangling</strong>.<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-7.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-7.png" alt="Spatial Data Bootcamp: QGIS - Map units"/>Close the Project Properties.</li>
</ol>
</li>
</ol>

<h4>2. Reprojecting vector data</h4>
<ol>
<li>Reproject data with geoalgorithms:
<ol>
<li>Open the <strong>Processing Toolbox</strong>: <em>Menu Bar > Processing > Toolbox</em><br><br>Then search "reproject", your results should be similar to the ones below. Double click on <strong>Reproject layer</strong> from the <strong>Vector</strong> category.<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-8.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-8.png" alt="Spatial Data Bootcamp: QGIS - search for reproject"/>
</li>
<li>Select Target CRS<br>

<ol>
<li>Input layer should be <strong>california_boundary [EPSG:4326]</strong>.<br><br>Click the ellipses <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-10.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-10.png" alt="Spatial Data Bootcamp: QGIS"/> to the right of <strong>Target CRS</strong> and change the CRS to <strong>EPSG:3311</strong>.<br><br>A temporary (stored in memory) layer will be created if you do not define a file location. You must define a location if you wish to use this reprojected.<br><br>This how how you <em>SAVE</em> your vector layer with a given projection.<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-9.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-9.png" alt="Spatial Data Bootcamp: QGIS - reproject layer"/>
</li>
<li>The output shapefile is created with all necessary files. California boundary saved with EPSG:3311:<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-11.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-11.png" alt="Spatial Data Bootcamp: QGIS - save projected layer"/>Return to QGIS.<br><br>
</li>
</ol>
</li>
</ol>
</ol>
<li>Saving layer with projection (reprojection):<br><br>This one is simple: <em><strong>Right-click layer (layer list) > Save As > (see image below)</strong></em><br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-12.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/projection-12.png" alt="Spatial Data Bootcamp: QGIS - save as to reproject"/><br><br>You have now been introduced to projections and their importance.<br><br>Close this project.<br></li>
</ol>

<hr>
<br><br>

<ol>
<li><a title="By Cartesian-coordinate-system.svg: K. Bolino derivative work: F l a n k e r (Cartesian-coordinate-system.svg) [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ACartesian_coordinate_system_(comma).svg">By Cartesian-coordinate-system.svg: K. Bolino derivative work: F l a n k e r (Cartesian-coordinate-system.svg) [Public domain], via Wikimedia Commons</a></li>
<li><a title="By Latitude_(PSF).png: Pearson Scott Foresman, donated to the Wikimedia Foundation derivative work: Gregors (talk) 08:13, 27 March 2011 (UTC) (Latitude_(PSF).png) [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ALatitude_lines.svg" >By Latitude_(PSF).png: Pearson Scott Foresman, donated to the Wikimedia Foundation derivative work: Gregors (talk) 08:13, 27 March 2011 (UTC) (Latitude_(PSF).png) [Public domain], via Wikimedia Commons</a></li>
<li><a title="By Longitude (PSF).png: Pearson Scott Forman derivative work: Gregors (Longitude (PSF).png) [CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ALongitude_blue.svg">By Longitude (PSF).png: Pearson Scott Forman derivative work: Gregors (Longitude (PSF).png) [CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons</a></li>
<li><a title="By Djexplo (Own work) [CC0], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ALatitude_and_Longitude_of_the_Earth.svg">By Djexplo (Own work) [CC0], via Wikimedia Commons</a></li>
<li><a title="By Geek3 (Own work) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ASphere_wireframe.svg">By Geek3 (Own work) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons</a></li>
<li><a title="By NASA/JPL/University of Texas Center for Space Research. [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AEarth_gravity.png">By NASA/JPL/University of Texas Center for Space Research. [Public domain], via Wikimedia Commons</a></li>
<li><a title="By NASA/JPL (http://sealevel.jpl.nasa.gov/gallery/posters.html) [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AJason-1_measurement_system.gif">By NASA/JPL (http://sealevel.jpl.nasa.gov/gallery/posters.html) [Public domain], via Wikimedia Commons</a></li>
<li><a title="By Apletters (Own work) [CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0) or GFDL (http://www.gnu.org/copyleft/fdl.html)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AMeridian-at-Greenwich.jpg">By Apletters (Own work) [CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0) or GFDL (http://www.gnu.org/copyleft/fdl.html)], via Wikimedia Commons</a></li>
<li><a title="By USGS, Mysid [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ALambert_conformal_conic.svg">By USGS, Mysid [Public domain], via Wikimedia Commons</a></li>
<li><a title="By Kai Krause [CC0], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ATrue_size_of_Africa.jpg">By Kai Krause [CC0], via Wikimedia Commons</a></li>
<li><a title="By Koenb at Dutch Wikipedia (Original text: productie van de afbeelding uit het .shp-bestand: Koenb) [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AWorld_borders_lambertcc000045.png">By Koenb at Dutch Wikipedia (Original text: productie van de afbeelding uit het .shp-bestand: Koenb) [Public domain], via Wikimedia Commons</a></li>
<li><a title="By RokerHRO (Own work) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AAzimuthal_Equidistant_S90.jpg">By RokerHRO (Own work) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons</a></li>
<li><a title="By KoenB (Own work) [Public domain], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ACilinderprojectie-constructie.jpg">By KoenB (Own work) [Public domain], via Wikimedia Commons</a></li>
<li><a title="By Koenb at nl.wikipedia (Original text : KoenB) [Public domain], from Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3APolyederprojectie-6-rendered.png">By Koenb at nl.wikipedia (Original text : KoenB) [Public domain], from Wikimedia Commons</a></li>
<li><a title="By Chris Rywalt (POVRay) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC-BY-SA-3.0 (http://creativecommons.org/licenses/by-sa/3.0/)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3ADymaxion_2003_animation_small1.gif">By Chris Rywalt (POVRay) [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC-BY-SA-3.0 (http://creativecommons.org/licenses/by-sa/3.0/)], via Wikimedia Commons</a></li>
<li>http://www.progonos.com</li>
</ol>
