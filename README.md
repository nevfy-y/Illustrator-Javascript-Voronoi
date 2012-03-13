#BRINGING VORONOI TO ADOBE ILLUSTRATOR  
this is a AI CS5 (Extend)script collection for generating Voronoi diagrams in Adobe Illustrator.  
The Voronoi implementation is taken from [gorhills javascript-voronoi port at github](https://github.com/gorhill/Javascript-Voronoi)   
Thanx a lot for this MIT licensed code.  
  
##GETTING STARTED    
to see what is happening just [download the whole package](https://github.com/fabiantheblind/Illustrator-Javascript-Voronoi/zipball/master). Run the script from Illustrator by hitting **CMD+F12 (on Mac) or STRG+F12 (on Win)** and selecting the file **voronoi_basic.jsx.** Or download the file [rhill-voronoi-core.js"](https://raw.github.com/gorhill/Javascript-Voronoi/master/rhill-voronoi-core.js) and paste the code below into a new file that lies next to the voronoi-core.

	#include "rhill-voronoi-core.js"
	var voronoi = new Voronoi();  
	var bbox = {xl:0,xr:800,yt:0,yb:600};  
	var vertices = [{x:200, y:200}, {x:50, y:250}, {x:400, y:100} /* , ... */];  
	// a 'vertex' is an object exhibiting 'x' and 'y' properties. The  
	// Voronoi object will add a unique 'voronoiId' property to all  
	// vertices. The 'voronoiId' can be used as a key to lookup the  
	// associated cell in 'diagram.cells'.  
	var diagram = voronoi.compute(vertices, bbox);  
	// now inspect the code with the function util_inspect_properties
	// by Peter "the Magnificant" Kahrel  
	// http://www.kahrel.plus.com/indesign/scriptui.html   
	// look under "Displaying properties and methods"  
	$.writeln (util_insepct_properties(result.cells[0].site));
	  
	function  util_inspect_properties (f) {  
	$.writeln (f.reflect.name);
	var props = f.reflect.properties;
	var array = [];
	for (var i = 0; i < props.length; i++)
	try {array.push (props[i].name + ": " + f[props[i].name])} catch (_){} array.sort ();
	$.writeln (array.join ("\r"));
	}
  
#EXAMPLES
All the examples below use *only* the points. Curves dont get calculated. If you want to reflect curves - add pathpoints along it!
###voronoi_basic.jsx
As mentioned above it builds the basic example by gorhill in Illustrator    	
###voronoi.jsx
a more complex graphic is created with the script **voronoi.jsx** (also contained in the package). It uses the Unibody 8 SmallCaps Regular font from [http://www.underware.nl/](http://www.underware.nl/)   
###voronoi_fromSelection.jsx
The "voronoi_fromSelection.jsx" script takes the selection from the active document and copies it to a new document with the same size as the source document. **It works with text, path items and compund paths. The best thing is to release all artworks to simple path items. (Not tested yet with mesh items, symbols, raster items, graph items or placedItems)** Than the copied items will be transformed.  
- textFrames get conveted to outlines  
- groups get ungrouped using [this code](http://forums.adobe.com/thread/456042) by Nokcha  
- all compound paths get released [based on this example](http://forums.adobe.com/message/2140054)   
Afterwards it creates the diagram onto a new layer.**Be aware of the amount of points you process**