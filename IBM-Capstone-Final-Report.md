# Finding Rare Points of Interest in Toronto
### Final Report of the IBM Coursera Data Science Capstone Project 
 
<br /> 

## Introduction

Tourists looking for travel guides will most likely look for information from location data or map service providers such as Foursquare, Google Maps, etc. These data providers leverage inputs of thousands of users to build a dataset of the most popular areas around the world. The default information provided on popular places will be useful for most travelers, but for tourists looking for unique places, this information might not be enough for ordinary travel plans; these travelers would most likely search for unique places and may not be satisfied with the default location search results. This project aims to propose high-quality venues that are unique or unusual so that travelers may have a more interesting or varied stay for a particular city.

The project will be limited to the Toronto area only, and will be most useful to tourists looking for unique places to visit, or even Toronto residents who want to find quirky new places in their city. This project will leverage the sample IBM lab exercises for extracting and cleaning the location data of Toronto, and will provide some exploratory data analysis, as well as recommendations for unique venues to visit in Toronto.

## Data
The data for this project will come from the following sources:
* **Wikipedia**  - An HTML page of Toronto postal codes used during the IBM Applied Data Science Capstone week 3 assignment. This data can be accesed here: (https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M)
* **IBM** - A CSV file with Toronto postal codes, and coordinates (longitude and latitude), also used during the the week 3 assignment. The CSV file can be accessed here:  (http://cocl.us/Geospatial_data)
* **Foursquare** - JSON files from different Venues API endpoints using a Foursquare developer account. The different endpoints are described in the Developer documentation here: (https://developer.foursquare.com/docs/places-api/endpoints/). The following are the specific endpoints to be used:
  * Explore endpoint - A JSON file with venue names, their venue IDs and categories.
  * Likes endpoint - A JSON file with the number of likes per venue.
  * Lists endpoint - A JSON file with the number of lists a venue is in.
  * Photos endpoint - A JSON file with a link to the a venue's photo.
  * Tips endpoint - A JSON file with a user's description of a venue.

The data will be retrieved by modifying the functions provided in the example lab exercise in week 3, and then cleaned and processed so that the end result will have the following columns:
* **Venue ID** - a string which is the unique identifier for each venue
* **Venue name** - a string which is the venue's common name
* **Categories** - a list of strings of the different categories that describes the venue
* **Likes** - an integer that represents the number of likes the venue has
* **Lists** - an integer that represents the number of lists that contains the venue
* **Tip** - a string which describes the venue
* **Image URL** - a string of the image's URL

The above data will then be used to find correlations between the likes and lists, as well as find the rankings of the categories, with the aim of finding venues with high likes or high list-counts, but in categories with few venues. The end result should have highly liked or listed venues that are in rare or unusual categories, which will then be used to build a list of highly rated but rarely discussed venues.

## Methodology

The data was first extracted using functions based on the example lab exercise in week 3. Additional functions were created to extract the likes, lists, photo URL, and tips for each venue.

Pearson's correlation was then applied on likes and lists to check if a combination of both could be used to query unique venues later on. A regression line was also created based on these fields.

The dataframe was then queried to find the least popular categories. A view of this dataframe was then saved, and only the venues with the most number of likes were saved to the Top 10 Venues dataframe. A photo and tip was also then extracted from Foursquare to come up with a final list of top 10 unique venues in Toronto.

## Results

The data was extracted from the different sources, cleaned and appended with the different likes, lists, and tips data to arrive at the dataframe below:
![Final Dataframe](https://github.com/josh-arrabaca/Coursera_Capstone/blob/main/Final%20Table.jpg?raw=True)

The Pearson's correlation applied on the venues' likes and list count showed an R value of 0.68 which is a moderate correlation. Likes and list count are therefore moderately interdependent, and the regression line showed that the list count can be extrapolated from a venue's number of likes. However, since the correlation is only moderate, and since we cannot determine which is the independent value, only the likes will be used for querying unique venues (instead of the original plan of using both likes and list count). Below is the regression plot:
![Final Dataframe](https://github.com/josh-arrabaca/Coursera_Capstone/blob/main/regression_line.png?raw=True)

When sorting through the dataframe's categories, it was discovered that there were already 70 categories with only one venue. This dataframe view would be the basis for finding the unique venues. The 70 rows were queried to find the venues with the highest number of likes. The sorted rows would form the top 10 unique venues.

The results showed that the most popular venue among the most unique venues is Billy Bishop Toronto City Airport (YTZ) (Billy Bishop Toronto City Airport) with 751 number of likes, and the least popular venue among the most unique venues is Lamport Stadium with 57 number of likes. Below are the top 10 venues, their unique category, and likes:

**Index**	| **Venue** | 	**Unique Category**|	**Likes**
--- | --- | --- | ---
0	|Billy Bishop Toronto City Airport (YTZ)|	Airport	|751
1	|The Distillery Historic District	|Historic Site	|545
2	|RS - Real Sports	|Sports Bar	|531
3	|SOMA chocolatemaker	|Chocolate Shop	|180
4	|Sugar Beach	|Beach	|153
5	|The County General	|Southern / Soul Food Restaurant	|124
6	|Otto's Berlin Döner	|Doner Restaurant	|121
7	|Dim Sum King Seafood Restaurant	|Dim Sum Restaurant	|96
8	|Athletic Centre	|College Gym	|62
9	|Lamport Stadium	|Stadium	|57

The venue images are shown in the presentation linked in appendix section at the end of this document.

# Discussion
The results showed a moderate correlation between a venue's number of likes and its list count. However, since the correlation is not very strong, and we cannot determine which of these variables is the independent variable, only the likes count was used for determining the top unique venues. 

For the unique categories, it was discovered that some of the categories with only 1 venue are actually variants of other popular venues. For example, "Dim Sum Restaurant" AND "Doner Restaurant" could be cleaned up to be included in category "Restaurant". Another example is "Historic Site" which could be included as "Tourist Spot". In addition, some more interesting variables or statistics could be used with Foursquare's "stats" endpoint (which requires an Oauth user token).
Nevertheless, the resulting list is unique enough to satisfy the goal of this project.

# Conclusion
The aim of this project was to provide a list of unique venues out of the hundreds of venues in Toronto. The project used the Foursquare API extensively, and used some machine learning algorithms to find the best variables for determining the uniqueness of a venue. In the end, the project mostly required some data wrangling with Pandas to extract only those highly-rated venues in categories with only one venue each. The result is an eclectic list of venues including an airport, chocolate shop, and even a beach. 

The resulting list can be enhanced further with some more text cleaning as well as the use of Foursquare's stats API for future projects.

# Appendix
* [Jupyter Notebook](https://github.com/josh-arrabaca/Coursera_Capstone/blob/main/IBM%20Data%20Science%20Capstone%20Project%20Week%204%265.ipynb)
* [Presentation Slides](https://github.com/josh-arrabaca/Coursera_Capstone/blob/main/Rare%20Places%20in%20Toronto.pdf)
