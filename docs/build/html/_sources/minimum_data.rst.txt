Minimum input data requirements
###############################

**5.1 Vector Geospatial File Data Formats:**

'DXF': 'raw', 'CSV': 'raw', 'OpenFileGDB': 'r', 'ESRIJSON': 'r', 'ESRI Shapefile': 'raw', 'GeoJSON': 'rw', 'GeoJSONSeq': 'rw', 'GPKG': 'rw', 'GML': 'raw',  'MapInfo File': 'raw'

r=read, a=append, w=write

- geology polygons with stratigraphic code and rock type info (required)
  
- fault polylines (required)

- bed dips as points in dip, dip direction (required)

- mineral deposit layer (optional)

- fold axial trace layer (optional)
  
**5.2 Geology Polygons (or Multipolygons):**

- no gaps or overlaps between polygons, nodes from neighbouring polygons coincide (we have code to fix errors when the mismatch is smaller than the minimum node spacing).

- Stratigraphic Coherency:
  - Ideally the map should consist of polygons which all have the same stratigraphic heirarchical level, e.g. all formations, all groups, all members etc. This is often not the case, and it makes unravelling the stratigraphy more complex, as the parent and child may appear in the same map, so the age sorting needed to build the model becomes ambiguous. National or state-level stratigraphies, and even stratigraphies described on map sheet legends are by definition simplifications of the the local system extracted by *map2loop*. *map2loop* uses the local stratigraphy first and then uses the regional stratigraphy (if available) as a guide to reduce the uncertainty.
  
- Attributes with (data type) and {code} (see section 2.2):
    - Fine Scale Stratigraphic coding, e.g. formation name (str) {'c'}
    - Coarser Scale stratigraphic coding, such as its parent, e.g. group (str) {'g'}
    - Alternate Coarser Scale stratigraphic coding, e.g. group (str) {'g2'}
    - Relative or absolute maximum age of Fine Scale Stratigraphic Code (float) {'max'}
    - Relative or absolute minimum age of Fine Scale Stratigraphic Code (float) {'min'}
    - Litho code to help determine if rock is intrusive (str) {'ds'}
    - Litho Code to help detemrine if this is a sill-like body (str) {'sill'}
    - Unique ID of polygon (str) {'o'}

**5.3 Fault Polylines:**

- single polyline per fault (no multipolylines)
- nodes on faulted boundaries coincident with geology polygon nodes

- Attributes:
    - Text that identifies polyline as a fault (str) {'fault'}
    - Dip of fault (str or float) {'fdip'}
    - Dip Direction of Fault (str or float) {'fdipdir'}

**5.4 Bedding Points:**

- single points (no multipoints)

Attributes:
  - Dip (float) {'d'}
  - Dip Direction or Strike (float) {'dd'}
  - Code to show what convention is used: Strike RHR, or DD at the moment (str) {'otype'}
  - Code to show what type of foliation: Bedding, S1 etc. (str) {'sf'}
  - Code to say this unit is overturned (str) {'bo'}

**5.5 Mineral Deposits: (Optional, can use default data from Notebook 3)**

- single points (no multipoints)

Attributes:
  - Site Code (str) {'msc'}
  - Name of deposit (str) {'msn'}
  - Type of feature: open pit, occurence, abandoned etc., (str) {'mst'}
  - Code to show what main commodity: Fe, Iron, etc. (str) {'mtc'}
  - Code to show what main commodity class: Industrial, Metal, etc. (str) {'mcom'}
  
**5.6 Fold Axial Trace Polylines: (Optional)**

- single polyline per trace (no multipolylines)

Attributes:
  - Text that identifies polyline as a fold axial trace (str) {'feature'}
  - Code that defines fold as syncline (str) {'syn'}
