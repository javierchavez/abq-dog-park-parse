#About
This is used to parse [this file](http://www.cabq.gov/parksandrecreation/documents/Dog%20Park%20Map%20Plone.csv) from City of Albuquqerque Data. 

###using

The parser returns a `List<DogPark>`  

So when you initiate the class like this:
	
	ParkParseCSV parser = new ParkParseCSV();
	
Besure you save the return to a `List<DogPark>`  :

	List<DogPark> parks = parser.parseFromUrl(new URL(urlString));
	
Then you can iterate:

	List<MarkerOptions> markerOptsList = new ArrayList<MarkerOptions>();

	for (int i = 0; i < parks.size(); i++) {
		markOptions = new MarkerOptions();
		
		lat = ((DogPark)parks.get(i)).get_ll()[0];
		lng = ((DogPark)parks.get(i)).get_ll()[1];
		
		markOptions.title(((DogPark)parks.get(i)).get_name());
		markOptions.snippet(((DogPark)parks.get(i)).toString());
		markOptions.position(new LatLng(lat, lng));
		markerOptsList.add(markOptions);
	}

And Finally add to your `GoogleMap`:

	for (int i = 0; i < markerOptsList.size(); i++) {
		googlemap.addMarker(markerOptsList.get(i));
	}
	
###Notes

Lat and Lon are in the `Dog Park` Class and can be retrieved from a `double[]` like this:

**Fist element is lat**

	double lat = ((DogPark)parks.get(i)).get_ll()[0];

**Second element is lng**
	
	double lng = ((DogPark)parks.get(i)).get_ll()[1];
	
