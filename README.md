#bringing voronoi to illustrator  
this is a AI CS5 script collection for generating Voronoi diagrams in Adobe Illustrator.  
The Voronoi implementation is taken from [gorhills javascript-voronoi port at github](https://github.com/gorhill/Javascript-Voronoi)   
Thanx a lot for this MIT licensed code.  
##getting started    
to see what is happening just run the script **voronoi_basic.jsx**  

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
	
a more complex graphic is created with **voronoi.jsx**   
there will be a version that works with the selection  

