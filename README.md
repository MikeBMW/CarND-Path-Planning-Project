# CarND-Path-Planning-Project

## Code scope
Most of my code is between the keyword of TODO and END;

L168,define variable of "lane", use it to switch to other lanes;

L170,define variable of "ref_vel", use it to control vehicle speed;

L253,set the prev_size which come from the previous path size,use previous path points to help doing a transition;

Line 346 to 348,create vector double list of ptsx and ptsy to use the sparsely spaced waypoints;

Line 350 to 352,define ref_x, ref_y, ref_yaw to keep track rference state;

## Use spline.h to smooth out the path
Line 11,include spline.h in the beginning of the main.cpp file;Create some points with spaces of 30 meters, then use spline to fit that space.Take points inside that spline;

L 355 to 386,check whether previous path size is empty or have some points which could be taken advantage of ;

Line 355 to 366,if previous size less than 2, just use the car state;

Line 368 to 386,if it is larger, then use the last point in that previous path and its second last point; Looking at what were the last couple of points in the previous path that the car was following,and then calculating what angle the car was heading.Then pushing them onto a list of previous points.

Line 388 to 399 define next_wp0,next_wp1,next_wp2, use 30, 60 and 90 to make sure the points are spaced pretty far apart.Pushing these 3 points to ptsx and ptsy.

Line 401 to 410 is doing a transformation to the local car's coordinates

Line 413 to 416 ,define spline s and set some points x and points y to the spline;

Line 418 to 427, building working points with last time previous points, they are the actual points that the path planner is going to be using;

Line 430 to 457, if there are any points from the previous path,add them to path planner.Instead of recreating the path from scratch every single time,add points onto it and work with the left points from last time.We always have 50 points to be used.

## Avoid hitting a car
Use the data which come from sensor fusion. The simulator reports all car information of s d and vx vy values which can be used to figure out where cars are at.

Line 267 to 331, go through the sensor fusion list.

Line 293 to 331,  Do some action if too close.

Line 297 , check other cars whether or not in my lane.

Line 306, check whether the distance of front car is less 30;

Line 333 to 336, decrease the speed of the car if necessary;

## Avoid jerk when cold start
Line 309, if the distance of front car is more than 30, set too_close to false;

Line 337 to 340, increase the speed of ref_vel if there is no car ahead of my car;control the added speed value could avoid jerk when cold start;

## Lane change
Lane 267 to 289, the code check whether there are cars near my car, both left or right will be checked, the gap is between -50 to +50 meters away from my car;

Lane 314 to 328, decide which lane to go, based on current lane.



