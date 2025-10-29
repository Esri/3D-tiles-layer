 # ESRI_crs
Vendor extension for 3D tiles.

 ## Contributors:
 - Ronald Poirrier, Esri
 - Jean-Philippe Pons, Esri

 ## Status:
  Released

## Optional vs. Required
This extension is optional and should be placed in the tileset JSON `extensionsUsed` list, but not in the `extensionsRequired` list.

## Overview
This extension allows 3D Tiles content to be authored in a specified coordinate reference system (CRS). For example, a projected coordinate system (PCS) with an optional vertical coordinate system (VCS). The data remain compatible with 3D Tiles' Earth-centered, Earth-fixed (ECEF) reference frame continous. 3D tiles data with ESRI_crs extension supply additional transformation matrices that convert the content from its local model space to world space coordinates within the specified coordinate reference system.

### CRS declaration
`ESRI_crs`declaration must be declared in the root tileset but not in sub-tilesets.

#### Properties

| Property | Type | Description |
| --- | --- | --- |       
|wkid|number|The well-known ID for the horizontal coordinate system. The wkid is required. |
|vcsWkid|number| The vertical well-known ID for the vertical coordinate system. If not defined orthometric heights are assumed in the units of the xy coordinate system.|
|wkt|string|The ESRI well-known-text description of the coordinate system. The wkt may include the vertical coordinate system. The wkt is used for custom coordinate systems *only*.|
|wkt2	|string|The newer well-known-text description of the coordinate system defined by [Open Geospatial Consortium (OGC)](https://docs.ogc.org/as/18-005r4/18-005r4.html). The wkt2 is used for custom coordinate systems *only*.|

#### Example:
``` json
{
  "asset": {
    "version": "1.1"
  },
  "extensions": {
    "ESRI_crs": {
      "wkid": 31255,    // PCS MGI/Austria GK central
      "vcsWkid": 5778   // VCS GHA height Austria (Gebrauchshohen ADRIA)
    }
  },
  "extensionsRequired": null,
  "extensionsUsed": ["ESRI_crs"],
  // [...]
}
```

#### Well-Known Coordinate Systems
The wkid identifies the code for the horizontal coordinate system used. Optionally, a vcsWkid code may be provided to define a vertical coordinate system (VCS). Please note that if vcsWkid is omitted, elevation values must be assumed to be relative to an unspecified geoid (i.e., orthometric height). More information about Esri wkid/vcsWkid can be found [here](https://www.esri.com/arcgis-blog/products/arcgis-pro/mapping/coordinate-systems-difference#WKID).

#### Custom Coordinate Systems
The wkt or wkt2 field may be used to declare a custom CRS as a Esri wkt string or OGC wkt version 2 string, respectively. Please note that some applications may not support custom CRS definitions. In this case the wkid/vcsWkid declaration must always be used for known CRS. The wkt or wkt2 and the definition of wkid and vcsWkid are mutually exclusive.

### Model-space to CRS
`ESRI_crs` extends the tile definition to include a new set of transformations and bounding boxes. These transformations follow the same composition rules as regular 3D Tiles data to form an independent chain of transformation from model-space to CRS coordinates.

#### Properties:
| Property | Type | Description |
| --- | --- | --- |       
|boundingVolume| object| Is identical to `tile.boundingVolume` except that `region` cannot be used. |
|transform|number[16]|A 4x4 affine matrix transformation (column major) that transforms from model space to node space.|

#### Example:
```json
{ // a tile object in tileset.json
"boundingVolume": {
    "box": [...], // ECEF bounding box (ignored in CRS mode)
    "transform": [...] // ECEF transformation matrix
},
"content": {
    "uri": "0738_3490/tile_002.glb"
},
"extensions": {
    "ESRI_crs": {
    "boundingVolume": {
        "box": [...] // CRS bounding box
    },
    "transform": [...] // CRS transformation matrix
    }
},
"geometricError": 281.6
}
```

### Compatibility with ECEF CRS
While the 3D content has been created in the specified CRS, the same model-space data can be transformed to ECEF reference frame by applying the traditional chain of transformations. Positional accuracy may be reduced when transforming large tiles to ECEF instead of their native CRS, but small-scale tiles typical for high-resolution should exhibit negligible distortion.

### Limitation
The `region` bounding volumes are incompatible with `ESRI_crs`.






