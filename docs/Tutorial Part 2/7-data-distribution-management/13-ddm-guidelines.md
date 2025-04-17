---
sidebar_position: 13
---

# Guidelines for Designing Good Checkerboard DDM

The checkerboard DDM approach is simple and yet powerful. It is possible to work with geographical squares, but also with other ways to map a multidimensional variable to one dimension with a fixed number of regions. You can for example use the fifty states of the US. The only requirement is that there should be an unambiguous way to map the input values to an integer.

You may of course also design DDM that uses a checkerboard with two Dimensions, one for LatitudeDim and one for Longitude. The result is very similar. In the above case they would both have a Dimension Upper Bound of 4 and you would get 16 distinct Regions. 

How many squares should you use and how should you design them? This really depends on how much you need to reduce the data flow. This is based on the number of object instances and their update rate. A general guideline is that, for a given object instance, you should change the associated regions less often than you call Update Attribute Values. 

Also note that the checkerboard is globally designed across the federation and may not perfectly fit any specific federate’s filtering needs. This means that you may want to do additional filtering inside a subscribing federate.
