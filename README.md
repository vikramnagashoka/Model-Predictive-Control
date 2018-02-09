# Model-Predictive-Control

Here the goal of this project is to predict the path of the car in the simulator provided. This simulator provides us with the steering wheel and acceleration values while the MPC controller predicts the track waypoints using this data. The model used for this is described below.
### Model 
The kinematic model includes the vehicle's x and y coordinates, orientation angle, velocity, cross-track error and orientation angle psi error denoted as epsi. Acceleration and steering angle are produced as the outputs of the Actuator. The model combines the state and actuations from the previous timestep (limited by N) to calculate the state for the current timestep based on the equations below:




This solution, as the Nanodegree lessons suggest, makes use of the IPOPT and CPPAD libraries to calculate an optimal trajectory and its associated actuation commands in order to minimize error with a third-degree polynomial fit to the given waypoints. The optimization considers only a short duration's worth of waypoints, and produces a trajectory for that duration based upon a model of the vehicle's kinematics and a cost function based mostly on the vehicle's cross-track error (roughly the distance from the track waypoints) and orientation angle error, with other cost factors included to improve performance.
