Read the final assignment instructions from the [https://autogis.github.io](https://automating-gis-processes.github.io/2018/lessons/FA/final-assignment.html).

# Multi-Stop Route Optimizer Tool
## Introduction
This final assignment aims to solve a very practical problem that almost everyone is likely to face at some point of their lives. For example, a group of friends is willing to visit each other's homes during one evening (but are uncertain about the optimal sequence) or perhaps you just want to know the fastest route to sequentially visit home, a grocery store, a post office and a library... 

This program can be used to solve multi-stop route optimization problem by minimizing total travel time of itineraries. The implementation is a command line interface/tool that will read all necessary user inputs (such as addresses of the stops) from keyboard. Travel times are extracted either from [Helsinki Region Travel Time Matrix 2018](https://blogs.helsinki.fi/accessibility/helsinki-region-travel-time-matrix-2018/) or [Digitransit Routing API](https://digitransit.fi/en/developers/apis/1-routing-api/). 

## Usage
First, the program geocodes user defined locations by using [Digitransit Geocoding API](https://digitransit.fi/en/developers/apis/2-geocoding-api/). Geocoded locations are saved as a shapefile and can be imported to the program on a later run (instead of geocoding new locations). After user has accepted the geocoding results, the program proceeds to find all possible combinations (permutations) of stops. Subsequently, total travel times of all stop-combinations are extracted and combined from either the [travel time matrix](https://blogs.helsinki.fi/accessibility/helsinki-region-travel-time-matrix-2018/) or [Digitransit Routing API](https://digitransit.fi/en/developers/apis/1-routing-api/). Optionally, user can define fixed origin and/or destination. Finally, best routes are selected and printed. 

[See some example runs from here.](demo/route-optim-outputs.md)

## Installation
Set up the python environment with the following commands:
```
$ conda create -n geoenv -c conda-forge python=3.6.5 jupyterlab geopandas geoplot pysal
$ pip install pycrs
$ pip install requests
$ pip install polyline
```
Add the [travel time matrix](https://blogs.helsinki.fi/accessibility/helsinki-region-travel-time-matrix-2018/)
 to the path `/data/HelsinkiTravelTimeMatrix2018`

## Starting the program
```
$ git clone git@github.com:AutoGIS-2018/final-assignment-hellej.git
$ conda activate geoenv
$ cd final-assignment-hellej
$ python route_planner_app.py
```

## Components
``` 
  ├── data
  │   ├── HelsinkiTravelTimeMatrix2018/ */ *.txt     
  │   └── MetropAccessGrid/ *.shp
  ├── demo
  │   ├── dt_geocode.py             # Jupyter notebook like script file to run with VSCode
  │   ├── dt_routing.py             # Jupyter notebook like script file to run with VSCode
  │   ├── optimize_route.py         # Jupyter notebook like script file to run with VSCode
  │   └── route-optim-outputs.md    # Outputs of example runs
  ├── input
  │   └── *.shp                     # Optional locations to use in multi-stop route optimization
  ├── utils                         # Utils-module
  │   ├── dt_geocode.py             # Utilization of Digitransit Geocoding API
  │   ├── dt_routing.py             # Utilization of Digitransit Routing API
  │   ├── routes_tt.py              # Forming and comparing multi-stop route options
  │   ├── travel_times.py           # Collecting travel times from travel time matrixes or Digitransit API
  │   └── utils.py                  # General utilities
  │── demo_geocoding.ipynb
  │── demo_route_optim.ipynb
  └── route_planner_app.py          # Main application (run this in terminal)
```

## License
[MIT](LICENSE)
