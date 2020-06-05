# Introducing PolyGear

![](https://raw.githubusercontent.com/dpellegr/PolyGear/master/imgs/PolyGear.gif "PolyGear")

PolyGear is a powerful OpenSCAD library to create **spur** and **bevel gears** as a single polyhedron. The library allows full control of the **involute tooth profile**, including pressure angle, backlash, variable helix angle, addendum, dedendum and profile shifting.

Being able to vary the helix angle allows for instantaneous generation and switch between herringbone, zerol, spiral and customized profiles; all constructed as a single and smooth polyhedron even for small facet number.

The gear is constructed in an **extremely efficient** way, by triangulating a minimalist vertex cloud with a single polyhedron.

I wrote this library because I was unsatisfied with the existing ones:

* https://www.thingiverse.com/thing:3575
* https://www.thingiverse.com/thing:636119
* https://www.thingiverse.com/thing:1604369

being, to my taste, either too hampered, fragile or computational expensive. My aim has been overcoming these limitations. Do not expect lightening holes or other gimmicks, but comprehensive and efficient control over your gear teeth.

I would expect that the comments in the code and the demo example should suffice as user **documentation**, but if I collect some good questions I may compile a FAQ.
________________

## Requirements:
Polygear requires **OpenSCAD v2019.05** or more recent.

## Library files:

 * PolyGear.scad - main file, the one that you should read and *use* in your project
 * PolyGearBase.scad - computation of the gear profile and some meshing functions
 * PolyGearUtils.scad - collection of more and less trivial complementary functions
 * linspace.scad - lightweight library for producing range of points
 * shortcuts.scad - a slightly enhanced version of the [excellent shortcuts library](https://www.thingiverse.com/thing:644830) by [Parkinbot](https://www.thingiverse.com/Parkinbot/about)

## Basic Knowledge:

The library uses industry standard terminology and conventions. KHK Gears published an [excellent summary](https://github.com/dpellegr/PolyGear/blob/master/docs/Basic%20Gear%20Terminology%20and%20Calculation%20-%20KHK%20Gears.pdf)
 which is mirrored in the docs folder for convenience. If words like "module" and "pressure angle" confuses you, please make sure to review it.

If you want to dive deeper in the evaluation/parameterization of the involute profiles, [this nice open access paper](https://github.com/dpellegr/PolyGear/blob/master/docs/Hartig%20Stein%20-%203D%20involute%20gear%20evaluation.pdf), is what inspired the computations implemented in PolyGearBase.scad.

## FAQ

### What is this "module" thing? Can't I just specify the radius?

Please take a look at the document from KHK Gears linked above. The short answer is that you could use the radius, but in the long run it would hurt yourself with fractional number of teeth and/or non meshing gears. You can think about the module as a universal measure of the size of the tooth. Having the same module is the first requisite when evaluating the proper meshing of two gears, and therefore it is very deeply rooted into the industry standard. 

If you really want to go the radius way, give a random module and use the openSCAD resize() command, but you have been warned...

### How are Bevel Gears constructed/determined?

The construction of the bevel gears starts from the reference circle of the bottom face. It is always centered at the origin of the XY plane and its radius is determined by the module and the number of teeth (as for spur gears).
The next important parameter is the `cone_angle` defined as half of the vertex angle of the cone on which the teeth of the gear lie.
Finally one needs to define either `w` or `z`, the first represent the slant height of the teeth (parallel to the cone face), the second is the height of the teeth (parallel to the cone axis which is the z axis).
At this point the reference radius of the top face is determined and the construction is completed.

<img src="https://raw.githubusercontent.com/dpellegr/PolyGear/master/imgs/bevels.svg" width="200">

### Why does the bottom face of my bevel gear lies at negative z?

This is because the end faces of the teeth of a bevel gears are constructed by projecting the end faces of the teeth of a spur gear (which are planar) on the spherical suface centered at the cone vertex and passing by the reference circle.

### I still have difficulties using the library, any further advice?

When you are developing your design, think as gears as smooth cylinders (spur) and cones (bevel) determined by their reference radius. You need to have these well specified. The library will then take care of producing properly meshing teeth on their lateral surfaces.

## Examples:

The example folder collects some complex assemblies constructed with just a few line of codes by empowering PolyGear.

## Enjoy!

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
