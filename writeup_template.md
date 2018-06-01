## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---

---
### Writeup / README

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`
<b>motion_planning.py</b>

It has multiple states. Each indivudal state will perform the functions written inside them.

Each state includes method and performs those actions. The order of them are Manual->Arming->Planning->TakeOff->Waypoint. At the waypoint stage it will loop until all given waypoints are finished. It'll then proceed to Landing->Disarming->Manual. The states and how they are in order represents a finite-state machine.

<b>planning_utils.py</b>

Provide methods in assisting of planning for our program. It includes the following functions:

create_grid

A* Search Algorithm 

heurisitic method

valid_actions

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
The first line of the csv file describes the global home position as lat0 37.792480, lon0 -122.397450. I extracted the values of lat0 and lon0 from the csv file. This is performed on [Line 132](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/a56a5e064f386e47a2ba4711355afd8f3943f7c1/motion_planning.py#L123)

#### 2. Set your current local position
I retreived the drone's current position in geodetic coordinates from self.global_position, and the global home position set from last step from self.global_home, then used the utility function global_to_local() to convert the current global position to local position. This is performed on [Line 145](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/a56a5e064f386e47a2ba4711355afd8f3943f7c1/motion_planning.py#L145)


#### 3. Set grid start position from local position
The original code hardcoded the starting point for the planning intitial coordinates. I changed this to be the current local position. [Line 158](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/a56a5e064f386e47a2ba4711355afd8f3943f7c1/motion_planning.py#L158)

#### 4. Set grid goal position from geodetic coords
I added (longitude, latitude) to direct the desired goal location. [Line 166](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/a56a5e064f386e47a2ba4711355afd8f3943f7c1/motion_planning.py#L166)

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
I added onto the A* implementation to include diagnoal motions on the grid that have a cost of sqrt(2). [Line 58](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/d08f2ffeada62f83afc195a3b63d699de74e28c7/planning_utils.py#L58) and [Line 91](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/d08f2ffeada62f83afc195a3b63d699de74e28c7/planning_utils.py#L91)

#### 6. Cull waypoints 
To prune the path of unnecessary waypoints, I implemented collinearity test and applied it to the path obtained from A* search. [Line 154](https://github.com/PercivalDEV/FCND-Motion-Planning/blob/8f298cfe3e5a8cf9501cb5b60fadcde3657b07f9/planning_utils.py#L154)



### Execute the flight
#### 1. Does it work?
It works!




