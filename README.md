# ChiCrawl
Final Team Project for CMSC122 Computer Science with Applications 2

Project Goal
Yelp can provide recommendations for a specific location and Google Maps can provide directions, but if you want to visit multiple 
bars or you want to compare bars near you, there is no feature that can recommend an optimized itinerary that accounts for your drinking 
preferences while minimizing walking time between bars. Our goal of the project is to create a web-based application which allows users 
to acquire information on Chicago nightlife by integrating the functionality of Google map and Yelp to create a more personal-oriented
application. More specifically, we would like to make a bar crawl generator with an interactive map along with the informations of bars 
and drinks based on user-entered preferences.

Description of functionalities

1. User enter preferences in the form fields
2. After submitted, scroll down for results
3. If results returned, user can click on the list of bars to get map route display, user can also specify travel mode, and show all bar locations.

Project Structure

1. Django framework
   - Chicrawl: contains general settings/urls for the framework with slight modifications to add 
              our app and static directory path
   - crawler:  contains the views.py handle the overal structure.
   - templates: contains two html files, the base.html contains the basic html structure
                and JavaScript code handling Google Maps features, the index.html
                handles what our home page looks like
   - data: contains databse and JSON files
  - res: contains JSON/csv files for neighborhood names and coordinates
  - static: contains CSS file and background pcitures
  
2. Yelp: (build_db directory)
 	 contains all code used to scrape Yelp and Foursquare for generating database.
	- chicago_bars.py : Uses the Yelp API to scrape business data for the top 80 ranked bars for each zipcode. 
	                    Creates a JSON file for each time it gets results from Yelp. The Yelp API returns up to 20 results at a time.
	- json_to_sql.py : Parses the JSON files generated by chicago_bars.py to get the name, latitude, longitude, number of reviews, star rating, 
	                   and address. Inserts that data into a SQLite3 database.
	- weighted_rank.py: Calculates the weighted rank for each bar and inserts it into the SQLite3 databse.
	- price_level.py: Uses the Foursquare API to scrape price tier (number of dollar signs) information for each bar and inserts it into the database.
	
3. Foursquare: (foursquare-api directory)
   get_dict.py uses the foursquare api to attain menu/tag/phrases information about each bar listed in the bars3.db sqlite3 database scraped from the yelp api. 
   The reason why we are using the foursquare api in addition to the yelp api is because we want to enable search term functionalities for our bar crawl app. 
   For example, the user can input terms such as “cocktail”, “whiskey”, “red wine”, etc. when they are customizing their bar crawl route. get_dict.py creates a 
   python dictionary with each KEY being the individual keyword in the menu/tags/phrases section and each VALUE being the list of restaurant that contains that keyword. 
   This python dictionary is eventually stored as a JSON file: foursquare.json.

My contribution to the project
- Responsible for all Django framework code, Google API, and all front-end code. 
- Responsible for partial Yelp database preparation and Dijkstra’s algorithm for walking distance optimization.
