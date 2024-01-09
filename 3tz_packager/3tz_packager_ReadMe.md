# 3tz_packager.exe
------------------
## Quick Links
[Introduction](#Introduction) <br />
[Running the executable](#Execute)  <br />
[Options](#Options)<br />
[Examples](#Examples)<br />

## Introduction <a name="Introduction"></a>

The 3tz_packager is a command line tool to package 3D tiles datasets into a 3tz file. A 3tz file can be used directly in ArcGIS Pro 3.2 or higher. You can upload a 3tz file to ArcGIS Online or ArcGIS Enterprise 11.3 or higher and publish a 3D tiles web layer.

You can package any 3D tiles dataset. ArcGIS organizes geospatial information in layers.  Only data representing integrated mesh or 3D objects can be visualized as 3D tiles layer in ArcGIS.

# Running the executable <a name="Execute"></a>

#### Open Command Prompt

1. Win+R

2. Enter __cmd__ into pop-up window

#### Run the executable

1. Specify the .exe path

  - Drag and drop the .exe into the command prompt window (absolute path)
    ```C:\Users\user\Desktop>C:\Users\user\Desktop\3tz_packager.exe```<br>
    OR

  - _cd_ into the directory that contains the .exe (relative path)
    - Use: 3tz_packager  
    ```C:\Users\user\Desktop\3tz_packager```

2. Specify the 3D tiles folder path

    - Set the name of the folder location containing the 3D tiles dataset and the name of the 3tz file.
   
  ```C:\Users\user\Desktop\3tz_packager C:\temp\3d_tiles c:\temp\MyPackage.3tz```

  This is the minumum required to use the 3tz_packager tool.<br>
  _Note:_ Existing 3tz file will be overwritten.

  ## Options <a name="Options"></a>

| Option Short | Option Long         | Action                  |
|----------------|-------------------------|-------------------|
| -nc | --no-compression | Disable compression for the output 3tz. It is recommended to always use compression for minimal file size. |
| -v | --verbose | Enable verbose output. |

## Examples <a name="Examples"></a>

```3tz_packager.exe  -v ./3d_tiles myCity.3tz```<br>
This command will output any message during packing.  The output file will be in the working directory.