# Restaurants-search-using-Google-Maps-and-Yelp-API
Web application for the restaurant search sorted as per an individual’s choice of cuisine, distance, reviews, ratings, and among others; displaying the result on an interactive map. 

Authors: Chandan Singh, Akshay Mane 
    
Youtube Link: https://youtu.be/B_7Urs_hyJ8

### Aim:

To find the top restaurants between any two locations across the US. 

### Motivation:

Finding a good place to eat is always a challenge especially when we travel to a new city. This app will help us resolve this issue. Consider you’re planning a long road trip, and you would like to know what are the restaurants along the way, which are best suited as per your budget, distance from where you are, and the positive reviews of the place. There are multiple apps that provide you the details of restaurants nearby and whether or not it is best suited for you. Our project is fundamentally based on the purpose of finding the best restaurant for an individual who is planning a long or short trip and would like to find out the best place to dine. 

### References:

https://gist.github.com/jeromer/2005586

https://medium.com/@bobhaffner/folium-lines-with-arrows-25a0fe88e4e


### Getting an API:

1. Google Maps API - (https://developers.google.com/maps/documentation/embed/get-api-key)


2. Yelp API - 

Step 1: Register with a Yelp user account.

Step 2: Once you have the Yelp account, go to Manage App and create an app with Yelp. Creating an app will provide you the “Client ID” and “API Key” which you can use to call their API. 
For more information on how to use Yelp API, you can visit here: https://www.yelp.com/developers/faq


### Packages to be installed:

1. folium - To create several types of interactive maps
2. geographiclib - For midpoints coordinates

### How to Install the aforementioned packages:

These packages need to be installed from the terminal window as follows:

pip install folium

pip install geographiclib

### Libraries to be imported:

urlibrequest - Helps in opening URL (mostly HTTP) Ref: https://docs.python.org/3.0/library/urllib.request.html

json - The output/data we obtain from API is in json format and we need the library to view it

pandas - To perform dataframe operations

numpy - To perform 

json_normalize - To convert the json output in a readable format

math - to perform mathematics operations 

requests - alternative for urlib to view the documentation in a clear format

### Working:

The working of our project is divided into 4 categories:
1. Google API
2. Co-ordinates of the Mid-point
3. Yelp API
4. Mapping	


### 1. Google API:

1. To begin with the project, the first thing we required was to know what's the start and end point. To get the exact location, we decided to obtain the coordinates. For this activity, we used Google Maps API. 
2. The required parameters are "origin", "destination", and "API key". The optional parameters are mode like driving or walking and other, arrival time, departure time and others. 
3. We were only interested in obtaining the latitude and longitude of the origin and destination, so we did not provide any optional parameters in the code. 
4. The output we obtained from the API gives lot of details. The list "routes" contains dictionary with multiple keys,of which we are only interested in keys: "start_location" and "end_location". The "start_location" is a key again, which has a value "lat" and "long" meaning latitude and longitude of the origin point. Similarly, "end_location" has a value "lat" and "long".

Reference: https://developers.google.com/maps/documentation/directions/intro?authuser=1


### 2. Co-ordinates of the Mid-point

After we obtain the latitude and longitude of the surce and destination, we find the coordinates of the mid-distance. For this, we use the library geographiclib, specifically "Geodesic" from it. We computed the coordinates and rounded it to 7 digits after the decimal.

### 3. Yelp API:

1. To look for restaurants, we consider Yelp's API, which provides rich data of restsurants with menus, reviews, ratings and others given the location. 
2. We used the Business search option under Business Endpoints to pull the details of restaurants near the source, destination and mid-distance. 
3. The required parameter is either location or latitude and longitude of the location we want to look the data for. Since we already obtained the coordinates, we can use it here and extraxt the list of restaurants under 25,000 meters of it. 
4. The optional parameters we used in our code is term, which is the business that we are looking for. In our case, it is restaurant; radius - in meters around the coordinates; limit - number of business results to return; offset - offset the list of returned business results by this amount; sort_by - Sort the result by one of the methods: best_match, rating, review_count or distance. In our case, we are sorting the result by distance. 

Reference - https://www.yelp.com/developers/documentation/v3/business_search


### 4. Mapping:

1. To plot the restaurants on the map, we used the 'folium' library.
2. The map shows the restaurants around the source, mid-point, and destination coordinates. The restaurants are distinguished as per the rating, which could be demonstrated in green, orange, and red colors. The green color indicates the rating above 4, the orange color indicates the rating between 2 and 4, and red color indicates the rating below 2. 

### How to Run the Code:

The code can be run on Jupyter Notebook. 

Select the cell and run the code, which will ask you for the source and destination.

Entering the source and destination will provide you the latitude and longitude of source and destination. Moreover, you can view the coordinates of the midpoint, and lastly the map. 

### Results:

The plot shows the restaurant near the city of Buffalo

![buffalo.PNG](attachment:buffalo.PNG)

The plot shows the line drawn between Minneapolis and Tampa with restaurants located at the source, mid-point, and desitnation.

![Minneapolis_tampa.PNG](attachment:Minneapolis_tampa.PNG)

The plot shows the distance between Oregon and Cleveland, with midpoint showing no restaurants around it.

![oregon_cleveland.PNG](attachment:oregon_cleveland.PNG)

The pop-up gives the restaurant's name, address, and distance from the source point.

![syracuse%20pop%20up.PNG](attachment:syracuse%20pop%20up.PNG)

### Limitations/Future Work: 

1.	We have only considered the option of restaurant, but our project can be used as a framework to find any places for grocery, hospital, sports club or a movie theatre and several other places as per their suited requirements while on a journey. 

2.	The results obtained from the API returned the dining place which aren’t widely spread or in a pattern that would cover the whole journey. That was one of the reasons we decided to include the mid-point coordinates to demonstrate the restaurants along the way. Further work can involve points at 1/4th and 3/4th of the total distance to include more restaurants result to provide more options for an individual.

3.	We found out that, Google Maps API gives us each and every direction to our route starting from our source to our destination. The results which we initially got gave us the data in json format, but due to time constraints, we thought of avoiding it. If we would implement this, then our result would show each and every restaurant on our route as well map the route based on the roads as compared to straight lines drawn currently. 

4.	The mid-point marker on the map, is not the exact middle point. There are 2 reasons for this:
a)	Library ‘Geodesic’ gives us the latitude and longitude in eleptical form
b)	The midpoint formula which we have used, considers earth as a flat surface, and plots the line considering it as a single plane, hence there is a variation between actual midpoint from source – destination and the one we have plotted. 

5.	Sometimes, we do not get any hotels in the midpoint because, of the following reasons
a)	Data for certain region not provided in the API
b)	Wrong coordinates given in the database
c)	Sometimes mid-point comes in the middle of the ocean, so obviously there aren’t any hotels around it.

