#Bringing Voronoi To Adobe Illustrator  
this is a AI CS5 (Extend)script collection for generating Voronoi diagrams in Adobe Illustrator.  
The Voronoi implementation is taken from [gorhills javascript-voronoi port at github](https://github.com/gorhill/Javascript-Voronoi)   
Thanx a lot for this MIT licensed code.  
  
##Getting Started    
to see what is happening just [download the whole package](https://github.com/fabiantheblind/Illustrator-Javascript-Voronoi/zipball/master). Run the script from Illustrator by hitting **CMD+F12 (on Mac) or STRG+F12 (on Win)** and selecting the file **voronoi_basic.jsx.** Or download the file [rhill-voronoi-core.js"](https://raw.github.com/gorhill/Javascript-Voronoi/master/rhill-voronoi-core.js) and paste the code below into a new file that lies next to the rhill-voronoi-core.js.  
The function util_inspect_properties(f) works with the [Extend Script Toolkit](http://www.adobe.com/devnet/scripting.html) console.

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
	try {array.push (props[i].name + ": " + f[props[i].name])} catch (_){}
	array.sort ();  
	$.writeln (array.join ("\r"));
	}
  
#Examples
There are three of them
###voronoi_basic.jsx
As mentioned above it builds the basic example by gorhill in Illustrator    
  
  
    
All the examples below use *only* the path points. Curves dont get calculated. If you want to reflect curves - add pathpoints along it! [(have a look at this)](http://preview.tinyurl.com/78yg4ht)
	
###voronoi.jsx
a more complex graphic is created with this script. It uses the Unibody 8 SmallCaps Regular font from [underware](http://www.underware.nl/)   
###voronoi_fromSelection.jsx
The "voronoi_fromSelection.jsx" script takes the selection from the active document and copies it to a new document with the same size as the source document. Than comes the magic…  
  
It works with text, path items and compound paths.
The best thing is to release all artworks (at least roughly) to simple path items. Than select the graphic you want to convert to a diagram. 
(Not tested yet with mesh items, symbols, raster items, graph items or placed items)  
Than the copied items will be transformed. The script will try to release all groups and compound paths turn text into outlines. But if you want to save some time do it yourself.    
#####User Interaction - Step by Step   
1. release as much compound paths as possible  
2. turn text to outlines    
3. release all groups   
4. select your graphic  
5. run the script  
Depending on how many points you process* you can make some coffee or watch the script working for you    
  
#####Transformations
These are the transformations that occur:
      
- copies selection to a new document with the same size as the source doc
- textFrames get converted to outlines  
- groups get ungrouped using [this code (ungroupV1.js)](http://forums.adobe.com/thread/456042) by Nokcha  
- all compound paths get released [based on this example](http://forums.adobe.com/message/2140054)   
- calculates the diagram  
- locks the original layer and makes it invisible  
- creates a layer with the edges  
- calculates cell colors based on hsl circle or randomly   
- creates a layer with the cells
- creates a layer with the sites  
  
#####Options  
In the top of the script are some global variables:  
    
- COLOREDCELLS -> if true all cells get colored randomly  
- HSBCOLORSCELLS -> if true the colors are on the hsb circle  
- STROKEDCELLS -> if true all cells get a black stroke  
- DRAWCELLS -> if true it creates a layer with the cells  
- DRAWEDGES -> if true it creates a layer with the edges   
- DRAWSITES -> if true it creates a layer with the sites  
  
#####Video 2 voronoi_fromSelection.jsx
<iframe src="http://player.vimeo.com/video/38493279?byline=0&amp;portrait=0&amp;color=ffffff" width="500" height="281" frameborder="0" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
#####License  
Same as gorhill. This code is under MIT License.  
This product includes software developed by netbluew@nate.com and its contributors  
([ungroupV1.js](http://forums.adobe.com/thread/456042) by Nokcha).  
  
Copyright (c)  2012 Fabian "fabiantheblind" Morón Zirfas  
    
Permission is hereby granted, free of charge, to any person obtaining a copy of thissoftware and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:  
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.  
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.  
see also http://www.opensource.org/licenses/mit-license.php

#*Be aware of your pathPoints.length
Use this code:  

	    var count = 0;      	for (var i =0; i < app.activeDocument.selection.length;i++){      	try{count+=app.activeDocument.selection[i].pathPoints.length;}catch(e){}    	};	    alert("you have "+count+ " pathpoints in your selection");  
  