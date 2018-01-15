# PID

Proportion, Integral, Derivative. This is perhaps the most important concept in Robotics, and is even widely used in industrial life. This is incredibly important to understand if you want your autons to be even remotely reliable.

I want to preface this by saying that the I and the D aspect of a PID will be incredibly hard to understand without understanding the basics of Calculus. I will do my best to explain it, but if you still do not understand, please just stick with a P control until you do understand.

Before we begin, I want you to think about this problem: Using an encoder, or some other sensor, how could you bring an arm up to a target? Well of course, you could use an if statement. Let's look at the following:

``` c
void moveArmToTarget( int target ){
    while(SensorValue[ArmEncoder] <= target){
        setArmPower(127);
    }
    setArmPower(0);
}
```

Now there are a lot of things wrong with this. When you suddenly stop powering your Arm, there will be a ton of momentum that will cause you to overshoot. Additionally, how do you hold it there? Here's a solution to hold it at the target:

``` c
void holdArmAtTarget( int target ){
    while(true){
        if(SensorValue[ArmEncoder] < target){
            setArmPower(127);
        } else {
            setArmPower(-127);
        }
    }
}
```

If the arm is above the targetted value, it will power downwards. If it is below the targetted value, it will power upwards. This is still a terrible solution though. What we will see here is not the arm holding at the wanted target. It will instead oscillate between being above and below the target. Now you can implement tons of different things to hold it up with a holding power using a threshold and all that nonsense, but there is a much better method, and you guessed it, a PID.

## What is PID?

A PID controller is about controlling a system. This system could be, for instance, a robot arm's angle. There is a `target`, aka a place to reach, and a `current value`, the place right now. There is also an `error`, which is the `target - current value`, or the difference of the two places. A PID controller is a piece of code that *minimizes the error* of a system. It does so by answering 3 fundamental questions:
1. How far away is the current value from the target? **current error - used with P.**
2. What was the error in the recent past, over time? **past error - used with I.**
1. How quickly is the error decreasing right now? **past error - used with D.**

By answering these questions, a system can be controlled precisely. Read on to see how!

## Proportion

First lets go over the Proportional control aspect, or the P.

To try to gain some intuition for the solution, think about this question: How can we power a motor based on the targetted value AND our current sensor value? 

Proportional control touches upon the idea of error. What exactly is error? Error is the difference between your targetted value and the current sensor value. In terms of code:

``` c
error = target - SensorValue[ArmEncoder];
```

Now, instead of using whether the Sensor's value is above or below the target, what if we use this error to power our motors instead? This will cause the arm to slow down as it approaches its target.

``` c
void holdArmAtTarget( int target ){
    int error;
    while(true){
        error = target - SensorValue[ArmEncoder];
        setArmPower(error);
    }
}
```

But, we can do better! Think about what this will be doing: we still have limited control over how much the arm is powering! For example, if we were using a potentiometer instead of an encoder, we would have a lot more values to work with, precicely 4096 values in 270 degrees of motion. 100 potentiometer values is a very small change. Would you really want to power your arm at 100 power when you are only 100 potentiometer values away? No!

Instead, let's make a constant. I'm sure you've talked about constants in your Math or Science classes before. If we make a constant, we can truly gain control over how much we want our arm to power. I wll be calling my constant kP. k is often used to denote constants.


``` c
void holdArmAtTarget( int target ){
    float kP = 0.01;
    int error;
    int power;
    while(true){
        error = target - SensorValue[ArmPotentiometer];
        power = error * kP;
        setArmPower(power);
    }
}
```




