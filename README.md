# Welcome to my Project "The Battle of the Neighborhoods"

## Introduction/Business Problem

Many people constantly seek new job opportunities within the same community they live in or across the city or even a different city itself. Let's say a person got an interesting job offer from a different city, say New York and he/she lives in Downtown Toronto currently. It would be really helpful to seek a place to live which is most similar to the current living location of that person.
Some of the popular location categories one might look for in the proximity of a living area are grocery stores, colleges or/and schools, parks, restaurants, coffee shops, hospitals, and other community areas like religious places, community halls, libraries, etc. So I’ll find out what are borough-neighborhoods that are very similar to a person's current location.

This information can help the person decide on which neighborhood he/she would love to live in once he/she moves to New York after accepting a new job offer.

### Similarity
How do we compare 2 cities and measure similarity? Fortunately, Foursquare offers venue category to each venue, this information can be used to count the number of venues for each category and compare it with all neighborhoods of New York.

## Data Wrangling

### New York
All the venues of New York City are available in a dataset provided by [PLUTO](https://www1.nyc.gov/site/planning/data-maps/open-data/dwn-pluto-mappluto.page) which is a part of the Department of City Planning (DCP). It contains Borough, Latitude, Longitude for each venue in New York City. Using [Foursquare API](https://foursquare.com/), we can get Neighborhood information for each venue in the dataset. Another way to get the New york city dataset is from Foursquare API with getting latitude and longitude of the center of New York City and getting all venues within a 500-mile radius and filtering out all venues with New York City as city name for the venue.

### Toronto Data
A similar exercise can be done to get all venues in Toronto by Foursquare API or as we did in the previous exercise, download the Toronto Zip Codes from Wikipedia, parse the Wikipedia webpage using [BeautifulSoup](https://pypi.org/project/beautifulsoup4/) package. Using the geolocator or the CSV file provided by the assignment, we can get latitude and longitude for the neighborhoods and iterate through the Foursquare API to get all venues in each neighborhood.

Below steps will be followed to clean the data from cities datasets

- Only process the cells that have an assigned borough. Ignore cells with a borough that is Not assigned.
- More than one neighborhood can exist in one postal code area. Split the neighborhoods as one per line.
- If a cell has a borough but a Not assigned neighborhood, then the neighborhood will be the same as the borough.

## Methodology
let's group each neighborhood and by taking the sum and maximum of the frequency of occurrence of each category. If the current neighborhood is in Toronto,  if a similar neighborhood needs to be found in New York, we need to consider all the similar venue categories to the selected borough of New York and Toronto before grouping and discard all the dissimilar venue categories in both cities datasets.

![venn diagram](https://github.com/shylajachippa/Coursera-IBM-Applied-Data-Science-Capstone/blob/main/venn_diagram_new_ork_toronto.png)


### Matrix Multiplication
This approach will be used to amplify similar venue categories and discard dissimilar venue categories when comparing 2 neighborhoods
For our problem, we need to find NY neighborhoods with maximum matching categories with a given neighborhood in Toronto and discard dissimilar venue categories

Steps to get matching locations

1. isolate columns from dataframes to get common venue categories columns
2. multiply given index of Toronto with the transpose of New York dataframe data values
3. sort the dot product of matrices to get the most matched
4. save the matching locations into a dataframe

## Results
![matching locations](https://github.com/shylajachippa/Coursera-IBM-Applied-Data-Science-Capstone/blob/main/matching_locations.png)

## Observations
The following observations are being made after analyzing the data above.

New York has double in venue categories than Toronto.
There are more Boroughs in Toronto than in New York but there are more neighborhoods in New York than Toronto.
The matched locations observations are as follows:

#### Manhattan,Murray Hill

- This location matches 9/10 most frequent venues in comparison to Toronto.
- Park is missing in this location but this neighborhood is the best match of all the matched locations.
- 11 venues that are missing in this location - Park,Performing Arts Venue,Mexican Restaurant,Historic Site,French Restaurant,Farmers Market,Antique Shop,Electronics - - Store,Chocolate Shop,Beer Store,Art Gallery

#### Queens,Murray Hill

- This location matches 9/10 most frequent venues in comparison to Toronto.
- Park is also missing in this location.
- 11 venues that are missing in this location - Park,Performing Arts Venue,Mexican Restaurant,Historic Site,French Restaurant,Farmers Market,Antique Shop,Electronics Store,Chocolate Shop,Beer Store,Art Gallery

#### Brooklyn, Boerum Hill

- This location matches 8/10 most frequent venues in comparison to Toronto.
- It has Park but no Pub and no Breakfast Spot. Although the Breakfast spot is absent, there are Cafés and Restaurants and Coffee Shops in the area.
- 11 venues that are missing in this location - Pub,Breakfast Spot,Shoe Store,Restaurant,Hotel,Event Space,Farmers Market,Dessert Shop,Chocolate Shop,Beer Store,Art Gallery

#### Manhattan,Flatiron

- This location matches 7/10 most frequent venues in comparison to Toronto.
- It has Park but no Theater no Pub and no Breakfast Spot. Although the Breakfast spot is absent, there are Cafés and Restaurants and Coffee Shops in the area. Pub and Theater are in the adjacent neighborhoods and comparatively New York neighborhoods are much closer compared to Toronto.
- 13 venues that are missing in this location - Pub,Theater,Breakfast Spot,Shoe Store,Restaurant,Performing Arts Venue,Historic Site,Event Space,French Restaurant,Antique Shop,Beer Store,Bank,Asian Restaurant

#### Manhattan,Sutton Place

- This location matches 7/10 most frequent venues in comparison to Toronto.
- It doesn't have Café,Theater or Breakfast Spot. Although the Breakfast spot is absent, there are Cafés and Restaurants and Coffee Shops in the area. Theater is in adjacent neighborhoods.
- 13 venues that are missing in this location - Theater,Breakfast Spot,Café,Shoe Store,Performing Arts Venue,Mexican Restaurant,Historic Site,Event Space,Farmers Market,Antique Shop,Electronics Store,Chocolate Shop,Art Gallery

## Conclusion
In this report, I analyzed the relationship between neighborhoods and their venue categories in different cities New York and Toronto. I identified the latitude and longitude from different data sources and used Foursquare to retrieve all venues in the locations, using this information, I could list the most frequent locations for each neighborhood. This gave some idea on neighborhood characteristics that will be helpful to choose a location in New York, given the person is currently residing in Toronto. The Matrix multiplication methodology used eliminates dissimilar venues and multiplies similar categories giving it a comparative advantage over other methodologies. For example, according to the example used above, if a person is currently living in HarbourFront, Downtown Toronto, the best place to choose is Murray Hill, Manhattan in New York since it matches most venue categories with HarbourFront, Downtown Toronto according to the graph above.

P.S : This project and course have allowed me to learn interesting Data Science concepts and apply them through various projects that intrigued my learned knowledge and encouraged me to dive deeper into Data Science. 
<hr>

# Repository Materials
If you are interested in my project during the course, read further


This repository contains jupyter notebooks and reports material for this course, the course agenda is detailed below.

## Week 1 - Introduction to Capstone Project

[Peer-review Assignment: Capstone Project Notebook](https://github.com/shylajachippa/IBM_Applied_Data_Science_Capstone/blob/main/Capstone%20Project.ipynb)

<p><i>In this assignment, you will be asked to create a new repository on your Github account, and to create a Jupyter Notebook and submit a shareable link to it for peer evaluation.</i></p>

## Week 2 - Foursquare API
<p><i>In this lab, you will learn in detail how to make calls to the Foursquare API for different purposes. You will learn how to construct a URL to send a request to the API to search for a specific type of venue, to explore a particular venue, to explore a Foursquare user, to explore a geographical location, and to get trending venues around a location. Also, you will learn how to use the visualization library, Folium, to visualize the results.</i></p>

## Week 3 - Neighborhood Segmentation and Clustering

[Peer-review Assignment: Segmenting and Clustering Neighborhoods in Toronto](https://github.com/shylajachippa/IBM_Applied_Data_Science_Capstone/blob/main/Neighborhoods%20Toronto%20K-means%20clustering%20Assignment.ipynb)

<p><i>In this assignment, you will be required to explore, segment, and cluster the neighborhoods in the city of Toronto. However, unlike New York, the neighborhood data is not readily available on the internet. What is interesting about the field of data science is that each project can be challenging in its unique way, so you need to learn to be agile and refine the skill to learn new libraries and tools quickly depending on the project.

For the Toronto neighborhood data, a Wikipedia page exists that has all the information we need to explore and cluster the neighborhoods in Toronto. You will be required to scrape the Wikipedia page and wrangle the data, clean it, and then read it into a pandas dataframe so that it is in a structured format like the New York dataset.

Once the data is in a structured format, you can replicate the analysis that we did to the New York City dataset to explore and cluster the neighborhoods in the city of Toronto.

Your submission will be a link to your Jupyter Notebook on your Github repository.</i></p>

## Week 4 - Capstone Project

Peer-graded Assignment: Capstone Project - The Battle of Neighborhoods (Week 1)

<p><i>Now that you have been equipped with the skills and the tools to use location data to explore a geographical location, over two weeks, you will have the opportunity to be as creative as you want and come up with an idea to leverage the Foursquare location data to explore or compare neighborhoods or cities of your choice or to come up with a problem that you can use the Foursquare location data to solve. If you cannot think of an idea or a problem, here are some ideas to get you started:

In Module 3, we explored New York City and the city of Toronto and segmented and clustered their neighborhoods. Both cities are very diverse and are the financial capitals of their respective countries. One interesting idea would be to compare the neighborhoods of the two cities and determine how similar or dissimilar they are. Is New York City more like Toronto or Paris or some other multicultural city? I will leave it to you to refine this idea. In a city of your choice, if someone is looking to open a restaurant, where would you recommend that they open it? Similarly, if a contractor is trying to start their own business, where would you recommend that they set up their office? These are just a couple of many ideas and problems that can be solved using location data in addition to other datasets. No matter what you decide to do, make sure to provide sufficient justification of why you think what you want to do or solve is important and why would a client or a group of people be interested in your project.</i></p>

## Week 5 - Capstone Project (Cont'd)

Peer-graded Assignment: Capstone Project - The Battle of Neighborhoods (Week 2)

<p><i>In this week, you will continue working on your capstone project. Please remember by the end of this week, you will need to submit the following:

1. A full report consisting of all of the following components (15 marks): Introduction where you discuss the business problem and who would be interested in this project. Data where you describe the data that will be used to solve the problem and the source of the data. The methodology section represents the main component of the report where you discuss and describe any exploratory data analysis that you did, any inferential statistical testing that you performed if any, and what machine learnings were used and why. Results section where you discuss the results. Discussion section where you discuss any observations you noted and any recommendations you can make based on the results. Conclusion section where you conclude the report.

2. A link to your Notebook on your Github repository pushed showing your code.

3. Your choice of a presentation or blogpost.</i></p>


