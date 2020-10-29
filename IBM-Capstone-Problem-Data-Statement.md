# Finding Rare Points of Interest in Toronto
### Week 4 Assignment of the IBM Coursera Data Science Capstone Project 
 
<br /> 

## Problem Statement

Tourists looking for travel guides will most likely look for information from location data or map servince providers such as Fourquare, Google Maps, etc. These data providers leverage inputs of thousands of users to build a dataset of the most popular areas around the world. The default information provided on popular places will be useful for most travelers, but for tourists looking for unique places, this information might not be enough for ordinary travel plans; these travelers would most likely search for unique places and may not be satisfied with the default location search results. This project aims to propose high-quality venues that are unique or unusual so that travelers may have a more interesting or varied stay for a particular city.

The project will be limited to the Toronto area only, and will be most useful to tourists looking for unique places to visit, or even Toronto residents who want to find quirky new places in their city. This project will leverage the sample IBM lab exercises for extracting and cleaning the location data of Toronto, and will provide some exploratory data analysis, as well as recommendations for unique venues to visit in Toronto.

## Data
The data for this project will come from the following sources:
* **Wikipedia**  - An HTML page of Toronto postal codes used during the IBM Applied Data Science Capstone week 3 assignment. This data can be accesed here: (https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M)
* **IBM** - A CSV file with Toronto postal codes, and coordinates (longitude and latitude), also used during the the week 3 assignment. The CSV file can be accessed here:  (http://cocl.us/Geospatial_data)
* **Foursquare** - JSON files from different API endpoints using a Foursquare developer account. The different endpoints are described in the Developer documentation here: (https://developer.foursquare.com/docs/places-api/endpoints/). The following are the specific endpoints to be used:
  * Explore endpoint - A JSON file with venue names, their venue IDs and categories.
  * Likes endpoint - A JSON file with the number of likes per venue.
  * Lists endpoint - A JSON file with the number of lists a venue is in.

The data will be retrieved by modifying the functions provided in the example lab exercise in week 3, and then cleaned and processed so that the end result will have the following columns:
* **Venue ID** - a string which is the unique identifier for each venue
* **Venue name** - a string which is the venue's common name
* **Categories** - a list of strings of the different categories that describes the venue
* **Likes** - an integer that represents the number of likes the venue has
* **Lists** - an integer that represents the number of lists that contains the venue

The above data will then be used to find correlations between the likes and lists, as well as find the rankings of the categories, with the aim of finding venues with high likes or high list-counts, but in categories with few venues. The end result should have highly liked or listed venues that are in rare or unusual categories, which will then be used to build a list of highly rated but rarely discussed venues.
