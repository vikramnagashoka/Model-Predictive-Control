# Model-Predictive-Control

### Model 
The model used here is a kinematic model which includes the vehicle's x and y coordinates, orientation angle, velocity, cross-track error and orientation angle psi error denoted as epsi. Acceleration and steering angle are produced as the outputs of the Actuator. The model combines the state and actuations from the previous timestep to calculate the state for the current timestep.

The Model predictive control has these following main steps:
 * We first define the duration of the trajectory by choosing N and dt. Here the values chosen are 10 and 0.1 respectively which mean that the optimizer considers time period of one second to determine a corrective trajectory.
 * Next we define the vehicle model given by the equations below
 
<img width="759" alt="model" src="https://user-images.githubusercontent.com/23641865/36012184-7f9d35aa-0d2a-11e8-8028-10f0dc2ae59a.png">

* Along with the model we specify the constraints for the actuators and the cost function as : 

<img width="334" alt="const" src="https://user-images.githubusercontent.com/23641865/36012182-7f876df6-0d2a-11e8-9cd8-0d293470faf3.png">

<img width="897" alt="cost" src="https://user-images.githubusercontent.com/23641865/36012183-7f8fcd70-0d2a-11e8-85e4-07dd3a0cb91f.png">

* Now with the state feedback loop in place, we pass the current state to the model predictive controller which calls the optimization solver to predict the control inputs that minimize the cost function as described above. Here we use IPOPT as the optimization solver.

## Pre-processing
To simplify fitting the way points to a polynomial, they are transformed to vehicle's perspective.

## Latency
To solve the problem of latency, a simple solution was to use the previous timestep's actuations. Although this solved the problem there were problems with cornering. To address this issue the an additional penalizer for the cost function involving velocity and steering angles was included. This resulted in much smoother driving. Also by limiting the max velocity to 50 the driving was smooth. Increasing to 70 still keeps the car on the road but cuts a few corners and hence 50 was used.
