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

## P - Proportion

Here is the fundamental solution:
``` c
error = target - SensorValue[ArmEncoder];
motor[port1] = 0.1 * error;
```
The above code is a complete **proportion controller**. Notice how the error is what drives the motor power. The more the error, the more the power! the constant, 0.1, is the tuning constant. This number can be adjusted to tune how the error affects the power. The higher the constant, the more the error will change the output.

Here is the same solution, in a more complex use case:
``` c
void holdArmAtTarget( int target ){
    int error;
    int kP = 0.1;
    while(true){
        error = target - SensorValue[ArmEncoder];
        setArmPower(kP * error);
        delay(10);
    }
}
```
Notice how this adds two layers onto the previous idea:
1. kP is just a named constant via an `int` variable.
2. instead of using `motor[port1]`, this uses `setArmPower` (a function).

## I - Integral

The **I** part is about fixing this problem: what if the system is really close, but not exactly there?
See this diagram:
![diagram](_media/not-powerful.png)
The power supplied from P control above is only 10 (not enough).
Even though the Proportion control from the last section usually works, when the value is *really close to the target*, Proportion control fails.

This is what **I** solves for us. Remember the key insight of Integral control: it *accounts for past error*.
The **I** step uses an `iAccumulator` variable to *keep adding up error over a long time, AKA using error from the past to influence the present*. What happens is, when the arm isn't at the target for long enough, the accumulator keeps growing and eventually it is big enough to raise the arm the rest of the way!

Here is the gist for the arm example:
```c
int error = 0;
int iAccumulator = 0;
int target = 3500;

while(true) {
    error = target - SensorValue[arm];
    iAccumulator = iAccumulator + error;
    motor[port1] = (0.1 * error) + (0.01 * iAccumulator);
    delay(25);
}
```
Notice above, the P control part is still here: `motor[port1] = (0.1 * error)`.

Now, the I part is added: ` + (0.01 * iAccumulator);`

Notice, the while loop will run 40 times *per second*, and so this line will run lots:

`iAccumulator = iAccumulator + error;`

This will grow iAccumulator, by adding the error over and over, until iAccumulator is big enough to help the arm get to where it needs to go.

Here is another integrated example:
``` c
void holdArmAtTarget( int target ){
    float kP = 0.1;
    float kI = 0.01;

    int error;
    int integral;
    int power;

    while(true){
        error = target - SensorValue[ArmPotentiometer];
        integral += error;

        power = error * kP + integral * kI;

        setArmPower(power);
        delay(10);
    }
}
```

Notice here, when setting the integral, I used the common ```+=``` notation. This syntax denoted the same as if it were to say ```integral = integral + error```. This will handle the integral's accumulation over time.

When using an integral, it is also important to consider whether a `maxIntegral`, or `iCap` is needed. The issue with the integral is that it can get too large (or too small). If the integral gets too large, imagine what would happen to the power. With too high (or too low) of an integral, we would only power the motors more than intended and cause more of an overshoot. To prevent this, and to make sure integrals only activate when needed, we set a max integral that the integral cannot pass. Here is the previous example modified with a maxIntegral.

This example incorperates a maxIntegral:
``` c
void holdArmAtTarget( int target ){
    float kP = 0.1;
    float kI = 0.01;
    float dT = 0.01;

    int error;
    int integral;
    int maxIntegral = 1000;
    int power;

    while(true){
        error = target - SensorValue[ArmPotentiometer];
        integral += error * dT;

        if(integral > maxIntegral) integral = maxIntegral;
        if(integral < -maxIntegral) integral = -maxIntegral;

        power = error * kP + integral * kI;

        setArmPower(power);
        delay(10);
    }
}
```

# How to Tune a PID:
Basic way:
1. set all constants except for P constant to 0. Set P constant to 0.1.
2. see how that works. Does is spring past? lower it. Does it fail to reach the value? raise it. Change the P constant until it works pretty well.
3. set I constant to 0.01, and make iCap 100.
4. see how that works. Does it have windup (missing the value over and over)? Lower I constant.  Does it not seem to move to the right value? raise I constant. Play around with iCap.
Advanced way:
Use this [link](http://smithcsrobot.weebly.com/uploads/6/0/9/5/60954939/pid_control_document.pdf) for help with tuning PID constants.

# Notes
1. Remember to *tune your constants*. It is simply not enough to make a PID. The constants determine how well it will actually work. Without them, nothing will work. 
2. When researching PIDs, don't be alarmed when you see terms you are not familiar with. Keep in mind that others like to call their variables different things. For example, instead of using k to denote the constants, many use the terms pGain, iGain, and dGain.
3. You might not need the I part! try just the P first. Simple is best.
4. There is more than one way to do this. Just because someone else's PID code looks different doesn't mean it is really that different. Look for the common threads in your code and others' code.
5. See number 1. :)