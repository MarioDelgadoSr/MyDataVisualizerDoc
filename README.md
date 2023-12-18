# My Data Visualizer Documentation 


# Contents

* [Introduction](#Introduction)
	* [Demonstration Site](#Demonstration-Site)
* [Quick Start](#Quick-Start)
* [Background](#Background)
	* [General](#General)
	* [Technical](#Technical)
* [Requirements](#Requirements)	
	* [Data](#Data)
		* [Data Attributes](#Data-Attributes)
	* [WebGL 3D Graphic](#WebGL-3D-Graphic)
* [Analysis](#Analysis)	
	* [Data Visual](#Data-Visual)
	* [Analyzer](#Analyzer)
		* [Data Grid](#Data-Grid)
		* [Visualization Scale and Legend](#Visualization-Scale-and-Legend)
	* [Visual Grid](#Visual-Grid)
* [Built With](#Built-With)
* [Creator](#Creator)
* [License](#License)
<!-- * [Concepts](#Concepts) -->

## Introduction

* [***My Data Visualizer***](https://github.com/MarioDelgadoSr/MyDataVisualizer) is the easiest way to visualize your ***low-data-volume-high-information-value*** [WebGL](https://www.khronos.org/webgl/) 3D visuals.
* It's an excellent framework to visualize measures and dimensions from [Internet of Things](https://www.forbes.com/sites/jacobmorgan/2014/05/13/simple-explanation-internet-things-that-anyone-can-understand/#6372cfeb1d09) visual assets.
* The application implements the [DataVisual](https://observablehq.com/@mariodelgadosr/datavisual-data-visual-design-pattern-for-webgl-3d-assets) design pattern.
* [***My Data Visualizer***](https://github.com/MarioDelgadoSr/MyDataVisualizer) is a [100% Client-side application](https://en.wikipedia.org/wiki/Client-side); your data is not uploaded to a server or the cloud.

### Demonstration Site	

* [My Data Visualizer Demo](https://mariodelgadosr.github.io/MyDataVisualizer/)
	
**Note**: 

* This documentation describes features and functionality in the free version of My Data Visualizer.  
* The full licensed version of the application and framework has additional features detailed in a separate document.

## Quick Start

![Screen Shot of My Data Visualizer Body Demo](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerBodyScreenShot.png)

* The quickest work-flow is utilizing a [glTF](https://en.wikipedia.org/wiki/GlTF) with data in a [.csv file](https://en.wikipedia.org/wiki/Comma-separated_values).  
	* You can use the files described here as a template for your DataVisual that is [uploaded to ***My Data Visualizer***](http://mydatavisualizer.com/demo/).
		* Data that are uploaded are parsed with the [D3 AutoType parser](https://github.com/d3/d3-dsv#autoType).
	* [Embedded data](#Data) in the glTF is another work-flow discussed in detail in this documentation.
* To get started, you will need a .glTF (or .glb file) and a .csv file with the data that will be visualized.
* The [documentation repository](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/tree/master/repository/Tutorial) has a working example for the *Body* *DataVisual* you can use to model your own *DataVisual*s. 
  It contains:
  
  	Repository File | Description
	----------------|------------
	[*Body.gltf*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.gltf) |  A .gltf text export of the Body.blend file with [Data URIs](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#uris).
	[*Body.csv*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) | A .csv file with data to *drive* the Body *DataVisual*.
	[*Body.glb*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.glb) | A .glb binary export of the Body.blend file.
	[*Body.blend*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.blend) | The original [Blender 2.79b](https://www.blender.org/) file used to export the .gltf and .glb files.  Use this file to see how a 3D visual asset is built in Blender.  [Other applications that export glTF files](https://github.com/KhronosGroup/glTF#gltf-tools) can be used as well if the [*meshes*](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes) visualized have distinct/unique [*materials*](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#materials) assigned to them.
	
* Only the [*Body.gltf*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.gltf) and [*Body.csv*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) files are necessary for the Quick Start.  
	* The [*Body.glb*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.glb)  file is included as an example of a binary export.  
	* The [*Body.csv*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) file's data can be used to visualize either [*Body.gltf*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) or [*Body.glb*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.glb).
* As shown in the *Body* *DataVisual*, the following are the requirements for the glTF and CSV data files:
	* [*Body.gltf*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.gltf):
		* Each [mesh](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes) that will be visualized with the data must have a unique [*name*](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#indices-and-names) attribute and [*material*](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#materials) associated with it.
		* The *name* attibute value is case sensitive and matches *name* column values in the data.
		* *name* attribute values will be [sanitized](https://discourse.threejs.org/t/issue-with-gltfloader-and-objects-with-dots-in-their-name-attribute/6726/2) before a match is attempted against the data.  
			* Example: A *name* of 'Cube.001' is sanitized to 'Cube001'; with the '.' removed from the *name*'s value.
	* [*Body.csv*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) Data:

		name | INSURANCE_CLAIMS | DOCTOR_VISITS | LAB_ORDERS | DATE_LAST_TEST | COLOR_INSURANCE_CLAIMS | LINK_
		-------|-------|-------|-------|-------|-------|-------
		Brain | 27000 | 3 | 0 | 2019-02-01T00:00 | green | http://www.bing.com/search?q=
		Heart | 234000 | 11 | 6 | 12019-06-09T00:00 | red | http://www.bing.com/search?q=
		Kidneys | 14500 | 5 | 1 | 2019-08-01T00:00 | yellow | http://www.bing.com/search?q=
	
	* [*Body.csv*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) Data column descriptions:
	
		CSV Column | Description
		-------|------------
		*name* | The values in the *name* column match the glTF mesh *names*.
		*INSURANCE_CLAIMS* |  Insurance Claim values associated with the *name* attribute values.
		*DOCTOR_VISITS*  | Doctor visits associated with the *name* attribute value.
		*LAB_ORDERS* |  Lab Order values associated with the *name* attribute values.
		*DATE_LAST_TEST* | Contains the [ECMA Script](https://www.ecma-international.org/ecma-262/9.0/index.html#sec-date-time-string-format) formatted date for the *LAST_TEST*. The '*DATE_*' prefix designates the data column as a JavaScript Date.  Other supported prefies are '*DATETIME_*' and '*TIME_*'. 
		*COLOR_INSURANCE_CLAIMS* | Contains pre-defined colors for the *INSURANCE_CLAIMS* column.  The '*COLOR_*' prefix designates the column as a pre-define color value column. Any [CSS Color Name or Hex Color value](https://www.w3schools.com/colors/colors_names.asp) can be used to pre-define a color.
		*LINK_* | Contains optional HyperLinks associated with *name* column values. At run-time, ***My Data Visualizer*** will append the *name* column value to the '*LINK_*' column value and instruct the browser to navigate to that [url](https://en.wikipedia.org/wiki/URL).	

## Background

### General

[***My Data Visualizer***](https://github.com/MarioDelgadoSr/MyDataVisualizer) was developed to add an important *dimension* to data visualization; [WebGL 3D graphics](https://blogg.bekk.no/webgl-and-data-visualisation-379d8252ea51?gi=fe1368432a8f).

With [***My Data Visualizer***](https://github.com/MarioDelgadoSr/MyDataVisualizer) data is contextualized on a 3D graphic representation of the real-world objects that the data is associated with.

For example, the following screen shot visualizes passenger revenue on a plane for each assigned seat location:

![Screen Shot of My Data Visualizer Plane Visualization](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerPlaneScreenShot.png)


### Technical

The following two [Computational Essays](https://blog.stephenwolfram.com/2017/11/what-is-a-computational-essay/) hosted on [ObservableHQ.com](https://observablehq.com/@observablehq/introduction-to-notebooks) provide a technical background on the design approach for ***My Data Visualizer***:

* [DataVisual (Data + Visual) Design Pattern for WebGL 3D Assets](https://observablehq.com/@mariodelgadosr/datavisual-data-visual-design-pattern-for-webgl-3d-assets) and 
* [DataVisual (Data + Visual) Design Pattern for WebGL 3D Assets using a glTF with Embedded Data](https://observablehq.com/@mariodelgadosr/datavisual-data-visual-design-pattern-for-webgl-3d-assets-u)


## Requirements

[***My Data Visualizer***](https://github.com/MarioDelgadoSr/MyDataVisualizer) requires:

* **Data** (measures and dimensions) following a set of simple [specifications](#Data-Attributes);
* **WebGL 3D** Graphic with addressable [material(s)](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#materials) for the graphic's sub-components that will be visualized.

Both of these components can be uploaded (see screen shot) to the [demonstration application](http://mydatavisualizer.com/demo/) as one of the following:

* A .gltf or .glb file with its associated .csv file (see [Quick Start](#Quick-Start) for an example);
* A .gltf file with embedded data; (see the [repository](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/tree/master/repository) for several examples).
* A .glb file with the embedded data (see the [repository](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/tree/master/repository) for several examples).

Data that are uploaded are parsed with the [D3 AutoType parser](https://github.com/d3/d3-dsv#autoType).

![Screen Shot of My Data Visualizer Upload](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerUploadScreenShot.png)


#### Data

The data to be visualized can be in either a [.csv file](https://en.wikipedia.org/wiki/Comma-separated_values) or embedded in the [glTF file](https://github.com/KhronosGroup/glTF/tree/master/specification/) that describes the WebGL 3D graphic itself.

* The [Body.csv](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv) is an example of the data associated with the [*Body.gltf*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.gltf) file:

name | INSURANCE_CLAIMS | DOCTOR_VISITS | LAB_ORDERS | DATE_LAST_TEST | COLOR_INSURANCE_CLAIMS | LINK_
-------|-------|-------|-------|-------|-------|-------
Brain | 27000 | 3 | 0 | 2019-02-01T00:00 | green | http://www.bing.com/search?q=
Heart | 234000 | 11 | 6 | 12019-06-09T00:00 | red | http://www.bing.com/search?q=
Kidneys | 14500 | 5 | 1 | 2019-08-01T00:00 | yellow | http://www.bing.com/search?q=

* Creating a .csv file with the data is relatively simple and can be accomplished with spreadsheet; like [Microsoft Excel](https://support.office.com/en-us/article/Import-or-export-text-txt-or-csv-files-5250ac4c-663c-47ce-937b-339e391393ba).

* In contrast, [BodyEmbeddedData.gltf](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/BodyEmbeddedData.gltf) illustrates the embedded data scenario.  Below is a reference to one of the several [extras](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#reference-extras) sections hosting the data associated with the individual meshes:

<pre style="background-color: gainsboro;"> 
	"extras": {
					"LINK_": "http://www.bing.com/search?q=",			
					"COLOR_INSURANCE_CLAIMS": "green",
					"DATE_LAST_TEST": "2019-02-01T00:00",
					"DOCTOR_VISITS": 3.0,
					"INSURANCE_CLAIMS": 27000.0,
					"LAB_ORDERS": 0.0
				}

</pre>


* The embedded data scenario involves using a graphical tool that allows you to add the [extras](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#reference-extras) sections to the WebGL 3D graphics.  The github repository [***Python Script to Add Blender Custom Properties From CSV File***](https://github.com/MarioDelgadoSr/AddBlenderCustomPropertiesFromCSV) details one possbile approach for developers that use the popular [Blender](https://www.blender.org/) application.

	* This video also provides step-by-step instructions on adding [Custom Properties](https://docs.blender.org/manual/en/latest/data_system/custom_properties.html) to Blender that are then embedded as extras when a [Blender glTF file is exported](https://wiki.blender.org/wiki/Reference/Release_Notes/2.80/Import_Export):
	
	[![Adding Custom Properties to Objects](https://img.youtube.com/vi/MWkoviO_xkY/0.jpg)](https://www.youtube.com/watch?v=MWkoviO_xkY)


##### Data Attributes

The following table summarizes the data attributes supported by ***My Data Visualizer*** for data hosted in either a .csv file or embedded within the glTF file:

Attribute | Description
-------|------------
*name* | The value associated with the *name* attribute must match the glTF mesh *names*.
*dimension* |  An attribute identifier for a dimension(s).  Examples: 'Part Number', 'Part_Number', 'PartNumber'
*measure*  | An attribute identifier for a measure(s). Example: 'Number of Complaints', 'Number_of_Complaints', 'NumberOfComplaints'
*COLOR_dimension, COLOR_measure* |  An indentifier with the '*COLOR_*' prefix designates an pre-define color attribute for a given *measure* or *dimension*.  Values can be any [CSS color name](https://www.w3schools.com/colors/colors_names.asp) or [hex triple](https://en.wikipedia.org/wiki/Web_colors#Hex_triplet) value.
*DATE_dimension, DATETIME_dimension, TIME_dimension* | An attriute identifier for an [ECMA Script](https://www.ecma-international.org/ecma-262/9.0/index.html#sec-date-time-string-format) formatted date specified as a *dimension* . The '*DATE_*', '*DATETIME_*' and '*TIME_*' prefixes designate the data as a JavaScript Date.  
*LINK_* | An attribute identifier for optional HyperLinks associated with *name* column values. At run-time, ***My Data Visualizer*** will append the *name* column value to the '*LINK_*' column value and instruct the browser to navigate to that [url](https://en.wikipedia.org/wiki/URL).	
*\s* | An attribute identifier prefix that instructs the data load parser to override the [D3 AutoType parser](https://github.com/d3/d3-dsv#autoType) and treat the columns contents as a string. Example: '\sPart Number' will interpret '123' as the string '123' and not the number 123.


#### WebGL 3D Graphic

* The WebGL 3D Graphic is described in a [glTF file with the 2.0 specifications](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0).  
* Several examples are provided in the documentation [repository](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/tree/master/repository).  
	* Note that each individual mesh (object sub-component) **must have a distinct material associated with it**.  If this condition is not satisfied, the visualization logic can not *drive* sub-component visualizations.
    * In addition, the glTF file **must have** any [buffers](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#binary-data-storage) and [images](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#images) for the .gltf file referenced with embedded [Data URIs](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#uris).
		* This is a [specific export option with the Blender glTF exporter](https://github.com/KhronosGroup/glTF-Blender-Exporter/blob/master/docs/user.md#embedding).
	* This video is a tutorial for exporting a glTF with Blender:
	
		[![Exporting GLTF file using Blender](https://img.youtube.com/vi/xfUZ1GLG68o/0.jpg)](https://www.youtube.com/watch?v=xfUZ1GLG68o)

## Analysis

[***My Data Visualizer***](https://github.com/MarioDelgadoSr/MyDataVisualizer) has three primary panels used in the data visualization analysis:

* Data Visual 
* Analyzer
* Visual Grid

### Data Visual

The ***Data Visual*** panel displays a 3D rendering of the WebGL graphic.   Several mouse interactions, quick keys and  buttons are available to interact with the visual (see screen shot):

Mouse Action | Description
-------|------------
Left | Rotate
Scroll | Zoom
Right | Pan
Left Double-Click| Toggle search isolation of an object. 
CtrlKey + Left | Select an object and navigate link(s).  If a link is associate wth an object, a selection drop will be displayed allowing navigation to the designated address (see screen shot).

Key | Description
-------|------------
Arrow | Pan
'b' | 'B'ird's-eye View/Rotate 
'c' or 'Esc' | 'C'lear Data Selections

Button | Description
-------|------------
GPU Performaance | Displays Graphic Processing Unit (GPU) statistics.
Reset View | Resets Bird's-eye View.
Axes | Toggles display of the origin axes associate with the visual.
Background | A color selection picker for the background color.
Bounding Box/Color | Toggles disply of a visual bounding box and color selection.
Camera Field of View | Allows selection of the visual's field of view.
Polar Angel |  Allows selection of the rotation polar angle.  With a polar angle of 180 degrees, the image can be viewed from underneath.
Zoom Speed | Controls the scroll zooming speed for a visual.
Pan Speed | Controls the pan speed.
Grid/Grid Color | Toggles the display of the visual's grid and its color.
Center Line Color | Sets the center line color for the grid when it is being displayed.
Grid Divisions | Sets the number of grid divisions when it is being displayed.

![Screen Shot of My Data Visualizer ForkLift1](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerForkLiftScreenShot1.png)

### Analyzer

The ***Toggle Analyzer*** button toggles the display of the Analyzer panel.  It contains the ***Data Grid***, ***Visualization Scale/Legend*** sub panels.

In the following screen shot: 

* The *PART* dimension associated with the Forklift visual is selected.
* A red (low) to green (high) color scale is selected and alphabetically assigned to the individual parts in the legend and visual sub-components.

![Screen Shot of My Data Visualizer ForkLift2](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerForkLiftScreenShot2.png)

#### Data Grid 

The ***Data Grid***: 

* Displays the data that visualizes the 3D WebGL graphic.  
* Selecting a column directs the application to visualize the graphic by either a scale colorization determined by the column's values or preset color assignments.  
* Selecting the ***Visualize Grid*** button will color visualize the ***Data Grid*** itself.   
* Searches or row selections can be performed on the the ****Data Grid**** to isolate sub-objects in the visual panel.
* When the ***Visual Grid*** is being displayed, searches in the ***Data Grid** are coordinated with it.

#### Visualization Scale and Legend

The ***Visualization Scale*** and ***Legend*** panels display a color scale selection slider with its corresponding legend.  The left mouse button is used to select the desired scale.

The triangle in the ***Visualization Scale***  panel illustrates the color scale from low to high values.

![Screen Shot of My Data Visualizer ForkLift3](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerForkLiftScreenShot3.png)


### Visual Grid

The ***Visual Grid***:

* Is enabled with the ***Toggle Visual Grid*** button.
* Displays specific attributes common to all visuals; *name*, *Color* (the original color associated with a mesh), *id*, *x* coordinate, *y* coordinate and *z* coordinate. 
* Selecting a column directs the application to visualize the graphic by either a scale colorization determined by the column's values or the original color assignments.  
* Selecting the ***Visualize Grid*** button will color visualize the ***Visual Grid*** itself.   
* Searches or row selections can be performed on the the ****Visual Grid**** to isolate sub-objects in the visual panel.
* When the ***Data Grid*** is being displayed, searches in the ***Visual Grid** are coordinated with it.
 
![Screen Shot of My Data Visualizer ForkLift4](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerForkLiftScreenShot4.png) 

## Built With

The following frameworks and applications were used to build ***My Data Visualizer***:

* [D3.js](https://d3js.org/) - D3 framework
* [Three.js](https://threejs.org/) - Three.js framework
* [glTF](https://www.khronos.org/gltf/) - Khronos' graphic library Transmission Format
* [GLTFLoader](https://threejs.org/docs/index.html#examples/loaders/GLTFLoader) - A loader for glTF 2.0 resources
* [Blender](https://www.blender.org/) - For building a 3D visual and [exporting](https://docs.blender.org/manual/en/dev/addons/io_gltf2.html) it to a glTF file.
* [w2ui UI Library](http://w2ui.com/web/) 


## Creator

* **Mario Delgado**  Github: [MarioDelgadoSr](https://github.com/MarioDelgadoSr)
* LinkedIn: [Mario Delgado](https://www.linkedin.com/in/mario-delgado-5b6195155/)
* [***My Data Visualizer***](https://mariodelgadosr.github.io/MyDataVisualizer/): A data visualization application using the [*DataVisual*](https://github.com/MarioDelgadoSr/DataVisual) design pattern.
* Contact: [MyDataVisualizer(at)gmail.com](mailto:MyDataVisualizer@gmail.com). 

## License

* [***My Data Visualizer***](https://mariodelgadosr.github.io/MyDataVisualizer/) is free for all non-profit entities.  
* Businesses and commercial enterprises are granted a full-use license as long as they make their application freely available to non-profits.
