# Programming Roadmap

This article is a resource to help you plan out what you personally need to work on in learning to program in ROBOTC.
It is up to you to take responsibility for learning what you need to learn about ROBOTC in order to make the robot programs your team needs! The more you learn yourself, the better.

This website has many articles about lots of the ideas mentioned here, but not every item can be found here (yet). In order to learn more, ask a programmer, do research online, or experiment with ROBOTC and read its documentation. A combination of all these is probably the best way to learn.

Remember, you don't have to learn *everything* at once. Take it at your own pace, but make sure you have the goal to learn it all at some point!

### Programming Terminology
*basic*

Be familiar with the meaning of these terms.
  - source code
  - compiler / compiling source code
  - source control
  - syntax
  - executing a program
  - compiler errors
  - asynchronous vs. synchronous

### ROBOTC Constructs
*basic*

know how to perform the following.
  - setting up the motors and sensors with names
  - motor setting
  - sensor reading and setting
  - waiting for some amount of time
  - waiting until something is true
  - compile a program
  - find errors in a program
  - download a program, start / stop the program.

### C Constructs
*basic*

Be aware of the following essentials of C (not specific to ROBOTC.)
  - assignment expressions (e.g. using the = sign to set motor/sensor power)
  - if, if/else if/else, while, for

### Variables & data types
*basic*

Important, not-ROBOTC-specific knowledge about how to store information.
  - what is a variable?
  - when is a variable useful?
  - know the meaning of: declaration, initialization, assignment
  - know the primitive data types:
    - int
    - float
    - bool
    - other (char, short, long)
  - typedef

### Functions
*basic*

Also not-ROBOTC-specific knowledge.
  - what is a function?
  - when is a function a good idea?
  - identify the parts of a function:
    - return type
    - function signature
    - function body
    - paramaters / arguments
  - function execution order (what happens when a function is called?)

### Tasks:
*medium*

Tasks *are* ROBOTC specific.
  - what is a task?
  - what is the difference between a function and a task?
  - when is a task useful?
  - how to start / stop tasks.
  - the task limit.
  - what happens when a task ends?
  - what happens when the main task ends (even if other tasks are running)?
  - what happens if you try to run the same task more than once?
  - what happens if you run different tasks calling the same functions at the same time?

### Controlling Systems with Sensors
*medium*

  - what is the goal of a PID controller?
  - what is the significance of the P, I, and D terms of PID?
  - know how to make a proportion controller.
  - know how to make a PI controller.
  - know how to make a PD controller.
  - know how to make a PID controller.

### Working with Fultiple Files
*medium*

  - using the contents of file A from file B.
  - scope in ROBOTC. [-> helpful scope article](https://www.geeksforgeeks.org/scope-rules-in-c/)
  - `.c` vs `.h` in ROBOTC*

### Structs
*advanced*

  - what is a struct?
  - when would 

### Preprocessor
*advanced*

  - Making macros with `#define`
  - the `#ifndef #define #endif` pattern
  - Using `#pragma systemFile` and `#pragma` once
  - Moving the motors and sensors setup to a different file other than main, with a special pragma config.