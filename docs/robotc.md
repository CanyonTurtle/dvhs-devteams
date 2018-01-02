# ROBOTC
### DVHS Robotics Novice Program 2017-2018
Programming is a fun and important part of robotics. This document will help you become an effective and prepared ROBOTC programmer for the VEX Robotics Competition. We hope that you will enjoy learning!

# Installing / Configuring ROBOTC


## Windows
1. [Create a Vex account and/or sign in:](https://www.vexrobotics.com/customer/account/login/) 
2. [Download ROBOTC](https://www.vexrobotics.com/downloadable/customer/products/)
3. Look under Downloads, choose ROBOTC for VEX Robotics 4.x (Windows EXE, for individual installation)
4. After the executable downloads, run it on your computer and follow the steps to finish installing.
5. Open ROBOTC (called ROBOTC for VEX Robotics 4.x)
6. Choose  Window -> Menu Level -> Super User
7. Choose  Robot -> Platform Type -> Vex 2.0 Cortex
8. Done! You are ready to write ROBOTC  programs for the cortex.

## Mac OSX
1. Set up your mac to also run windows by following these steps: https://support.apple.com/en-us/HT201468
2. After you have windows up and running on your mac, follow the windows installation instructions.




# Basics
Firstly, ROBOTC is a robotics platform that uses the C programming language as a means to program robots. 
C is a low-level imperative programming language - it has very direct control over the machine.
In order to learn to use ROBOTC, a basic understanding of C is required.

This guide mainly adds ROBOTC knowledge, with some C-specific ideas mixed in. You will be greatly assisted if you supplement this reading with [our favorite online C tutorial](https://www.tutorialspoint.com/cprogramming/c_program_structure.htm).

You don't need to understand the whole language - this document shows some use cases so you can get a feel for what you need to learn.

Okay, so you have ROBOTC installed. Let’s open it and make a new file, which should create this:

``` c
file1.c
task main()
{



}
```

First off, understand that task main() is the ‘entry point’ of the program. As soon as the cortex turns on and connects, it runs the contents of this file and will start executing (doing) the lines you add, from top to bottom, right inside the first { .

You can save all files with the extension ‘.c’, which means the file is a c ‘source’ file. The term 'Source code' refers to the human-readable code being typed.

Let’s get moving! We should try powering the motor corresponding to port1 on Cortex:

``` c
// motorMover.c
task main()
{
  motor[port1] = 127;


}
```

We have just set the power level of port1 to 127 (maximum forward power). Understand that setting the power level on a motor port is like toggling a switch - that port will keep being 127 power until some other statement changes the power to something else.

What if we want the motor on port1 to be powered for three seconds, then reverse-powered for two seconds, then stop?

``` c
// timedMotor.c
task main()
{
  // forward
  motor[port1] = 127;
  wait1Msec(3000);

  // reverse
  motor[port1] = -127;
  wait1Msec(2000);

  // stop
  motor[port1] = 0;
}
```
Here we can see two new parts of ROBOTC: 
`// comments`: lines that look like this. Comments are useful for documenting (explaining) your code while you go. Documenting helps you remember what you did later on, and helps other people understand what your code is supposed to do.
wait1Msec(int time); This command waits for some amount of time. The command must be supplied with a time, which must be an integer.

If-Else, While
Note that the previous program will only run once and then stop. Perhaps we want a program to keep running for the entire duration that it is on, maybe forever? We also might want to change our program depending on user input, or other conditions, perhaps a sensor. These help us accomplish more advanced goals in ROBOTC:
- [If-else statements](https://www.tutorialspoint.com/cprogramming/if_else_statement_in_c.htm)
- [While loops](https://www.tutorialspoint.com/cprogramming/c_while_loop.htm)

Please read the above links!

The following example uses the while loop and if statement, as well as user input. For instance, we could continually check if a user has pressed a button to determine if a robot’s claw should open or close.

``` c
// clawControlLoop.c
task main()
{
  // keep going forever
  while(true) {
    
    // if the user presses button 5U
    if (vexRT(Btn5U) == 1) {
      motor[port1] = 127;
    }
    // if the above didn't happen, do this
    else if (vexRT(Btn5U) == 1) {
      motor[port1] = -127;
    }
    // if all the above failed, lastly do this as default.
    else {
      motor[port1] = 0;
    }
  }
}
```

The above code will keep doing the following forever:
Check if button 5U is pressed, and if so, power the motor forward
If button 5U wasn’t pressed, but button 5D was, power the motor backward
If neither button was pressed, the motor will be set to 0.
Remember that if you don’t set the motor back to 0, it will keep powering what it was set to last (unless you turn it off).

Note that vexRT(Btn5U) will return (run and give back the answer of) either 1 or 0 depending on if the user is pressing the button or not. Note this shorthand for button input:

``` c
if(vexRT(Btn5D)) {
  // something...
}
```

Since the C language treats 1 as true when using it as a conditional (the part inside the parentheses of the if-else statement or while loop), you can omit the == 1 if you prefer.
Variables
Storing information is really useful. Use this external resource to learn [what a variable is, and how to make them in C](https://www.tutorialspoint.com/cprogramming/c_variables.htm).

Now, let’s see a use case of variables. Perhaps, storing the user’s joystick input for driving?

``` c
simpleDriverProgram.c
task main()
{
  int leftPower;
  int rightPower;

  while (true) {
    
    // store user input into variables
    leftPower = vexRT(Ch1);
    rightPower = vexRT(Ch2);


    // use the variables to power motors!
    motor[port1] = leftPower;
    motor[port2] = rightPower;
  }
}
```

This code has several key things going on:
A `while` loop - that keeps going forever. Remember that while loops check the condition at the top, and if it is true, the while loop’s body inside the { ... } will execute once, and the entire process repeats until the top condition is false.
Two int variables: leftPower and rightPower, being used to temporarily store user input. The analog channels can return any number between -127 and 127, corresponding to the user pressing fully back or fully forward, so the answer is stored in the int type.
The use of vexRT(Ch3) to read user input. Ch3 corresponds to the analog channel on the left:


hi
