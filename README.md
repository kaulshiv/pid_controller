# CarND-Controls-PID Writeup

### Steering Controller
I used a PID controller to control the steering of a simulated vehicle. The controller took the cross track error (CTE) as input . My process for choosing the gains of the controller started with choosing K<sub>p</sub>. I set the other gains to zero and slowly increased K<sub>p</sub> so that it didn't overshoot the center of the lane. To alleviate the oscillating or swerving from the center of the lane, I had to increase the K<sub>d</sub> gain. Since I didn't observe any systematic bias in the vehicle's steering, I used a modest integral gain. I clipped error values that were greater than 1 in magnitudes since the steering control only took inputs in the range `[-1,1]`. The final gain values were K<sub>p</sub>=`0.1`, K<sub>i</sub>=`0.0001`, and K<sub>d</sub>=`5.0`.

__

### Throttle Controller
Since I wanted to achieve smoother vehicle handling around turns, I also used a controller to modulate the throttle (acceleration). The throttle input also took values in [-1,1]. I updated this controller with the squared value of CTE. My rationale for this was that I wanted to ease up on the throttle when the car was off center, regardless of whether the car was veering off to the right or left. If the controller error was above a certain threshold I set the throttle value to `0.1`, otherwise I set it to `0.3`. I experimented with setting throttle values negative to decelerate, but found that the vehicle would brake haphazardly, leading to unsafe driving. 

I only used proportional gain of K<sub>p</sub>=`1.0` for this controller. I didn't use integral gain since once again there was no systematic bias in the control of the throttle. I also didn't see the need to add derivative gain since the thresholding based approach I took to setting the throttle seemed to lead to stable, non-oscillating error values.

__

### Results

A video of my controllers operating on a vehicle on a simulated track can be seen [here](https://www.youtube.com/watch?v=sgMc6TNXzBY)
 