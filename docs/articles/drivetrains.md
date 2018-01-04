# Drivetrains

Virtually every robot in the VRC program is built with a drive as the means of locomotion. It is important to understand the basic physics behind drives, and how to make and power them properly.

# Elementary Drive Physics

Drives come in many varieties, and rarely are drives ever exactly the same. Drives need to have the following properties:

### 1. Stability
This is essential to drives - if your drive falls over, game over. The key to making a stable drive is to ensure that your robot's **center of mass** is resting comfortably within the points of contact (AKA wheels). Also, the lower the COM within the drivebase, the more stable. Consider the following:

![drivecom](_media/drivetrains/drives-COM.png)

Which of these drives would be most stable? Think about it - if the wheels spun really fast, which drive's wheels would be least likely to slip out from under it? The middle one:

![drivecomtriangles](_media/drivetrains/drives-COM-triangles.png)

See how visualizing only the important parts provides a different way to understand the issue here. Which triangle, set on a table, would be hardest to 'knock over'? The middle one.

Now, notice how having a tall robot is like having a shorter drivebase, in this sense:

![drivecomtriangles](_media/drivetrains/wonky-drives.png)