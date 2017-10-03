# Uber-Trips-Data-qgis-import
# Using trips.json data provided by uber to convert it into geojson for qgis import and analyze the data for quick visualization.
# Tools used : Jupyter, qgis

# Python Code

# Import all the required libraries
import pandas as pd 
import numpy as np
from shapely.geometry import LineString
import geojson

# Read data
df = pd.read_json("trip.json")

# Convert json to linestring
segments_ls = []
for i in range(len(df.segments)):
    seg = df.segments[i]
    coords = []
    for j in range(len(seg)):
        (long, lat, timestamp) = seg[j]
        coords.append((long, lat))
    linestring = LineString(coords)
    segments_ls.append(str(linestring))
    

# Exporting data to csv fromat.
df2 = pd.DataFrame(segments_ls, columns=['segments'])
df2.to_csv('trips.csv')
