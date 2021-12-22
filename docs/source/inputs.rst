Inputs
######

For clarity, we refer to ‘inputs’ as the inputs to map2loop and map2model libraries and ‘augmented data’ as the products of map2loop. The augmented data in turn form the inputs to the target 3D geological modelling engines. All temporary inputs and outputs from the related map2model library are wrapped within the map2loop library.
   
The information contained in a geological map falls into three categories of geometric data: positional data such as the position of faults, intrusive and stratigraphic contacts; gradient data, such as the dips of contacts or faults and finally spatial and temporal topological data, such as the age relationships between faults and stratigraphic units. As modellers we combine all of these direct observations with conceptual information: knowledge from near-by areas; our understanding of the tectonic history of the region, including assumptions regarding the subsurface geometry of faults and plutons, and generic geological knowledge (such as our understanding of pluton emplacement mechanisms) to provide sufficient constraints to build a 3D geological model. Often, these concepts are communicated via geological cross-sections supplied with the map, however these are typically based on limited or no additional data as they combine the conceptual ideas mentioned above with local positional and gradient information derived from the map, although they can now routinely be validated using regional geophysical datasets such as gravity and magnetics (Spampinato et al., 2015; Martin et al., 2013). Even when we have seismic reflection data in basins, the role of conceptual biases cannot be ignored (Bond et al., 2007; Bond, 2015) In addition, the map will usually supply a stratigraphic column that provides a more direct but simplified representation of stratigraphic relationships.
   
In this library we draw inspiration from existing manual workflows and structural decision-making processes by developing a suite of algorithms that allow us to automatically deconstruct a geological map to recover the necessary positional, topological and gradient data as inputs to different 3D geological modelling codes. Some of the code simply reproduces the 3D modelling packages’ abilities to import different datasets, however much of it is dedicated to extracting information that is contained within the map but rarely extracted from it in a systematic fashion, as it can be rather tedious to do so, although systems such as GMDE certainly help (Allmendinger, 2020). 
   
The libraries described here retrieve information from GIS layers or online servers, clean and decimate the data if needed, and then go through a series of data analysis steps to extract information from GIS layers stored locally or on online servers. This information includes: the local stratigraphy, the geometries of the basal contacts of units, and faults, estimates of local offsets along faults, and estimates of local formation thickness. Once these and other information have been extracted, they are output as standard formats (Graph Meta Language (GML), csv, geotif and ESRI shapefile formats) so that the target 3D modelling systems can use them as they are. 
   
Once the input parameters are defined, it is important to emphasise that the entire workflow is automated, so all decisions 
about choices of parameters are made up front and the consequences of these decisions can be directly analysed in terms of 
the augmented outputs of the map2loop code, or via the 3D models that can themselves be automatically built from these 
augmented outputs. Once the Configuration File has been generated, and the workflow control parameters defined in the map2loop Control Script, all further actions are fully automated, from accessing the input data, up to and including the construction of the 3D model using LoopStructural or GemPy. 
   
In the example we present in these docs, we use the 2016 1:500 000 Interpreted Bedrock Geology map of Western Australia 
and the WAROX outcrop database (GSWA, 2016) as sources of the data needed to build a first-pass model of 
the region around the Rocklea Dome in the Hamersley Region of Western Australia. The area consists of upright refolded folds of Archean and Proterozoic stratigraphy overlying an Archean basement cut by over 50 NW-SE trending faults that form a part of the Nanjilgardy Fault System (Thorne and Trendall, 2001). 
   
The map2loop library uses the Geopandas library to load data from several persistent formats (ESRI shapefiles, 
MapInfo tab files, JavaScript Object Notation (JSON) format files) and or from a Web Feature Service (WFS). 
Geospatial data can be in any standard coordinate reference system (assuming a European Petroleum Survey Group 
(EPSG) code is supplied, http://epsg.io). These libraries are used to load and transform the input geological 
geometries and attributes. 
   
In the following subsections, the descriptions of the six sources of input data used by map2loop and map2model,
are deliberately generic, as these two libraries uses a configuration file 
that allows the user to define which fields in the GIS layers or WFS servers contain which information. 
A Jupyter notebook (http://jupyter.org) helps the user to create this HJSON format configuration file from 
the input layers (Utility 1 - Config file generator.ipynb). The minimum input data required to run map2loop is 
described in the section Minimum input data requirements.
   