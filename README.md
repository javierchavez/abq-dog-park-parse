[<img src="http://javierachavez.com/wp-content/uploads/2013/05/gdg.png">](https://plus.google.com/104324957573179054979)

#Google Code Lab 
 
  
###About this parser
This is used to parse [this file](http://www.cabq.gov/parksandrecreation/documents/Dog%20Park%20Map%20Plone.csv) from City of Albuquqerque. 
  

###Getting situated
Copy `ParkParseCSV.java` into your project

Change the package to your package name
`package com.some.package;`

###Using
The parser returns a `List<DogPark>`  

So you initiate the class like this:
	
	ParkParseCSV parser = new ParkParseCSV();
	
Be sure you save the return of `parseFromUrl()` to a `List<DogPark>`  :

	//param is a URL object
	List<DogPark> parks = parser.parseFromUrl(new URL(urlString));
	
Then you can iterate:

	final int size = parks.size();
	//array holding marker options
	MarkerOptions[] markerOptArray = new MarkerOptions[size];

	for (int i = 0; i < size; i++) {
		//create a new object
		MarkerOptions markerOption = new MarkerOptions();
		
		//get lat and lng
		double lat = ((DogPark)parks.get(i)).get_ll()[0];
		double lng = ((DogPark)parks.get(i)).get_ll()[1];
		
		//set fields
		markerOption.title(((DogPark)parks.get(i)).get_name());
		markerOption.snippet(((DogPark)parks.get(i)).toString());
		markerOption.position(new LatLng(lat, lng));
		
		//add markerOptions object to array
		markerOptArray[i] = markerOption;
	}

And finally add to your `GoogleMap`:

	for (int i = 0; i < markerOptArray.length; i++) {
		googlemap.addMarker(markerOptsList[i]);
	}
	
###Notes

**Casting**  
When getting a `DogPark` object from a list make sure you cast to get access to `DogPark`'s fields.
	
	((DogPark) parks.get(i))

**Feilds**	
`Dog Park` has these fields:  
Accessed with get_field()
	
		String _name;		
		String _address;
		String _notes;
		String _website;
		double[] _ll;
		String _hours;
		boolean _isWater;

**Position**

latitude and longitude are in the `Dog Park` Class and can be retrieved from a `double[]` like this:

*First element is latitude*

	double lat = ((DogPark) parks.get(i)).get_ll()[0];

*Second element is longitude*
	
	double lng = ((DogPark) parks.get(i)).get_ll()[1];
	
