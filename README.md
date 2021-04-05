# The Dactyl-ManuForm Keyboard - Python 3 - Cadquery
This is a fork of [Dactyl-Manuform](https://github.com/tshort/dactyl-keyboard) by Tom Short, which itself is a fork of [Dactyl](https://github.com/adereth/dactyl-keyboard) by Matthew Adereth, a parameterized, split-hand, concave, columnar, ergonomic keyboard.

While the code structure remains comparable to the original, Clojure and OpenSCAD have been replaced by Python and cadquery/OpenCASCADE.  The predecessors were exceptional contributions to the ergo keyboard community by the authors but used a rather esoteric programming language, Clojure, and a relatively inconsistent geometry engine, OpenSCAD.  My hope is that by converting the code the community will have an easier time modifying and evolving this design.  

## Updated Geometry Engine, now generating STEP files !!!
As part of the effort to create a new engine I converted the code to cadquery/OpenCASCADE.  While OpenSCAD has provided an open source 3D engine that is extremely popular, it frankly creates barely passable STLs when you have complex geometry.  After being extremely frustrated trying to fix the mesh I realized it is just not a stable engine to create high quality files.  OpenCASCADE is extremely powerful but requires extensive detail to operate.  cadquery provided an excellent platform to run a stable geometry engine with a simplified API. 

![STEP File in FreeCAD](./resources/FreeCAD_STEP_screen.png)

## Added Feature
Added a new switch for hot swap and a way to include any additional geometry in the key plate by use of an imported file.  For hot swap just change the line to `hot_swap = True`.  To import an arbitrary geometry set the `plate_file = None` and `plate_offset = 0.0`.  The file must be .step for OpenCascade / cadquery and .stl for openSCAD / solid python.  The zero reference should be the key center (XY), and the top of the plate (Z).  Plate offset is a Z-axis translation for minor adjustments without modifying the geometry file.  If you don't want the "nubs" you have to modify the plate function.  It will propagate to all key plate usage.  

**DISCLAIMER:  I have not built the hot swap version and cannot speak to the geometry.  I found it running around in various places and don't know the origin.**  

If you know the origin I would like to credit the originator.  If you test it I'd love to know how well it works or if you come up with a better geometry I'm happy to add it.  

Message me on Reddit u/j_oshreve if you are really stuck.  I don't have much time to help, but can answer the occasional question.  Also feel free to put in a pull request if you come up with something crafty and want to give others access to it.

![Hot Swap in OpenSCAD](./resources/OpenSCAD_hotswap.png)

## Status / Future
FWIW, the cadquery version is essentially a double translation and is now a bit of a mess.  I wanted to share with the community as the first version of dactyl-manuform that exports as a STEP file, allowing easier editing.  I am happy to maintain the code, but I am unlikely to spend much more time cleaning it up as I am working on an entirely new object-oriented generator in Python/cadquery.  This was my proof of concept for eliminating OpenSCAD from the workflow and I thought it worth giving back to the community. 

**The majority of the the rest of the below content is as defined by previous authors, except where noted.**

![Imgur](http://i.imgur.com/LdjEhrR.jpg)

The main change is that the thumb cluster was adapted from the [ManuForm keyboard](https://github.com/jeffgran/ManuForm) ([geekhack](https://geekhack.org/index.php?topic=46015.0)). The walls were changed to just drop to the floor. The keyboard is parameterized to allow adjusting the following: 

* Rows: 4 - 6 
* Columns: 5 and up
* Row curvature
* Column curvature
* Row tilt (tenting)
* Column tilt
* Column offsets
* Height

I built a 4x5 version (40% size) for myself. The default has a bit more tenting than the Dactyl. See the following model files for configurations that may be most common:

* [40% size, (4x5)](https://github.com/tshort/dactyl-keyboard/blob/master/things/right-4x5.stl)
* [60% size, (5x6)](https://github.com/tshort/dactyl-keyboard/blob/master/things/right-5x6.stl)

## License

Copyright © 2015-2020 Matthew Adereth, Tom Short, and Joshua Shreve

The source code for generating the models (everything excluding the [things/](things/) and [resources/](resources/) directories is distributed under the [GNU AFFERO GENERAL PUBLIC LICENSE Version 3](LICENSE).  The generated models and PCB designs are distributed under the [Creative Commons Attribution-NonCommercial-ShareAlike License Version 3.0](LICENSE-models).
