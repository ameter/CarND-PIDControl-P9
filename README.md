# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Reflection

#### Describe the effect each of the P, I, D components had in your implementation.

##### P (Proportional)
- Steer as a proportion of cross track error (CTE).
- Causes car to overshoot target path.

##### I (Integral)
- Steer as a proportion (P) of cross track error MINUS integral (I) (sum) of all CTEs.
- Takes all previous CTEs into account to gradually adjust steering to imperfections in the system over time.
- Used to compensate for imperfections in the system, such as such as steering alignment being slightly off.

##### D (Differential)
- Steer as a proportion (P) of cross track error MINUS temporal derivative (D) of the cte.
- Reduces overshoot by allowing car to steer less sharply based on the difference of the error in the current sample vs the previous sample.

##### Testing Results

Kp steers the car sharper based on how large the CTE is.  So, using only P caused the car the oscillate, increasinly overshooting the center until it crashed.

Here's a [link to a video showing the result of only using P-control](./writeup_images/p_only.mov)

Kd steers the car less sharply based on the difference of the CTE in the current sample vs the previous sample.  So including Kd in the controller reduced the overshoot observed in the P-controler above enough that the car was able to stay on the tack.

Here's a [link to a video showing the result of only using PD-control](./writeup_images/pid_control.mov)

Ki adjusts steering over time based on all previous CTEs.  Including it this implementation did not significantly improve the results.  This is most likely due to the fact that this implementation was executing in a simulator which was not susceptable to, nor did it artificially introduce, real-world imperfections such as steering alignment error, etc.

#### Describe how the final hyperparameters were chosen.

The final hyperparameters (P, I, D coefficients) were determined through manual tuning.  I really liked the twiddle approach and spent some time attempting to implement it for this.  However, while the basic implementation was very easy, the interaction with the simulator (programmatically resetting it, etc.) was not.  Given more time, I would have continued working on the twiddle approash, but due to time constraints and the need to move on to the next project, I resorted to choosing hyperparameters through trial and error.  I did, however, modify main.cpp to accept the hyperparameters as command line parameters, which greatly speeded the manual tuning process.  While I'm confident more optimal hyperparameters could be obtained programmatically through twiddle or SGD, the identified parameters were sufficient for to meet the requirements of this project. 

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
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

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

