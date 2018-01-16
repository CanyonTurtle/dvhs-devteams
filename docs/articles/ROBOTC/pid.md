# PID

A PID controller, informally called a 'PID', is widely used in industrial life and in robotics. This is incredibly important to understand if you want your autons to be even remotely reliable.

The PID Controller solves challenges that come up when controlling a system. More on that later.

Before we begin, think about this problem: Using an encoder, or some other sensor, how could you bring an arm up to a target? Well you could use an if statement. Let's look at the following:

``` c
void moveArmToTarget( int target ){
    while(SensorValue[ArmEncoder] <= target){
        setArmPower(127);
        delay(10);
    }
    setArmPower(0);
}
```

Now there are a lot of things wrong with this. When you suddenly stop powering your Arm, there will be a ton of momentum that will cause you to overshoot (keep drifting past the target value). Additionally, *how can we hold the arm at the right place?* Here's a solution to hold it at the target:

``` c
void holdArmAtTarget( int target ){
    while(true){
        if(SensorValue[ArmEncoder] < target){
            setArmPower(127);
        } else {
            setArmPower(-127);
        }
        delay(10);
    }
}
```

If the arm is above the targeted value, it will power downwards. If it is below the targeted value, it will power upwards. This is still not the best solution though. The arm won't hold at the wanted target. It will instead oscillate between being above and below the target. How can we *get slower as we approach the right answer?*

With these difficulties in mind, let's learn about a PID controller, which solves these challenges for us.

## What is PID?

A PID controller is about controlling a system. This system could be, for instance, a robot arm's angle. There is a `target`, aka a place to reach, and a `current value`, the place right now. There is also an `error`, which is the `target - current value`, or the difference of the two places. A PID controller is a piece of code that *minimizes the error* of a system, or makes the error go down over time. It does so by answering 3 fundamental questions:

1. How far away is the current value from the target? **reducing the current error - used with P.**
2. What was the error in the recent past, over time? **accounting for past error - used with I.**
1. How quickly is the error decreasing right now? **preventing the future error - used with D.**

By answering these questions, a system can be controlled precisely. What you need to understand is that **when the error is minimized, the system is where you want it to be**. Therefore, we can treat the whole issue of getting our systems where we want them as a game of minimizing the error. Read on to see how to use PID controllers.

## Proportion

First lets go over the Proportional control aspect, or the P.

To try to gain some intuition for the solution, think about this question: How can we power a motor based on the targeted value AND our current sensor value?

Proportional control touches upon the idea of error. Remember, error is the difference between your targeted value and the current sensor value. In terms of code:

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
        delay(10);
    }
}
```

But, we can do better! Think about what this will be doing: we still have limited control over how much the arm is powering! For example, if we were using a potentiometer instead of an encoder, we would have a lot more values to work with, precisely 4096 values in 270 degrees of motion. 100 potentiometer values is a very small change. Would you really want to power your arm at 100 power when you are only 100 potentiometer values away? No!

The problem is, the error and the speed that you want are correlated, but the details aren't settled yet. Exactly *how fast should the power change, considering error?*

This challenge is solved by a constant. I'm sure you've talked about constants in your Math or Science classes before. If we make a constant, we can truly gain control over how much we want our arm to power. I will be calling my constant kP. k is often used to denote constants.


``` c
void holdArmAtTarget( int target ){
    float kP = 0.1;
    int error;
    int power;
    while(true){
        error = target - SensorValue[ArmPotentiometer];
        power = error * kP;
        setArmPower(power);
        delay(10);
    }
}
```

Now, we have achieved true power over our arm. As it approaches its target, it will slow down, and at its target hold a very small power to hold it at that target.

However, this method is not perfect. With a pure p control, even if the constant is tuned to perfection, there will still be some degree of undershoot or overshoot. To solve these, we need to use an integral and a derivative, respectively.

## Integral

BEWARE: SOME OF THE FOLLOWING WILL **NOT** MAKE SENSE WITHOUT UNDERSTANDING WHAT AN INTEGRAL IS AND WHAT IT DOES.

With a pure p control, it is very common to have an undershoot. What I mean by this is, for example, your arm is 100 potentiometer values below its target. But, because the p constant is for example 0.1, you are only powering your motors at 0.1*100 = 10 power! This will not move your motors to the targeted value. What can we do to stop this?

Like many other problems, we use calculus. In this case, we will be using calculus to examine the error vs time graph.

Try to imagine the error vs. time graph. In my mind, it is a decreasing, concave up function, kind of like an exponential function. Very similar to an exponential function actually, because due to the problem mentioned before, the SensorValue can never reach its intended target, so it would act almost asymptotic to the x-axis. Our goal is to eliminate this "asymptote", and have the error hit zero. To do this, we use, you guessed it, an integral.

In case you were curious, in terms of physics the official term for this integral we are using is abasement, or the integral of position. We are looking for how the arm is away from its target, but also for how long.

What would taking the integral of this error vs time graph give us? Recall that integrals accumulate y-values, or in this case error-values over time. By adding up the errors over a period of time, the integral will increase and we can power the motors.

First, let's make an integral variable, and an integral constant, same as the proportion constant. We will want to update this integral variable in the same ```while(true)``` as before. Also remember, integrals add up the ``functionValue * dT``. In our case, we don't really have to worry about the dT, because we can handle it in the constant we are going to make. But, conceptually, it is nice to keep. in out case, because there is a 10 millisecond delay between each loop, dT is 0.01 seconds.


``` c
void holdArmAtTarget( int target ){
    float kP = 0.1;
    float kI = 0.001;
    float dT = 0.01;

    int error;
    int integral;
    int power;

    while(true){
        error = target - SensorValue[ArmPotentiometer];
        integral += error * dT;

        power = error * kP + integral * kI;

        setArmPower(power);
        delay(10);
    }
}
```

Notice here, when setting the integral, I used the common ```+=``` notation. This syntax denoted the same as if it were to say ```integral = integral + (error * dT)```. This will handle the integral's accumulation over time.
