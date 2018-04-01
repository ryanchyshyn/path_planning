[//]: # (Image References)

[image1]: ./img/1.jpg "Screenshot"

# CarND-Path-Planning-Project
![image][image1]
Self-Driving Car Engineer Nanodegree Program
   
### Overview
In this project the goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. There will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.

### Implementation
The code has two major parts:
1. Trajectory planning.
2. Lane change detection.

## Trajectory planning/Model documentation
The trajectory planning implementation uses provided map waypoints, simulator variables (like car_s and car_d, previous_path_x, etc) and "spline" function. The idea is to get previous trajectory points, add several new points in in front of the car, generate spline function based on these data and finally use this function to generate smooth trajectory that consists of previous trajectory and new one.
The one thing that should be taked into account is that "spline" function requires that "X" data should be continous while fitting. To meet this specification the coordinates system is rotated before fitting the data, and then reverted back.

## Lane change detection
The car start at the center lane and uses the following "driving" alghorithm: drive in current lane unless there is no other car in front, if there is such a car in front then try to change the lane to the left or right if there is no car, otherwise slow-down the speed.
