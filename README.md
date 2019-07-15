# My Data Visualizer Documentation


# Contents

* [Introduction](#Introduction)
* [Quick Start](#Quick Start)
* [Concepts](#Concepts)

## Introduction

* ***My Data Visualizer*** is the easiest way to visualize your ***low-data-volume-high-information-value*** [WebGL](https://www.khronos.org/webgl/) 3D visuals.
* The application implements the [DataVisual](https://observablehq.com/@mariodelgadosr/datavisual-data-visual-design-pattern-for-webgl-3d-assets) design pattern.

**Note**: 

* This documentation describes features and functionality in the free version of My Data Visualizer.  
* The full licensed version of the application and framework has additional features detailed in a separate document.

## Quick Start

![Screen Shot of My Data Visualizer Body Demo](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/img/MyDataVisualizerBodyScreenShot.png)

* The quickest workflow is utilizing a glTF with visualizing data in a .csv file.  
	* Embedded data in the glTF is another workflow discussed in detail in this doumentation.
* To get started, you will need a .glTF (or .glb file) and a .csv file with the data that will be visualized.
* The [documentation repository](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/tree/master/repository/Tutorial) has a working example for the *Body* *DataVisual* you can use to model your own *DataVisual*. 
  It contains:
	* The original [Blender 2.79b](https://www.blender.org/) file ([*Body.blend*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.blend)) used to export the .gltf and .glb files.
	* [*Body.gltf*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv): a .gltf text export of the Body.blend file with [Data URIs](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#uris).
	* [*Body.glb*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.glb): a .glb binary export of the Body.blend file.
	* [*Body.csv*](https://github.com/MarioDelgadoSr/MyDataVisualizerDoc/blob/master/repository/Tutorial/Body.csv): a .csv file with data to *drive* the Body *DataVisual*.
* Only the *Body.gltf* and *Body.csv* files are necessary for the Quick Start.  
	* The Body.glb file is included as an example of a binary export.  
	* The *Body.csv* file's data can be used to visualize either Body.gltf or Body.glb.
* As shown in the *Body* *DataVisual*, the following are the requirements for the glTF and CSV data files:
	* glTF:
		* Each [mesh](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#meshes) that will be visualized with the data must have a unique [*name*](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#indices-and-names) attribute and [*material*](https://github.com/KhronosGroup/glTF/tree/master/specification/2.0#materials) associated with it.
		* The *name* attibute value is case sensitive and matches *name* value in the data.
		* *name* attribute values will be [sanitized](https://discourse.threejs.org/t/issue-with-gltfloader-and-objects-with-dots-in-their-name-attribute/6726/2) before a match is attempted against the data.  Example: A *name* of 'Cube.001' is sanitized to 'Cube001'.
	* CSV Data column descriptions:
		* *name*: The values in the *name* column match the glTF mesh *names*.
		* *INSURANCE_CLAIMS*, *DOCTOR_VISITS*, *LAB_ORDERS*: Contain values associated with the *name* attribute values.
		* *DATE_LAST_TEST*: Contains the [JavaScript Date](https://www.w3schools.com/js/js_dates.asp) for the *LAST_TEST*.  
			* The '*DATE_*' prefix designates the data column as a JavaScript Date.  Other supported prefies are '*DATETIME_*' and '*TIME_*'. 
		* *COLOR_INSURANCE_CLAIMS*: Contains pre-defined colors for the *INSURANCE_CLAIMS* column. 
			* The '*COLOR_*' prefix designates the column as a pre-define color value column.    
			* Any [CSS Color Name or Hex Color value](https://www.w3schools.com/colors/colors_names.asp) can be used to pre-define a color.
		* *LINK_*: Contains optional HyperLinks associated with *name* column values.  
			* At run-time, ***My Data Visualizer*** will append the *name* column value to the *LINK_* column value and instruct the browser to navigate to that [url](https://en.wikipedia.org/wiki/URL).	

## Concepts




## Built With

* [D3.js](https://d3js.org/) - D3 framework
* [Three.js](https://threejs.org/) - Three.js framework
* [glTF](https://www.khronos.org/gltf/) - Khronos' graphic library Transmission Format
* [GLTFLoader](https://threejs.org/docs/index.html#examples/loaders/GLTFLoader) - A loader for glTF 2.0 resources
* [dat.gui](https://workshop.chromeexperiments.com/examples/gui/#1--Basic-Usage) - dat.gui
* [Blender](https://www.blender.org/) - For building a 3D visual and [exporting](https://docs.blender.org/manual/en/dev/addons/io_gltf2.html) it to a glTF file.


## Author

* **Mario Delgado**  Github: [MarioDelgadoSr](https://github.com/MarioDelgadoSr)
* LinkedIn: [Mario Delgado](https://www.linkedin.com/in/mario-delgado-5b6195155/)
* [My Data Visualizer](http://MyDataVisualizer.com): A data visualization application using the [*DataVisual*](https://github.com/MarioDelgadoSr/DataVisual) design pattern.


## License

* *My Data Visualizer* is free for all non-profit entities.  
* Businesses and comerical enterprises must purchase a license.  
	* The license includes access to the *My Data Visualizer* javaScript-based framework; which developers can use to embed data-driven WebGL assets in applications. 
* Contact [MyDataVisualizer(at)gmail.com](mailto:MyDataVisualizer@gmail.com) for details. 
