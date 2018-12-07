# AeroQuad Review
A review of a gps position hold implementation

### Before We Begin...
 - Aeroquad: Open source multicopter firmware. [https://github.com/AeroQuad/AeroQuad](https://github.com/AeroQuad/AeroQuad)
 - The code is a little raw. There are few comments and it can be difficult to follow. It's not the prettiest.
 - The goal is to demonstrate critical thinking, problem solving, and practical application of a software solution.
 - GPS position hold was not supported in the v3.2 release, but basic components were in place for experimental and/or development purposes. (It didn't work)

##### Step 1
 - Civilian GPS is only accurate to within 2.5 meters.
 - Instead of targeting a specific point (lat/lon), why not target a 2.5 meter radius?
 - Updates to GpsNavigator.h
 - [commit](https://github.com/jcleve/AeroQuad/commit/bcf0a68dc90f82712a5228c6bbe392d8bfd310e5)
 - [video](https://www.youtube.com/watch?v=r-jBX3hJkwE)
