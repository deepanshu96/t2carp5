# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---
In this project we implement Model Predictive Control to drive the car around the track. This time however we are not given the cross track error, would have to calculate that ourself! Additionally, there's a 100 millisecond latency between actuations commands on top of the connection latency.

### The Model
* We use a kinematical model in our project which neglects all the dynamic effects such as torque, inertia and other forces on the car. The model uses vehicles x and y coordinate, its velocity v, oriental angle, cross track error and error in the heading direction. The following equations are used in the model :-

- x_[t+1] = x[t] + v[t] * cos(psi[t]) * dt
- y_[t+1] = y[t] + v[t] * sin(psi[t]) * dt
- psi_[t+1] = psi[t] + v[t] / Lf * delta[t] * dt
- v_[t+1] = v[t] + a[t] * dt
- cte[t+1] = f(x[t]) - y[t] + v[t] * sin(epsi[t]) * dt
- epsi[t+1] = psi[t] - psides[t] + v[t] * delta[t] / Lf * dt

### Timestep Length
* N=10 and dt = 0.1 was chosen as it was mentioned in the course material. Also other values were tried but the previously mentioned values best suited the model.

### Polynomial Fitting 
* The coordinates were transformed to vehicles coordinate system and then a third order polynomial was fitted to the waypoints. The following transformation equations were used :-

- X = cos(psi) * (ptsx[i] - x) + sin(psi) * (ptsy[i] - y);
- Y =  -sin(psi) * (ptsx[i] - x) + cos(psi) * (ptsy[i] - y); 

### MPC with Latency
* The command sent from actuators to the vehicles have a latency delay of 100 ms, hence the values of the state varibles was first initialized then predicted 100ms into the future and passed as intial state to the state variable. This method took care of the latency delay issue thus encountered in the model predictive control. 






