# Final Assignment

### Status

Once you are finished with the final assignment, edit this readme and add "x" to the correct box:

* [x] Submitted

* [ ] I'm still working on my final assignment. 


### Instructions

*you can remote these instructions for the final submission*

Read the final assignment instructions from the course webpages [https://autogis-site.readthedocs.io](https://autogis-site.readthedocs.io/en/latest/lessons/FA/final-assignment.html). Remember to write readable code, and to provide adequate documentation using inline comments and markdown. Organize all your code(s) / notebook(s) into this repository and **add links to all relevant files to this `README.md`file**. In sum, anyone who downloads this repository should be able to **read your code and documentation** and understand what is going on, and **run your code** in order to reproduce the same results! :) 

**Modify this readme so that anyone reading it gets a quick overview of your final work topic, and finds all the necessary input data, code and results.** 

*Note: If your code requires some python packages not found in the csc notebooks environment, please mention them also in this readme and provide installation instrutions.*

*Note: Don't upload large files into GitHub! If you are using large input files, provide downloading instructions and perhaps a small sample of the data in this repository for demonstrating your workflow.*

Fill in details of your final project below. You can remove this instructions-section from the README-file if you want.

## Topic: 
Service geoparser (S-group store data and Finnish pharmacies). 

For my master's thesis: "Measuring accessibility equity - GIS-based approach for ex-post evaluation of transport systems" I used an R-package (`https://github.com/ipeaGIT/r5r`) to calculate accessibility across Finland for multiple different opportunity types for sustainable transport modes (cycling and public transport). The methodology required me to acquire location data on  different opportunity types across the whole nation of Finland. In many cases location data on different opportunity types is readily available in typical GIS supported formats. Specifically, location data on grocery stores and pharmacies is not readily available.

From the perspective of daily mobility, services like grocery stores and pharmacies are a crucial opportunity type to be able to access. Yet, up to date location data about them can be hard to acquire. For this purpose we decided to create a repository that would help provide such data. My contribution to this repository is also the final assignment for this Autogis course. Specifically the S-group parser and pharmacy parser

### Structure of this repository:
A more detailed look of my work and the scripts can be found in the `Service geoparser` repository: https://github.com/AaltoGIS/service_geoparser

From there you can find scripts to geoparse and geocode different service types across Finland. Specifically the `get_info_for_sgroup.py` and `get_info_for_pharmacies.py` are my contribution.

### Input data / packages used:

Packages (and what they are used for):
- Selenium (parsing service website data)
- Webdriver Manager (configures the browser used for webcrawling)
- Geopandas and pandas (geocoding and handling data)
- Time (used for specific parsing instances where webcrawler needs to pause to prevent e.g. dataloss)

Data is collected from service provider websites, using Selenium webdriver functionality:
- S-group stores https://www.s-kaupat.fi/myymalat
- Finnish pharmacies 'https://www.apteekki.fi/apteekkihaku.html'

### Analysis steps:
`get_info_for_sgroup.py`:
- The program inherits Selenium webcrawler functionalities that are used to parse website information.
- The program loops through each store type page from the service provider's website, appending store information to a list using Selenium functionality.
- Some invalid store data entries and unwanted information is avoided by using if statements inside the loops. Invalid entries are fixed manually, when these statements are true
- Before geocoding invalid addresses (the onces that can't be found from the Nominatim's API) are fixed by using a dictionary.
- Once each individual store entry has been collected and invalid addresses are fixed to be compatible, the address data is geocoded and saved to GeoJSON fromat on the disk using pandas and geopandas packages.

`get_info_for_pharmacies.py`:
- The program inherits Selenium webcrawler functionalities that are used to parse website information.
- The program scrolls down the service provider's website to open up all the available data entries.
- The program parses through each individual store entry, collecting information, like its name and address to a list.
- Before geocoding invalid addresses (the onces that can't be found from the Nominatim's API) are fixed by using a dictionary.
- Once each individual pharmacy entry has been collected and invalid addresses are fixed to be compatible, the address data is geocoded and saved to GeoJSON fromat on the disk using pandas and geopandas packages.

### Results:
Number of S-group grocery stores geolocated: 975

![S-group stores](https://user-images.githubusercontent.com/105248249/198872104-26011cc2-0d3d-40d5-9d32-28fdc49eedd2.png)

Number of pharmacies geolocated: 803

![pharmacies](https://user-images.githubusercontent.com/105248249/198873220-2c355c01-2e03-468d-bf7a-db37b7c9bf50.png)


Collected data can be used for multiple different analysis location based analysis. Because the stores are categorized by their type (i.e., size) they can be used to analyze e.g. service type reach or availability issues.

### References:
- Selenium: https://selenium-python.readthedocs.io/
- Nominatim debugging interface: https://nominatim.openstreetmap.org/ui/search.html
- Autogis course: https://autogis-site.readthedocs.io/en/2021/
- Geopandas: https://geopandas.org/en/stable/index.html
- Pandas: https://pandas.pydata.org/docs/index.html
- Service geoparser repository is done in collaboration with Henrikki Tenkanen
