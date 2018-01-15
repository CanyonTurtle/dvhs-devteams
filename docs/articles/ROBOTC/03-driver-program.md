# Simple Driver Program

Let's use all the information we just learned to make a simple driver control program!

In this program, we will be coding a robot with a simple 4 motor drive, 2 motor claw, and 6 motor lift.

Here is the wiring:

1 - Claw Motor 1
2 - Drive Motor 1
3 - Drive Motor 2
4 - Lift Motors 1,2: y-cabled through power expander
5 - Lift Motor 3
6 - Lift Motor 4
7 - Lift Motors 5,6: y-cabled through power expander
8 - Drive Motor 3
9 - Drive Motor 4
10 - Claw Motor 2

If you don't know what some of this means, please visit the wiring article!

Let's get to coding!

## Making the Correct File

Since we will be taking this robot to a competition, we must use VEX's competition template. Hit file, hover over "New... > " and select "Competition Template". If you see a bunch of comments, you did it right.

Here's a quick explanation of the competition template. When the controllers connect, the void pre_auton will run. If there is no comp switch connected, the program will jump to the task usercontrol(). 

## Motor and Sensor Setup

