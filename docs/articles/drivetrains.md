# Drivetrains

Virtually every robot in the VRC program is built with a drive as the means of locomotion. It is important to understand the basic physics behind drives, and how to make and power them properly.

# Elementary Drive Physics

Drives come in many varieties, and rarely are drives ever exactly the same. Drives need to have the following properties:

### 1. Stability
This is essential to drives - if the drive falls over, game over. The key to making a stable drive is to ensure that the robot's **center of mass** is resting comfortably within the points of contact (AKA wheels). Also, the lower the COM within the drivebase, the more stable. Consider the following:

![drivecom](_media/drivetrains/drives-COM.png)

Which of these drives would be most stable? Think about it - if the wheels spun really fast, which drive's wheels would be least likely to slip out from under it? The middle one:

![drivecomtriangles](_media/drivetrains/drives-COM-triangles.png)

See how visualizing only the important parts provides a different way to understand the issue here. Which triangle, set on a table, would be hardest to 'knock over'? The middle one.

Now, notice how having a tall robot is like having a shorter drivebase, in this sense:

![drivecomtriangles](_media/drivetrains/wonky-drives.png)

The above drives are different sizes, but their stability is very similar. Clearly, having as wide a drivebase as possible is a strong way to ensure robot stability.

Also consider that the robot may have lifting parts, and the COM will change - sometimes the robot might be precarious! maybe the drive won't even be enough to stabilize it. Maybe build antitips?

### 2. Proper Speed-Torque Tradeoff
How fast do you want your robot to go? How strong does it need to be? These questions are linked. Remember,

`Power === Torque * Speed`

The more torque you have, the less speed, and vice versa. 

#### About possible internal gear ratios

>What are motor internals? [Watch an educational YouTube video by team 1961.](https://www.youtube.com/watch?v=W9JUJJ5ADEw)

TODO do some calculations.