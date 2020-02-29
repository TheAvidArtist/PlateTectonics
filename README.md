# PlateTectonics

## Installations
    #conda install -c pyviz holoviews geoviews datashader
    #!pip install -U googlemaps
    #!pip install "gmplot"
    #!pip install folium
    #conda update -n base -c defaults conda
    #pip install pygmaps-0.1.1.tar.gz
    #conda install basemap
    #conda install -c pyviz geoviews
    
## Imports
    import csv
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    import zlib
    import datetime
    import glob
    import math
    import mpl_toolkits
    import dateutil.parser
    import gmplot
    from gmplot import *
    import pandas as pd
    import pylab
    import matplotlib
    import pygmaps as pygmaps
    import geopandas as gpd
    from bokeh.models import HoverTool
    from bokeh.io import output_notebook
    output_notebook()
    pd.set_option('display.max_columns', 100)
    from holoviews.operation.datashader import datashade
    import geoviews as gv
    import geoviews.feature as gf
    import geoviews.tile_sources as gvts
    from geoviews import dim, opts
    import xarray as xr
    import cartopy.crs as ccrs
    from cartopy import crs
    from colorcet import fire
    import os
    os.environ['PROJLIB'] = r'C:\ProgramData\Anaconda3\pkgs\proj4-5.2.0-hfa6e2cd1001\Library\share'

    gv.extension('bokeh', 'matplotlib')

## Graphing Time vs Magnitude of Earthquakes

    Data=pd.read_csv('query.csv')

    mag = []
    lat = []
    long = []
    time = []

    for i in range (0, len(Data)):
        time.append(dateutil.parser.isoparse(Data['time'][i]))
        lat.append(Data['latitude'][i])
        long.append(Data['longitude'][i])
        mag.append(Data['mag'][i])
    
    dates = matplotlib.dates.date2num(time)
    plt.figure(1)
    plt.plot_date(dates, mag)
    plt.figure(1).set_figheight(10)
    plt.figure(1).set_figwidth(30)
    plt.scatter(time,mag)
    plt.title('time vs magnitude')
    plt.xlabel('time')
    plt.ylabel('magnitude of earthquake')
    print(dates)

  ![Fig 1](https://github.com/TheAvidArtist/PlateTectonics/blob/master/Better.png)

 ## Google Maps
 
    gmap4 = gmplot.GoogleMapPlotter(47.990873, -127.843849, 5 )
    gmap4.apikey = "AIzaSyDeRNMnZ__VnQDiATiuz4kPjF_c9r1kWe8"
    gmap4.heatmap(lat, long)
    gmap4.draw( "C:\\Users\\Administrator\\Desktop\\HeatMap.html" )
    
## Mapping Points

    Cords = gv.Points(Data, ['longitude', 'latitude'])

    (Data.longitude.min(), Data.longitude.max(),
             Data.latitude.min(), Data.latitude.max())


    tooltips = [('time', '@time'),
                ('mag', '@mag'),
                ('Longitude', 'longitude'),
                ('Latitude', 'latitude'),
                ]
    hover = HoverTool(tooltips=tooltips)

    Earthquakes = (gvts.ESRI * Cords).opts(
        opts.Points(width=1000, height=1000, alpha=0.3,
                    color='red', hover_line_color='black',  
                    line_color='black', xaxis=None, yaxis=None,
                    tools=[hover],size=np.sqrt(dim('mag'))*10,
                    hover_fill_color=None, hover_fill_alpha=0.5))
                    
    Mapplot = (gvts.ESRI * Cords).opts(
        opts.Points(width=1200, height=700, alpha=0.3, color=('yellow'), hover_line_color='black',
                    xaxis=None, yaxis=None, tools=['hover'],
                    size=np.sqrt(dim('magnitude'))*10))
    gvts.ESRI.options(width=1200, height=700) * Cords
