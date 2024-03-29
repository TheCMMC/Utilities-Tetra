#Utilities-Tetra

This software is under copyright of the CMMC and no license is offered at the moment. It is used for the Proof of Concept and GFI bioreactor project by the [CMMC](thecmmc.org).

Sample utility C++ code using CGAL for estimating velocity at an arbitrary 3d point from given velocities at sample points.

To incorporate into another program requires the computational geometry c++ header files CGAL from cgal.org. CGAL is distributed under a dual-license scheme. CGAL can be used together with Open Source software free of charge. Using CGAL in other contexts can be done by obtaining a commercial license from [GeometryFactory](http://www.geometryfactory.com/). For more details see their [License page](https://doc.cgal.org/latest/Manual/license.html).

For simplicity, all the functionality is in one file: two functions are implemented and a main program illustrates their use:

fill_triangulation: fills a triangulation data structure with points from a given file containing a line of 3d point coordinates followed by 3d velocity components.

estimate_velocity: given a triangulation data structure and an arbitrary 3d point, locates the point in the triangulation and approximates the velocity based on those of points nearby in the triangulation.
Currently just averages the nearby vertices; better would be to interpolate as in page 3 of https://www.hpl.hp.com/techreports/2002/HPL-2002-320.pdf
Extra care may be needed so that when points are near faces we still get accurate results https://www.johndcook.com/blog/2020/02/27/numerical-heron/

main: passed two files as arguments. Create triangulation data structure from data in first file argument, print out velocities for points in second file argument.

Build:

cgal_create_CMakeLists -s tetra
cmake -DCMAKE_BUILD_TYPE=Release .
make

When the intention is to link with biocellion or other codes that require a relocatable library, use:
cmake -DCMAKE_BUILD_TYPE=Release -DCGAL_CXX_FLAGS="-shared -fPIC" .
(This will result in a core dump if the test code below is executed.)

Run:

./tetra test_data_1 test_data_2

