# PlateTectonics

    #!pip install -U googlemaps
    #!pip install "gmplot"
    import gmplot
    from gmplot import *
    import pandas as pd
    import pylab
    import matplotlib as plt
    import matplotlib.pyplot as plt

    df=pd.read_csv('query.csv')

    mag = df.mag
    lat = df.latitude
    long = df.longitude
    time = df.time

    plt.figure(1)
    plt.figure(1).set_figheight(10)
    plt.figure(1).set_figwidth(30)
    plt.scatter(time,mag)
    plt.title('time vs magnitude')
    plt.xlabel('time')
    plt.ylabel('magnitude of earthquake')

  ![Fig 1](https://github.com/TheAvidArtist/PlateTectonics/blob/master/GoodNuffForNow.png)
