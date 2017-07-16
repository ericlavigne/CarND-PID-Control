# CarND PID Control
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

Self-Driving Car Engineer Nanodegree Program

---

The car in the following video uses PID control to drive around a closed track.
PID control considers only three inputs:

* Offset from center of the road (Proportional)
* Average offset (Integral)
* How fast the offset is changing (Derivative)

[![project video](https://github.com/ericlavigne/CarND-PID-Control/raw/master/recording-thumb.png)](https://youtu.be/FEVOgNq8Syc)

These three aspects of the PID controller each have a separate role to play in controlling
the car. The Proportional term turns the car in the right direction to stay on track.
The Derivative prevents overshooting, so that the car drives more smoothly. The Integral
term corrects for systemic bias. Or at least that's the intent...

The car in the video above had no systemic bias. I still found the Integral term useful
for increasing the steering angle on sharp turns, in which the Proportional and Derivative
terms failed to bring the car back to center for several seconds.

Based on the intent of the Proportional and Derivative terms, the Proportional term should
keep the car turning in the right direction, and the Derivative term should reduce the
oscillations due to overshooting. Instead, I found that increasing either term helped to
keep the car turning in the right direction and that increasing either term too much would
cause oscillations. Such oscillations were especially difficult to avoid at higher speeds
and were the main reason that the car's speed is limited to about 60 MPH. Speeds of over
100 MPH are possible on this track with optimal steering.

I tuned the Proportional, Integral, and Derivative coefficients manually, changing their
values in small increments and checking if vehicle performance improved or degraded with
each small change. I found it helpful to start with low speeds and gradually increase the
vehicle speed as the parameters improved.

At higher speeds, the same change in steering angle causes a faster change in vehicle offset.
For this reason, I modified the algorithm slightly, multiplying the total PID error by 1/v.
This allowed the PID parameters to remain valid over a wider range of speeds.

*Note: Find the latest version of this project on
[Github](https://github.com/ericlavigne/CarND-PID-Control).*

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 
