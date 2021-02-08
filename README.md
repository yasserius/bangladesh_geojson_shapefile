# GeoJSON Shapefiles of Bangladesh - Division, District/Zilla, Upozilla, Thana/Union

<img src="https://raw.githubusercontent.com/yasserius/bangladesh_geojson_shapefile/main/bangladesh_shapefiles_geojson.png" height=400px>

GeoJSON or SHP shapefile - Boundary / Outline shapes of Bangladesh Divisions (বিভাগ), Districts / Zila / Jela (জেলা), Upazila / Upojela (উপজেলা), Unions / Thanas (থানা)

# Download
Shapefiles in SHP format: [[humdata.org]](https://data.humdata.org/dataset/administrative-boundaries-of-bangladesh-as-of-2015) (Original Source)

Shapefiles in GeoJSON format: [[Google Drive]](https://drive.google.com/drive/folders/1qRUvObNAQRsuwt3-PtViBJsmIKOKJWD0?usp=sharing) (Converted)

# Contents

**Note:**

- adm = Administration Regions
- adm0 = Entire Bangladesh
- adm1 = 8 Divisions
- adm2 = 64 Districts/Zilas
- adm3 = 492 Upazilas
- adm4 = 5160 Thanas/Unions

**GeoJSON files:**
- `bangladesh_geojson_adm0_whole_bangladesh_outline.json`
- `bangladesh_geojson_adm1_8_divisions_bibhags.json`
- `bangladesh_geojson_adm2_64_districts_zillas.json`
- `bangladesh_geojson_adm3_492_upozila.json`
- `bangladesh_geojson_adm4_5160_unions_thanas.json`
- `bangladesh_geojson_admALL_2_entire_bd_division_district_unions.json`
- `bangladesh_geojson_admALL_entire_bd_division_district_unions.json`

Inside `small` folder (smaller file size):

- `small_bangladesh_geojson_adm0_whole_bangladesh_outline.json`
- `small_bangladesh_geojson_adm1_8_divisions_bibhags.json`
- `small_bangladesh_geojson_adm2_64_districts_zillas.json`
- `small_bangladesh_geojson_adm3_492_upozila.json`
- `small_bangladesh_geojson_adm4_5160_unions_thanas.json`


# How to open GeoJSON / SHP files with Python
- [Plotting Choropleth Maps using Python (Plotly)](https://www.youtube.com/watch?v=aJmaw3QKMvk)
- [Shapefiles in Python: a super basic tutorial](https://chrishavlin.com/2016/11/16/shapefiles-tutorial/)

# How to convert from SHP to GeoJSON (using ogr)
Source of converter function: [medium.com](https://medium.com/tech-carnot/interactive-map-based-visualization-using-plotly-44e8ad419b97) <br>
Link to OGR: [link](https://mothergeo-py.readthedocs.io/en/latest/development/how-to/gdal-ubuntu-pkg.html)
``` python
# Python >= 3.7
import ogr
import json

def shp2json(shp_path):
  """
  Convert SHP files to GeoJSON with OGR.
  Outputs JSON file to same directory as the SHP files.
  
  Input:
    - shp_path (str):
        e.g. "D:/somewhere/bangladesh.shp"
  """
  driver = ogr.GetDriverByName('ESRI Shapefile')
  data_source = driver.Open(shp_path, 0)

  fc = {
      'type': 'FeatureCollection',
      'features': []
      }

  lyr = data_source.GetLayer(0)
  for feature in lyr:    
      fc['features'].append(feature.ExportToJson(as_object=True))

  output_name = shp_path.split(".")[0] + ".json"

  with open(output_name, 'w') as f:
      json.dump(fc, f)
      print("GeoJSON file created: {}".format(output_name))
```
*You can also do it with libraries like geopandas.*
