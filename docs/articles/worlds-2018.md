# Lessons from World Championships

*Thoughts from Cannon about how to prepare to be a world-champion team.*

This document is going to be a little different, I am addressing this directly to you, development team members.

Over the past week, I had the opportunity to attend World Championships with our T, E, and A teams. Our teams had a losing record, which was a bummer, but I feel like we learned a lot of valuable lessons from the trip. I hope this document will not only give you an idea of what World Championships is like, but also help you to do better at all the tournaments your teams will be attending.

Here are three key points that I think Worlds tought me this year.

1. Make your team known.
2. Consistency is everything.
4. Have fun!

When we arrived to Worlds, lots of Northern California teams actually stayed in our hotel with us: 8000 and 315 teams, both prominent norcal teams, were both in the same lobby as us for most breakfasts, and we saw them all the time at the Kentucky Expo Center (KEC). It was fun to see familiar faces there, but as soon as we got to the convention center, we were surrounded by *hundreds* of teams we had never met before.

There were robots of all kinds: robots that were "meta": a reverse-double-four-bar, vertibar + roller intake, 4-bar mobile goal, and 4-motor drive. Robots that were unusual: 62A became infamous this weekend with their defense-only 8-motor-drive ramp-weilding defense bot. There were even teams that were relatively inept; some of the robots on our alliances could only do 3 or 4 cones per match (as opposed to 15-20).

It may seem like it would be impossible to make sense of the 100 teams in our division, but our team was instantly able to spot out several teams, based only on their reputation. We were amongst teams like 7700R, 315, 5327, 1961x, and 169C among others. All of these teams had created online presences for themselves, on VexForums, on YouTube, and in tournament. We had seen their reveal videos all year, and we knew they were high calibur.

Our matches went poorly (more on that later). When Alliance Selection came around, our teams were in angst; we wanted badly to be picked, because we felt like our high-calibur robots were underrated from our unlucky matches, and if only a strong team would pick us, we would be able to excel in eliminations.

but what suprised me was, that the teams with reputation (7700R for instance) were selected above other less-known teams, even if the lesser-known teams had capable robots and solid match records. This was because teams that had a reputation were a "safe bet", as opposed to teams like us who had relatively little online presence in terms of revealing the robot, and being known in the VRC community. This is when it was clear: the more connected, the more reputable, the more known a team is, the more opportunitites it has in Alliance selection.

This is my takeaway #1: **make your team known**. Some ways to do this:

- make reveal videos and publish them.
- reach out to other teams at tournament, ask to show them your robot
- make friends and contacts at every tournament
- try to make a favorable online presence within the VEX Community.

Now, let's talk about 5776T's absolutely terrible luck with qualifiaction matches (and what we could have done to prevent some of it).

We went 4-6 this year in quals, and it was a bit heartbreaking, honestly. Here is a summary of some of our mishaps:

### Match 1
Our opponent fell, and became completely sprawled across the 10pt zone, within auton. We couldn't score mobile goals, and lost by 2 points against a 1v2.

### Match 2
Our drive started to stall out, and our autostack wasn't strong enough, but we won the match.

### Match 3
Our opponents played defense on our robot by going inside our 10pt zone, and defending both of our robots from placing anything in that zone, causing us to lose by alot.

**interlude: we spent some time back at the hotel figuring out what was the problem with our drive, and we were able to diagnose it: one of our axles was bent, we had too much friction on the wheels, our motor controllers were suspicious, and we had wired the drive into ports 1 and 10 (not a good idea, put the least-used motors on 1 and 10, because the builtin motor controllers aren't very good and they cause a PTC trip easily).**

### Match 4
Our opponents were formidible, and our alliance was not strong, and our autostack code wasn't configured enough. We were unable to keep pace and we lost by 3 points.

### Match 5
We lost - we weren't able to get to the mobile goals fast enough, and we spent too long not scoring enough. We lost by 5 points.

### Match 6
We lost.

### Match 7
We actually won this match by alot.

### Match 8
At the start of the match, one of the rubber bands on our bar fell off, and we were unable to stack cones quickly anymore, so we lost by 2 points. We lost this match.

### Match 9
We won this match fair and square.

### Match 10
We won this match.

Now, we had all kinds of misfortune happen in our matches. But we still could have done some things to change the outcome:
- our autonomous code wasn't precise enough at depositing in the 20pt zone - it would get misaligned by the return trip of the cones, and by the cones themselves on the way over. We might have done better if we had solved this challenge differently before we got to Worlds, perhaps with more sensors or with a slimmer drive.
- Our maintenance and checking got lazy. We didn't ziptie down some of our bands, and we didn't check for rubber band integrity often enough to ensure they would work. We should have had a "Tuning Procedure", which involved checking the wires and rubber bands of the robot.
- We waited too long to fully appreciate that we needed to replace the Motor Controllers on our drive, and we had a misconfigured port layout that used ports 1 and 10 for the drive.
- Lithium Grease OP: we should have put lithium grease on all of our gears and between some spacers - we started doing this halfway through, and it totally helped. Lithium grease is really effective at reducing friction (hint: friction is likely to cause problems in drives and lifts). 
- Our driveteam worked overly hard, and got a bit tired during matches. Don't get me wrong, our driveteam did an amazing job, but everyone performs better on a good night's rest, plenty of food and water, and with taking breaks. It is important to mantain the competitors as well as the robot! It is my conviction that drivers prepare best with purposeful practice and with plenty of sleep.

All of these specific areas our team could have improved added up, and it had the effect of making our robot overall less consistent.

I heard it best from Mr. Technik, a prominent VRC mentor who I conversed with at Worlds this year (this is paraphrased, but it gets the point across). He told me that winning in VRC is not really focused on engineering: sure, there is design, progamming, and robotics, but those things can be learned in one semester of engineering classes at university. However, what VRC teaches that is unique is these things: how to manage and complete a project, how to prepare for failure, and how to make a consistent, repeatable system.

So There is my takeaway #2: **Consistency is everything**.

My suggestions for setting up consistency in your future competitive teams is to do the following:
1. Design your robot/code with the stresses of competition in mind. For instance, you should answer these questions:
  - how easy is it to replace motors, MCs, or sensors if things go wrong?
  - What about cortex/battery accessibility?
  - How protected are the wires from the feild, other robots, *and the robot itself?*
  - How quickly will repeated use of this robot cause failure in the motors/linkages?
  - How precisely does this have to be tuned? (shoutout to myself sophomore year, sorting out 2 orange rubber bands and 1 thin rubber band, ziptie-ing them precisely onto the puncher, so they were layered and positioned exactly the same way on either side, and literally 10 other things just on the puncher that had to be checked, or else literally every shot would miss. Hint: make your bot easy to tune. please...).
  - How easily can the robot be driven?
2. Design the software so it is easy to understand by everyone, re-use, tune, and revert. For instance:
  - write comments explaining why the code is written the way it is. This is extremely important to working in collaboration over long periods of time! You will write complex code, and you might not visit that code for months! Do you think you will easily remember exactly how that code works after 4 months? I doubt it. And commenting is helpful to get everyone on the same page with how the code works!
  - put re-usable code in functions.
  - If a function is being used in multiple places, take extra time to make sure you understand exactly how that function works, and what will cause it to succeed/fail. If you spend a short time rushing through functions A and B, and then function C relies on A and B, you might give yourself extra headache. Remember, the entire thing will only behave as expected if all 3 functions work. So spending time testing function C before you understand A and B could cause you to waste time realizing that all the random problems are caused by A and B, which you could have solved much more easily in isolation. This concept is called "Unit Testing".
  - Put values inside variables. For instance, if you want to power a lift with 100 power for a fast speed, you could do `#define FAST_LIFT_POWER 100` at the top, and then use `motor[lift] = FAST_LIFT_POWER`, which is much more readable and you will remember it later.
3. Organize the team! Come up with procedures for how your team will operate in a consistent manner. For instance, your team should formalize how they will operate with regard to the list below.
  - who will drive, scout, tune, etc... at tournament
  - how the robot must be cross-checked in tuning (making sure all the bands are in place, all the motors / MC connections are unbroken, etc...)
  - what match strategy will be attempted in different scenarios.

Hopefully these suggestions can help your team be consistent in tournament. Having a strong design means nothing without the fininshing touches, because the coolest robot doesn't win, the robot that works in every match, with a prepped driver and working code, is going to be the most likely to win. Your team needs to put in the work to get to this point, where the preparation is in place to go in to matches and tournaments with confidence and premeditated plans of action.

As soon as the alliance selection ended, and we realized that our time this year as a VRC competitive team was coming to a close (especially for us seniors - wahhhh), I think many of us felt dejected and were a bit unhappy with our run at worlds. But that feeling faded. Because after all, VRC is just a game. The real memories I will have of our worlds trip is when everyone made memes about my sprained ankle (haha, I got to scooter around all week). And I will remember alot of yelling "REEEEEE". I will remember ranting about the lack of a water game, losing at Fortnite, and shouting "I LOVE YOU KARTHIK" in the middle of the KEC stadium when he started announcing. I will remember that everyone came back to the hotel smiling and laughing, as as great friends and fellow teammates. 

This is takeaway #3. Even though we didn't win, we had a really, really fun time, and we learned alot. I hope that as you guys undertake competitive robotics, and whatever else you choose, that you will let fun find you along the way, because your attitude, not the outcome, will make the difference in how much you get out of robotics. I challenge you all to give it your best shot, and to make it fun!

-Cannon