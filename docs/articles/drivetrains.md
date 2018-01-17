# Drivetrains

Virtually every robot in the VRC program is built with a drive as the means of locomotion. It is important to understand the basic physics behind drives, and how to make and power them properly.

# Basic Drive Considerations

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

### 3. Room for the Lift, Cortex, Manipulator, etc...
your drive kind of, majorly depends on what your robot is supposed to do. Make sure you know where your lift towers are going - often you can re-use your lift tower bracing as your drive bracing. The Cortex can often be mounted on the drive too, preferably with [rubber links](https://www.vexrobotics.com/275-1029.html).

### 4. Build Quality
The key to building nice drivetrains is to keep them as simple as possible. Can you build a drive with 6 7-segment c channels? perfect. simple enough, and pretty light. Make sure the [Spacing is On-Point](articles/refining-build-skill?id=know-thy-spacing) as well. If you can keep the drive C - channels mounted with C channels running across the drive sideways, this is almost always preferable - it simply lines everything up neatly. It is up to the designers though - there countless ways to solve this problem!

Also, every wheel and gear's screw or axle should **always** be supported by either a bearing or a motor on each side. If there is no  bearing / gear, the friction will make the drive far less effective.

Another important consideration is: if you use gears, there should be almost no idler gears (any gear that's not the input or output, basically).

![gearpic](_media/drivetrains/gearing-drive.png)

> This drive illustration is missing a lot - the second metal side, any spacers, also it's not real. This is simply to illustrate a point, not to show a perfect drive.

Notice how with simply moving the motor placement, you can reduce the amount of idler gears. You can alternatively link drive sides together with chain, or you could not link them at all. That brings us to...

### 5. Linked Sides
Should a drive have linked sides? it depends. The pros:
- if one wheel is off the ground, the side still has 2 motor's worth of power
- the wheels are guaranteed to spin at the same speed on a given side - the drive is more likely to move in a straight line without programming assistance

The cons:
- linking the wheels adds friction
- it's a teeny bit heavier
- less space for the lift towers to be inside the drive. You might have to get creative with the linking.

Consider these tradeoffs. Maybe you can get away with not linking the drive.

### 5. Gear Linked or Sprocket and Chain Linked?
At first glance, gears and sprockets appear to do the same job: transmit motion from the motor to another point on the robot (in this case the wheels on our drivetrain).

Pros for Gears:
- Can be more mechanically efficient considering how they do have as much "play" as sprockets
- With a large selection of gear sizes and thicknesses, can be adaptable to many situations
- No chain to snap or get caught

Cons for Gears:
- When using in a drive train, it is inefficient to have a large "chain" of gears as seen in the above pictures
- Gears need more vertical clearance and consideration must be made about the contact with field and game object

Pros for Sprockets:
- Better than gears for transmitting power over distance
- May be optimal for linking the front and back of your drive train together if you put sprocket, motor, and wheel on the same axle
- You will have no "idler" wheel or sprocket in that configuration

Cons for Sprockets:
- Sometimes the spacing between the sprockets may not result in an integer number of chain being used, resulting in the requirement of a tensioner.
- Adding a more than 2 sprockets especially if all of them are co-linear may result in an uneven tension on the sprockets not on the end of the loop.
