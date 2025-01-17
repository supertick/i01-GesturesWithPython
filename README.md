i01 InMoov Servo Control and Gestures in Python.
=
Welcome to the how-to control your InMoov servo services in MyRobotLab(MRL) using python and creating gestures tutorial.

#INSERT IMAGE

This tutorial assumes that you have already have a basic understanding of using MRL and the InMoov services (i01).  
- Know how to launch servo services from the InMoov (i01) UI, calibrate and move your servos with the sliders in the servo services.

INMOOV SERVO SERVICES
= 
As you open up the default InMoov Servo services, you will see them displayed on the left side panel. 
- They are displayed with a Servo Icon, followed by the service names for each part.

![ServoServices0](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/8efaaadc-8526-4296-a853-af70d069bc26)

The names of these servo services is what will be especially important as we move onto python. 



INTRO TO PYTHON
=
You can access python from the tab on the left side. It will be in your service listing by default. 
![i01main1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/cb65f2df-41f2-4ede-9c3f-9c487263f5ea)

Since we will be experimenting and you may have other tabs open which launch with your i01 services, click "New" and enter a name. 
- "Test" for example.

![PythonNewFile1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/6b2e63fe-8790-4ee3-a0ba-3b0c987bfece)

Now you should have a new tab open for whatever you named the file. "Test".

![001-PythonTab1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/e5ff36b9-5454-43ea-af59-c05b9519ac00)






"#" In python
= 
If you are completely new to python, it is a good idea to remember the # symbol. 

![Hashtag](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/c03c05d0-f4a8-45d8-903e-59449f2ad4d2)

Using the hashtag symbol, we can let python know it should ignore any lines beginning with "#" and the text will turn green.
- This is useful for making notes for yourself or others within your code.
- You can also use this to disable lines of code that you don't want read. Useful for temporarily disabling lines or keeping the code still written out that you may want to use at a later time.

LINE SPACING IN PYTHON
=
Line spacing (How many blank lines between lines) will not matter in python. 
- You can spread lines out as much as you want to make things easier to find/manage.

![Linespacing](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/eca0ba88-62de-448d-9abd-2951c4e62ff5)

Execute / Run a script
=

To run a script you have written out, hit the "execute button".
![Execute1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/243661ae-afe6-4eee-9523-c6df9cd53b36)

You can run the following the example from the above image for yourself to test it. It will do NOTHING! :D

#THIS IS A TEST SCRIPT WITH NO FUNCTION, EXECUTE ME!


ADJUSTING SERVO SERVICE NAMES FOR PYTHON
= 

Python is very picky with names. It generally does not like the names of the i01 services as they contain too many dots. 

![ChangeNames0](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/70bf1d0f-a946-44ac-8194-2e8cdd889e18)

Make sure when using python to change the names of your servo services to use underscores " _ " instead of dots " . "
- i01.head.neck >>> i01_head_neck
- i01.leftArm.bicep >>> i01_leftArm_bicep
- etc, etc. 

Here is a list of all the current i01 InMoov servo services currently available at the time of writing this tutorial.

![Servos1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/9cd9e0e9-cfdb-4492-ada6-77b725090cd4)

CAPITALIZATION / CASE MATCHING MATTERS!
= 
If you using for example i01_head_neck , it CANNOT be written with a different case of letters. 

![CasematchingMatters](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/1c0d2496-72e8-4c0b-9c95-d421d704ebdf)

- It must be written with the same matching character case for python to know it is the same service.



ERROR
=
If you forget to change the service names accordingly, you will likely see a traceback error like this.

![traceback](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/213a07e9-c496-48e5-9b55-8b18c9e0479a)

Alternatively, if you do see errors at any time, the error will help you identify why there is an error and which line it can be found in.
- You will see the error listed in the bottom "console". 

![Console1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/95cfa139-faff-46da-930c-64693e4c1de6)

Here is another example of an error and how to identify it within the console. 
![TraceErrorHelp](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/930cf690-ac0f-4854-89a7-19c2f61dfebc)

In this case, the traceback error told us...
- The error occured in line 1. 
- i01_head_neck is not defined. This is because it does NOT currently exist. I have not started the i01.head.neck servo service yet.


SERVO MOVEMENT RECAP (Sliders VS Python)
= 
Movement ranges between ( 0° < 90 > 180° ). This will apply to servos with limited Min/Max settings as well and keep within your set limits. 

In the image below, you can see that I have my "i01_torso_midStom" servo limited to Min:60 / Max: 120.

![002limits1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/f23ce389-6268-4ff4-ae24-aa372cc0561c)


When moving the slider to the 0 position, it is moving the servo to my defined Min: 60 position despite still using a 0-180 range slider.

![MidStomSlider1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/c5ee905f-87d2-474e-bb82-f95e19446e57)

- Think of 0° as max rotation in one direction (according to your Min/Max limits)
- 180° as max rotation in the opposite direction. (according to your Min/Max limits)
- 90° will be your center position. (according to your Min/Max limits)

These same ranges will apply when moving your servos in python as well. Your servos will act the same way as the sliders.


.moveTo()
=
Using the .moveTo() command line, we will be adding the desired position we want the servo to move to within the "( )".
- Example: i01_torso_midStom.moveTo(180)

![003-midStom180](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/147d798e-2960-428b-8284-aabb0e732b6c)

You can see here, when I click back to the i01_torso_midStom servo service, it has moved the slider to the 180 position.

![004-midStomB](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/3d74e6fd-1d27-4130-85ba-2d4c588bf03a)

MOVING MULTIPLE SERVOS AT THE SAME TIME WITH .moveTo()
= 
You can move as many DIFFERENT servos as you want at the same time!

![MultiServo1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/2dc2f2c3-b669-4f5d-8c47-51a9baf4404e)

Moving the SAME servo more than once will be continued below in "THE IMPORTANCE OF SLEEP".


.rest() 
=
Using .rest() will return the servo to your defined rest position.
![Rest0](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/4ac194f9-026c-492a-84ff-3de7a4080993)

.rest() will function the same way as if you click the Rest button in the servo service.
![Rest](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/9d8cc71f-9509-4473-b0d0-0c7bdd4cc915)

This can make life easier for you if you don't remember all rest positions.





APPLYING SPEED LIMITS
= 
When changing the speeds of you servos, you are actually setting speed limits to further reduce the speed of a servo.

The speed limit settings range between ( 0 - 200 + None )

- 0 - Slowest (likely not moving at this speed)
- 200 - Fastest "while still limited"
- None - Removes all speed limits = FULL SPEED (MAX)

SIDE NOTE: The speed limits only range between 0-200 with the slider. It is possible to go beyond 200 with python.
- It is hard to tell you exactly what the max limit range will be as it will depend on your servos. 
- If you set it too high, you may not even notice a difference between the servos max speed and the limits applied.
- You likely won't need to go beyond 200, just it maybe possible. (You can experiment if so desiring to do so.)


.setSpeed()
= 
Using the .setSpeed() command line, we will be adding the desired speed limit we want set for the servo within the "( )".

![NeckSpeed](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/1450af15-95eb-44dc-80f4-f7c4bc67002f)

As you can see, the speed limit was also changed in the i01.head.neck servo service as well. 

![NeckSpeed2-1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/b8ba74f0-3521-4e62-887d-1b4fb14d827d)

Side Note: I'm not entirely sure at this time if the slider is bugged or this is intentional. 
- The speed limit is set to 100, but the slider is still at the prior speed limit position. (semi useful for remembering prior set speed regardless) 
- The speed limit IS being applied correctly.

.setSpeed(None)
= 
.setSpeed(None) will remove all speed limits from the servo. 

![SpeedNone](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/85ba2e06-ec17-4197-9a15-6a16ec49a807)

Again if going back to the servo service, you can see that it has changed the speed limit to Max.

![SpeedNone2](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/fedb3ab6-d255-445f-9b24-141c0eb37875)


.setMaxSpeed()
= 
Alternatively you can also use .setMaxSpeed() to accomplish the same speed limit removal as .setSpeed(None). 
- Either way will work fine, they are essentially the same thing.

![SpeedMax](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/c1378723-4cc0-4b09-8ceb-4c975c7d20e6)


SPEED LIMIT POSITIONING IN YOUR CODE
= 
The desired speed limit for a servo must be set prior to moving the servo for the limits to apply. 
- .setSpeed() will be written above the .moveTo() command.

![LimitPositioning](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/7efe5129-b9be-4023-a2bf-32859db1357a)


THE IMPORTANCE OF SLEEP
= 
sleep() will be essential for you to get used to using as it plays such a big role in creating gestures, amongst other things.

The sleep() command line is what you will add to your code to break servo movements apart and let python know that it can wait a certain amount of time and then move onto the next movement line.

You will add the desired time length within the "( )" to add a pause before python moves to the next lines. 
- You can use either milliseconds or seconds in the "( )" to create a pause/break.

![Sleeptimers](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/3b8231f7-5456-4b7e-b04b-6a9ffede0375)


The following examples will hopefully show you why sleep() is so important.

You will NEED to add sleep() to your code to let it know there is a break between movements of the same servo! You will see in the following example why !!!!!

- Example 1: Move to 180 > wait 3s > move to 0 > wait 2s > return servo to center.
- The sleep timers are what allows to servo to reach its position before moving to the next.
 
![Sleepexample1](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/2507a03b-3551-4213-8e8c-ff821fa32119)


THE BAD EXAMPLE (What NOT to do)
=
WARNING!!!! Do not attempt this example. 
- In this example, the servo will attempt to reach the 180 position and the 0 position at THE SAME TIME.
- Without adding a sleep() between the lines, python won't know that they are meant as two seperate movements.

![BadExample](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/a17d40ad-88f2-4617-bfa3-30fa86bfb69c)

Side Note: You likely won't break your servos if you forgot to include it.... but it is a good idea to try and avoid it.
- Things may get funny if you forget sleep().

Moving multiple servos to various positions
=
As mentioned earleir, you can move as many different servos as wanting at the same time. Now we will move 5 servos together.
- All servos to 180 > sleep for 5s > all servos to 0 > sleep for 5s > all servos to 90 > sleep for 0.1s.

![Multiservosleep](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/3e8d807a-7550-4e64-aeb5-0aacd002cd12)


Applying various limits to multiple servos movement stages.
= 

In this example, you can see how to apply speed limits + move multiple servos > sleep > repeat to your hearts content or until you go crazy. :D

![VariousStageChanges](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/8a2417fa-255a-46c9-9c31-de03084068fd)

Not enough sleep!
= 
You need to give the servo a reasonable enough time to reach its position before sending it to the next position.

- In this example, the .sleep() timer is set so short, the servo cannot reach the 180 posistion before moving to the 0 position.

![NotEnoughSleep](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/bb6df91f-da56-41b3-8a05-086395ed8655)

Tips for a good sleep!
= 

It will take some practice getting used to how long sleep timers will need for each servo to be able to reach from position to position.

![NotEnoughSleep2](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/89cfbd62-ac0c-4023-b8e9-38e5789dd2b3)

- Experiment with different length timers. 
- You will need a longer timer moving a servo from 0 to 180 than you would moving it from 0 to 90. 
- I suggest starting with slightly longer sleep times, run the code, reduce/adjust as needed, repeat until you are happy with it.

AUTO DISABLE TIMERS
= 
You will need to make sure your servos auto disable timers are long enough that the servo is able to reach its longest destination range. 
- 0-180 for example. If you servo can reach from 0 - 180 within 5 seconds for example you know it is safe.
- You can continue to reduce and repeat until you have found an ideal auto disable timer. 
- This can be a bit tricky once you apply different speed limits, so you will need to experiment.

![AutoDisableTimer](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/504ffb01-b31d-4c8c-9871-8c9a430eae28)

WARNING! - ADVANCED GESTURE AUTO DISABLE COMMANDS
= 
USE WITH CAUTION!!!!

![ServosAtRisk](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/1435675f-b96c-468e-bf9a-d00b4c320126)

You really should not use these until you are very compfortable playing around with your servos. 
- Auto disable timers are important as they help prevent your servos from burning out. 

With the following example, we can disable the autoDisable timer within python and also re-enable it.

![DangerZone](https://github.com/CyberSyntek/i01-GesturesWithPython/assets/81597534/28efe23e-507c-4055-afc3-e65662df6e07)

USE CASE: 
- Can be useful for when we need a servo to maintain power for longer than normal to hold a position.
  - Omoplate is an example of a servo that requires power to be held up. Once autodisable kicks in, it can come crashing down.
 
- Can use useful for when using slower speed limits to avoid autoDisable timer kicking in before destination reached. 

I strongly suggest you don't use this until you have played with ALOT of gesture creation and start getting more and more fancy with them. 
- .setAutoDisable(False) #Disable autoDisable.
- .setAutoDisable(True) #Enable autoDisable.

And that is all I am going to cover for individual line servo commands! HOWEVER, there are more options available still! .... but I'm hungry and need lunch. :D

=======================================================

SERVO GROUPS! 
=

*beep boop* Updates in progress!

=======================================================

SERVO GROUPS EXPLAINED
= 

*beep boop* Updates in progress!

=======================================================

DEFINING YOUR GESTURES (FORMAT AND SAVING)
=

*beep boop* Updates in progress!

=======================================================

IMPORTING YOUR GESTURES
=

*beep boop* Updates in progress!

=======================================================

MAYBE ASSIGNING VOICE COMMANDS TO YOUR GESTURES?
= 

*beep boop* Updates in progress!

=======================================================

NO IDEA, MAYBE MORE... o/ 

