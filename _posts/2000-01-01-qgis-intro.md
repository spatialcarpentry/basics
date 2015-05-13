---
title: "QGIS Intro"
layout: post
category : Know the Basics
tagline: 
tags : [qgis, projections, raster, vector, reproject]
---

#### Pre-requisites:

- Setup
- Basics Overview
- Raster & Vector
- Reference Systems
- Installation of QGIS

#### Objectives:

- Gain a basic understanding of QGIS
- Set up project properties
- Import raster and vector data
- Inspect vector and raster data
- Reproject vector/raster data

#### Data: 

iPlant Data Store: <br>&nbsp;&nbsp;&nbsp;``/Community Data/aegis/Spatial-bootcamp/basics/qgis-intro``

- [Arizona Counties boundaries (shapefile)](http://de.iplantcollaborative.org/dl/d/31085E1F-F3E3-4E30-8848-FC14011E6015/arizona_counties.zip)
- [data two - Western United States MODIS MOD09Q1 - 2015-04-23 (raster)](link-to-data-two)

{% include JB/setup %}

----

If you haven't already, see [Installing QGIS](http://spatialcarpentry.github.io/setup/setup/qgis-install/) before continuing. Subsequent lessons depend on a QGIS installation.

<h3>1. About QGIS</h3>

<a title="By User:Anitagraser on QGIS Wiki, User:Anitagraser (http://www.qgis.org/wiki/File:QGis_Logo.png) [CC BY-SA 3.0 (http://creativecommons.org/licenses/by-sa/3.0)], via Wikimedia Commons" href="http://commons.wikimedia.org/wiki/File%3AQGis_Logo.png"><img width="128" alt="QGis Logo" src="//upload.wikimedia.org/wikipedia/commons/thumb/7/71/QGis_Logo.png/128px-QGis_Logo.png"/></a>

> QGIS is the best GIS tool in the free and open-source software (FOSS) community.

> QGIS is a user friendly Open Source Geographic Information System (GIS) licensed under the GNU General Public License. QGIS is an official project of the Open Source Geospatial Foundation (OSGeo). It runs on Linux, Unix, Mac OSX, Windows and Android and supports numerous vector, raster, and database formats and functionalities.

This lesson is a brief exploration of QGIS. <a href="http://docs.qgis.org/2.6/en/docs/user_manual/" target="new">See the official QGIS User Guide here</a> for topics not covered below.

<h3>2. Explore QGIS</h3>
<ol>
<li> If you haven't done so already, **open QGIS to begin exploring the interface**.<br><br>
Below is the QGIS graphical user interface (GUI), allowing for much easier access to geoalgorithms (as compared to the command-line interface!). It has the standard top menu bar and icons linking to most commonly used tools as you'd see in any other GUI. Data in the map view is of Washington state geology symbolized by geologic type.<br><br>
 <img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-gui.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-gui.png"/><br>
<table class="table-no-border">
<tr>
<td><h6>1. Menu Bar</h6><p>The menu bar provides access to QGIS features. Hover over to view menu bar options. The QGIS version is displayed while not hovering over the menu bar. Most common features or tools are accessable through the toolbar icons which will be the prefered method throughout this QGIS introduction. Add data through <em>Menu Bar > Layer > Add Layer</em></p></td>
</tr>
<tr>
<td><h6>2. Toolbar</h6><p>The toolbar provides access to most standard QGIS functions. Go to <em>Menu Bar > View > Toolbars</em> to activate or deactivate toolbars. Hover over tools to view the description and puropose.</p></td>
</tr>
<tr>
<td><h6>3. Map Legend</h6><p>The map legend is a list of all layers in the project. Each layer can be turned on or off with the layer's checkbox.  It's possible to group layers.</p></td>
</tr>
<tr>
<td><h6>4. Map View</h6><p>The map view displays the active layers in the map project. You can set the map view extent by right-clicking on a layer and selecting <em>Zoom to layer extent</em></p></td>
</tr>
<tr>
<td><h6>5. Status Bar</h6><p>The status bar displays current position in map coordiantes (e.g., meters or decimal degrees) as the mouse pointer moves across the map view. To the left of the coordinate display is the button gor toggling extents and mouse position display. To the right of the map coordinates is the scale, which may be set to one of the predefined zoom extends of 1:500 to 1:1,000,000. This scale setting will adjust as you zoom or pan throught the map view. Options for map rendering are to the right of the current map scale setting. To the far right is the current CRS for the map project.</p></td>
</tr>
<tr>
<td><h6>6. Processing Toolbox</h6><p>The processing toolbox must be turned on by naviagting to <em>Menu Bar > Processing > Toolbox</em>. This helpful tool allows searching by keyword for the geoalgorithm from each of the active processing roviders.</p></td>
</tr>
</table>
</li>

<li>Project properties:<br>
<ul>
<li>To view project properties, navigate to <em>Menu Bar > Project > Project properties</em></li>
<li>Here in project properties you're able to give your project a title, configure projections, save to relative paths (because we're creating links to our data in order to import into QGIS!), and other items relate to the project itself. QGIS referes to projections as the Coordinate Reference System, or CRS.</li>
</li>
<li>Vector/Raster geoalgorithms<br>
<ul>
<li>Vector and raster spatial functions are accessed through <em>Menu Bar > Vector/Raster</em>, or through the processing toolbox. QGIS refers to spatial functions as geoalgorithms, which are explained below.</li>
</ul>
</li>
<li>Working with Project Projections<br>
<p><blockquote>QGIS allows users to define a global and project-wide CRS (coordinate reference system) for layers without a pre-defined CRS. It also allows the user to define custom coordinate reference systems and supports on-the-fly (OTF) projection of vector and raster layers. All of these features allow the user to display layers with different CRSs and have them overlay properly.[^2]</blockquote></p>
<p>Each new project starts with the global default projection, [EPSG:4326 - WGS 84](http://www.spatialreference.org/epsg/wgs-84/):<br><br>
<pre>proj=longlat +ellps=WGS84 +datum=WGS84 +no_defs</pre><br>
This can be changed at <em>Menu Bar > Settings > Options > CRS > Default CRS for new projects</em><br><br>
However, this is not the same as changing the project projection. You may define the project projection from <em>Menu Bar > Project > Project Properties > CRS</em>. Also keep in mind, the CRS of a new project will change to the CRS of the first layer added to the project.<br><br>
'On the fly' CRS transformation is not enabled by the default QGIS installation.</p>
</li>
</ul>
</li>
</ol>

<h3>3. Providers</h3>
<p>QGIS utilizes spatial functions or geoalgorithms through a set of Providers which are also free open-source software. Below is list of some QGIS Provider.</p> 

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-providers.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-providers.png"/>

<h3>4. Geoalgorithms</h3>
<p>Some basic spatial functions are clip, buffer, and intersect. These are covered in <a href="http://spatialcarpentry.github.io/spatial-analysis/ask%20some%20questions/functions/">Spatial Functions</a>. So, QGIS is simply a graphical user interface for accessing these command-line-based tools. The main geoalgorithms are provided by GDAL, GRASS, and QGIS. Navigating through the Menu Bar will display the general name of the tools. Accessing these tools through the Processing Toolbox will display each Provider and their functions.</p>

<img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-toolbox.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-toolbox.png"/>

<h3>5. Exercise: Inspect vector data</h3>
<ol>
<li>Import vector data<img src="{{BASE_PATH}}{{ASSET_PATH}}/images/add-vector.png"/>
<ol>
 <li>If you have not already, go to the top of this page to the <a href="#data"><strong>Data</strong></a> section and download both vector and raster data sets.</li>
 <li>Open QGIS and import the Arizona Counties shapefile by clicking the <strong>Add Vector Layer</strong> button in the Toolbar or by navigating through <em>Menu Bar > Add Layer > Add Vector Layer.</em><br><br>Subsequent exercises will refer to adding data through the buttons in the Toolbar.<br><br></li>
 <li>Click <strong>Browse</strong> to locate the shapefile: arizona_counties.shp<br><br><strong>Reminder:</strong> A shapefile contains 5 files, however only open the &#42;.shp extension in QGIS (or other GIS applications)<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-1.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-1.png" alt="QGIS - Add vector layer"/></li>
 <li>We now visualizing counties in Arizona. <strong>Think about it:</strong> We are not actually visualizing the single boundary of Arizona, but the boundaries of its counties which complete the boundary of Arizona.<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-2.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-2.png" alt="Spatial Carpentry: QGIS - viewing vector data"/></li>
  </ol>
</li>
<li>View vector properties
<ol>
<li>To view vector (and all layers) attributes, <em>Right-click layer > Open Attribute Table</em><br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-3.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-3.png" alt="Spatial Carpentry: QGIS - view vector data attributes"/><br><br>This data was extracted from Global Administrative Areas, which will be covered in <strong>Data Collection</strong>. This is simple boundary data; just gives us country, state, county name, and unique identifiers for each entry. Example uses of this type of data are: joining Census tabular data; visualizing boundaries; cutting satellite imagery to a desired area.</li>
</ol>
</li>
<li>Configure projection
<ol>
<li>There are several methods to configuring projections: set layer projections, set project projection (with on-the-fly projection), and reprojecting layers. There are also several methods to reprojecting layers which is covered later in this section. </li>
<li>To view the current map projection, look towards the bottom right of the QGIS GUI:<br><br><img data-featherlight="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-4.png" src="{{BASE_PATH}}{{ASSET_PATH}}/images/qgis-intro-4.png" alt="Spatial Carpentry: QGIS - map projection"/><br><br>This current map projection is EPSG:4326. As it was discussed in <strong>Reference Systems</strong>, EPSG:4326 refers to World Geodetic System established in 1984, last revised in 2004 (as of May 2015) <sup id="fnref:1"><a class="footnote" href="#fn:1">1</a></sup>. This is a common reference system in web mapping and is also used with the GPS.</li>
<li>To change the project projection <em>Menu Bar > Project > Project Properties > CRS</em><br><br>You're able to change the project projection to a predefined coordinate reference system (QGIS terms: CRS) or define your own. It's most probable that you'll be using a predefined CRS. You must enable 'on-the-fly' CRS transformation to change the project projection; this reprojects all subsequently imported layers to this defined CRS. CRSs will make or break your research. This will be discussed in later lessons.<br><br>Geographic Coordinate Systems are what the Projected Coordinate Systesm are referenced to...<br><br></li>
</ol>
</li>
<li>Metadata</li>
<li>Styling</li>
<li>Map units</li>
</ol>
<h3>6. Inspect raster data (need data!)</h3>
<ol>
<li>Import raster data <img src="{{BASE_PATH}}{{ASSET_PATH}}/images/add-raster.png"/></li>
<li>Raster properties</li>
<li>Metadata</li>
<li>Raster stats</li>
<li>Resolution - zoom in close enough to see pixels</li>
</ol>
<h3>7. Reproject vector</h3>
<ol>
<li>Open a new project and import vector (need data!)</li>
<li>Reproject steps..</li>
</ol>

---- 

<div class="footnotes">

<p>References:</p>

<ol>
<li id="fn:1"><a href="http://web.archive.org/web/20120402143802/https://www1.nga.mil/ProductsServices/GeodesyandGeophysics/WorldGeodeticSystem/Pages/default.aspx">"World Geodetic System website of the NGA (archived April 2012)". National Geospatial-Intelligence Agency.</a></li>
</ol>
