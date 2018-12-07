# AeroQuad Review
A review of a gps position hold implementation

### Before We Begin...
 - Aeroquad: Open source multicopter firmware. [https://github.com/AeroQuad/AeroQuad](https://github.com/AeroQuad/AeroQuad)
 - The code is a little raw. There are few comments and it can be difficult to follow. It's not the prettiest.
 - The goal is to demonstrate critical thinking, problem solving, and practical application of a software solution.
 - GPS position hold was not supported in the v3.2 release, but basic components were in place for experimental and/or development purposes. (It didn't work)

##### Step 1 - Target Zone
 - Civilian GPS is only accurate to within 2.5 meters.
 - Instead of targeting a specific point (lat/lon), why not target a 2.5 meter radius?
 - Updates to GpsNavigator.h
 - [commit](https://github.com/jcleve/AeroQuad/commit/bcf0a68dc90f82712a5228c6bbe392d8bfd310e5)
 - [video](https://www.youtube.com/watch?v=r-jBX3hJkwE)

##### Step 2 - Slower
 - Still seems to be overshooting the target zone. Let's slow it down a bit.
 - Adjusted some PID values and constants. Very minor update.
 - Updates to GpsNavigator.h
 - [commit](https://github.com/jcleve/AeroQuad/commit/f9706d270a0db45abe31e7d4f72719ef517246e5)
 - [video](https://www.youtube.com/watch?v=TKBPJUfeawY)

##### Step 3 - Filtered/Averaged GPS Data
 - Behavior appears improved, but seems to be a bit erratic and we're still overshooting the target.
 - Because the GPS is only accurate to within 2.5 meters, we may be seeing inconsistent positions being recorded.
   Let's try keeping the last 4 positions and averaging it with the current to filter/dampen the current position.
 - [commit](https://github.com/jcleve/AeroQuad/commit/b88fce3cbee5024da0673f7171d349f4211b6c0d)
 - [video](https://www.youtube.com/watch?v=BOyLYXRIbcU)

##### Step 4 - Test, Validate, Improve, Repeat
 - Test different methods of finding the distance between two waypoints. Speed and accuracy are mutually exclusive.
 - Added logging to retrieve values for heading, distance, and time to calculate in a controlled environment. (Back yard)
 - Updates to GpsNavigator.h
 - [commit](https://github.com/jcleve/AeroQuad/commit/714ef7701ddbdcd521d7437d9db7e78886663ec8)
 - Apply linear weight value to correction angle based on distance from target zone.
 - [commit](https://github.com/jcleve/AeroQuad/commit/bb3c6d1628cbf0fd5eeb9a1a9c279d6f49f09314)
 - Instead of a linear function, let's try to determine a weight from a defined exponential curve (exponential growth function)
 - Updates to GpsNavigator.h
 - [commit](https://github.com/jcleve/AeroQuad/commit/b75fbaba7b8b9278780ad8f00e203e59e42c0b30)
 - [video](https://www.youtube.com/watch?v=wQXof8apN-U)

##### Step 5 - Refine
 - Hold behavior is markedly improved. Adjust hold plane to make control adjustments more granular
 - [commit](https://github.com/jcleve/AeroQuad/commit/124c029e1ee7d504bb54de385c485b46beb477cf)
 - [video](https://www.youtube.com/watch?v=-53BUIlLRrY)
 
