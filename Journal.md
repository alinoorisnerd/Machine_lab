# **Machine Lab - Ali's Journal**

## Thursday - 29 Jan
For this assignment, we are required to control the speed of the 'sweep motion of the Servo, alongside triggering its movement using the push / tactile switch.

### Here is the circuit drawn:

![IMG_3568](https://github.com/user-attachments/assets/6a4712ec-af45-40b7-9444-818c157fa4ed)



### Image of the circuit itself :

![IMG_3567](https://github.com/user-attachments/assets/d91ff849-4d1a-4c6e-ad7b-a08a50492652)


### Code :

```
#include <Servo.h>

Servo myservo;

const int servoPin  = 9;
const int potPin    = A1;
const int buttonPin = A3;

int pos = 0;
int dir = 1;

void setup() {
  Serial.begin(9600);
  pinMode(buttonPin, INPUT_PULLUP);
  myservo.attach(servoPin);
  myservo.write(pos);
}

void loop() {
  if (digitalRead(buttonPin) == HIGH) {
    Serial.println("YES");

    int potVal = analogRead(potPin);

    int speedDelay = map(potVal, 0, 1023, 2, 25);

    myservo.write(pos);
    delay(speedDelay);

    pos += dir;
    if (pos >= 180) { pos = 180; dir = -1; }
    if (pos <= 0)   { pos = 0;   dir = 1;  }
  }

}

```
### Issues faced :
None. Having taken intro to IM and other courses, this was a fairly simple task.


## Thursday - 3 Feb (Extension granted to Class till 5th of Feb)

![IMG_3569](https://github.com/user-attachments/assets/783cfced-9542-4092-91b9-5e9b45eb177a)


For me I prefer to work on the Famous need for Speed Game . To me, the game is a core memory growing up and feels appropriate given the non-violent nature of the game. At the sametime, the game-itself is based on racing. 

<img width="512" height="512" alt="unnamed" src="https://github.com/user-attachments/assets/790d62b1-a2e9-4ae4-8242-1223d7f761bf" />

After having visited the installation from 2 years ago, which is based on the Joyland theme, I did happen to observe some faulty components. On the front of the frame sits the Mechanism on disply, and on the back of the frame sits the power management and wiring. Wires with tapped labels attached is something I am inspired by.
With heaps and heaps of wires, sorting them on the basis of color alone isn't feasible by itself.
Thereof, wirelabeling and cable management is a crucial aspect of built, which allows for debugging when time comes.

### Mechanism proposed :

![unnamed](https://github.com/user-attachments/assets/324c2efb-a9b3-4038-ab4a-9b370e801ede)

For the mechanism, I believe Wheels moving, and the car actually vibrating would be crucial compoents.
Sound and light follow as secondary elements. For the wheels , as shown in the drawing, wheels are attached to cogs and these cogs are driven by a centeral / bigger cog, which is driven by a single motor.
The second motor is used to drive half-weighted plated to add vibration as the car revs.


## Tuesday - 10 Feb :

For this particular assignment, we were tasked with finishing the in-class exercise. Even though I didn't attend the class taught on 5th of February, later durin the day I went through the lecture notes and finished the tasked assigned.
I wasn't handed the adapter or any of the materials (e.g L298 H motor driver). I sifted through stuff in the IM lab, behind the whiteboard on the rack, and completed the ration list.

<img width="494" height="655" alt="image" src="https://github.com/user-attachments/assets/c9177b96-f300-4177-a4cd-2dce724551c8" />


Once done, I stripped the wires from 12 V 60 W power adapter, and solder them to female Coaxial cable. For safety purpose, after soldering the connection, I tapped the ground and hot wire.

<img width="492" height="662" alt="image" src="https://github.com/user-attachments/assets/445e29a8-ead3-43b9-96da-412247109f2f" />


After this, I inserted wires of male coaxial cable to 12 V and ground terminal on the L298H motor driver. ENA, In1, and IN2 pins were attached to the arduino. 

ENA (Enable pin A) was attached to PWM pin 5 for altering motor speed.
IN1 was connected to PMW pin 7, and IN2 was connected to pin 6 for LOW.
Last but not the least, the motor's positive and ground terminal were connected to the Output 1, and output 2 of the H-bridge driver, respectively.

Following code was written inside Arduino to test drive the 12 V 650  RPM motor :

```
// Pin definitions
const int enA = 5;  // PWM pin
const int in1 = 6;
const int in2 = 7;

void setup() {
  // Set pins as outputs
  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
}
void loop() {
  // Rotate motor forward slowly
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);

  for (int speed = 0; speed <= 255; speed++) {
    analogWrite(enA, speed);
    delay(20); 
  }
  analogWrite(enA, 255);
  delay(2000);

  for (int speed = 255; speed >= 0; speed--) {
    analogWrite(enA, speed);
    delay(20);
  }
  delay(1000);
}

```

The motor spins as intended!
<img width="878" height="499" alt="image" src="https://github.com/user-attachments/assets/ccdbdb6e-ffb5-4bf0-ab69-cb08a56c9035" />


However, now the next stage was to prototype the proposed mechanism in the previous entry.
Since my concept is to drive the wheels using cogs and main motor, using a toy wheel and the hub attached to motor, I created the rotary concept where the wooden sticks tapped ontop acted as the 'teecth' of the code. As a result when the motor and the hub spun, it spun the wheel as well!

<img width="487" height="647" alt="image" src="https://github.com/user-attachments/assets/0bc132af-3b51-4e16-bf8e-4da4c16c0519" />


### Thu - 12 Feb :

## Prototype refinement - Bevel Gear CAD design  

To refine and better present my idea, I opened CAD software, and looked into Bevel Gear system. Bevel gear mechanism aligns with my rough sketch, proposed previously.
Base gear driving two other gears is what I want to achieve. Here is the basic implementation of Bevel gear system in CAD:

<img width="1311" height="680" alt="image" src="https://github.com/user-attachments/assets/00ec3092-6645-44be-8ac0-9c4b76d02239" />


<img width="732" height="592" alt="image" src="https://github.com/user-attachments/assets/0de6bed5-8b81-4366-a00a-5545afb450a2" />

In total, two pairs will act as two wheel for the car system, however; I am confused between opting for Satellite bevel system or a worm gear.
With worm gear, multiple Cogs may put stress on a single base gear, therfore will ask Professor Shiloh for his suggestions.

<img width="146" height="143" alt="image" src="https://github.com/user-attachments/assets/600d8c07-a95c-4f42-a6be-b5d460ae3b41" />

# Tue - 18 Feb :

## Building Da Thing!

For this assignment, we were tasked with building the mechanised version of our sketches. 
Me and my team identified three main components which were : the wheels, the moving road, and the engine. Since the engine happens to be the most time consuming, we decided to get started with it at the earliest.

We proposed multipe engnie ideas. One was to follow the tutorial online to origami a miniature paper version of V8 engine. The following youtube tutorial was a potential inspiration:

https://www.youtube.com/watch?v=13_4r95FAMk&t=328s&pp=ygUCdjg%3D

The other one being a 3D crank shaft based print.
Being made out paper makes the structure vulnerable to damage, especially due to the moving parts. Therefore, we opted for a 3D print, with the assumption that It will come out awesome!

Here is the design we made :

<img width="1216" height="980" alt="image" src="https://github.com/user-attachments/assets/d6bb7837-d7ac-404a-9fc0-e9d705895af0" />

<img width="668" height="1208" alt="image" src="https://github.com/user-attachments/assets/5b166bde-3fa4-4b92-ad1d-4e85aca15365" />

## Due process :

While printing, we realized that the piston heads, crankshaft, and other mechanism when scalled down didn't have quite the resolution. Infact, the bumpy edges would mess up the rotatary movement. After 3 prints, the fourth one came out right. However, imporantly, we did spend a lot of time designing the engine so that it can fit the hood of the car of a particular demension. The time after was dedicated to print and polishing.

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/c6062b44-e382-453e-bc4f-f8059f97f4f7" />
<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/4cec581e-f22d-4f5a-b0ff-8947f5501e86" />

## Attaching motor and conclusion:

One thing was realized after attaching the motor was that the mechanism required good anchor points on the crankshaft's ends. However, since we were unable to print the engine cover, the thing dangeled around.  Moreover, due to rough surface, the pistons would pop off. 
Our conclusion was to manufacture the engine out of somethign metallic, and to use WD-40. Infact this class should have a lecture of the greatness of WD-40!

It was learning process nonetheless, and most importantly, we made a huge progress. From here onwards, it will be easy for us to continue with the engine and having realized the defects and shortcoming, for the midterm, we will make it work!!!!

# Tue - 03 March :
## Main Mechanism for the project
The main mechanism that we identified for the project included the engine, the rotating symmetrical road and attached wheelbase (to give impression of the car doing a doughnut), and the car model. I decided to go for the engine since it was something that I wanted to build! Yes the war just stared and amidst skirmishes I find myself sticking around I.M Lab. Perhaps the pursuit of building a V8 did really make me care less about this frenzy situation.

I started off with the basic design principle. Since the other workshops and areas were closed, I had to make the best out of whatever I could get my hands on. I therefore opted for gold mine situated right next to professor Shiloh's office. Having some experience with the 3D printed crankshaft and pistons, I knew the somewhat mechanism and how to translate it from PLA to a much more metallic one. I drew basic shape on my notebook provided by professor, and with to and fro between the IM lab and the depot upstairs, I finally found the pulleys and bearing which would end up coming together just like my sketch :

<img width="3024" height="4032" alt="IMG_3779" src="https://github.com/user-attachments/assets/afe79f67-75ea-484c-9d2b-b29344040798" />

<img width="3024" height="4032" alt="IMG_3778" src="https://github.com/user-attachments/assets/2e82b0c0-7c70-48a7-9527-fa2634216333" />

I stared with one linkage : 

<img width="3024" height="4032" alt="IMG_3782" src="https://github.com/user-attachments/assets/6ec1bb2f-a244-4030-b8af-09950afca3c9" />

<img width="4032" height="3024" alt="IMG_3780" src="https://github.com/user-attachments/assets/43a6acb1-4a93-46ed-a216-0380ae11a169" />

Then I later progressed by adding more, and subsequent patterns saw the cranshaft take place. I added M3 screws to mimic piston and pisten heads. Initially the pulley would either jam up or would screw and come off. Therefore I added M3 bolts on both end of the pulley to give it enough space to spin but at the same time not move horizontally along the shaft. Folowing was the later progress :

<img width="4284" height="5712" alt="IMG_3785" src="https://github.com/user-attachments/assets/88541f5a-0d2f-4b95-b93a-c0ca8c16f56a" />

<img width="4284" height="5712" alt="IMG_3788" src="https://github.com/user-attachments/assets/88733a98-8928-4a86-b88e-8a2e5f5138f9" />

<img width="4284" height="5712" alt="IMG_3791" src="https://github.com/user-attachments/assets/fd927215-f8ad-4319-b4a6-43a86f7a84cb" />

Once done, I drilled some holes and added mpunting  stand - for the V8 turned W4 engine  -u sing L-brakets and wooden sheet.

<img width="5712" height="4284" alt="IMG_3816" src="https://github.com/user-attachments/assets/cf793cec-d6b7-432b-a132-4e9e6060dd07" />

Lastly I added straws to hold the piston (M3) screws diagonally to mimic the engine cylinder.


<img width="5712" height="4284" alt="IMG_3817" src="https://github.com/user-attachments/assets/3265f3ab-5440-4e03-96be-85735b903307" />





# Fri - 08 April :

It feels weird to be at home and yet still having to work on an IM project. Maybe I was a bit too attached to the I.M Lab!
Nonetheless, the meeting with processor went on to be 25 minutes long. Stuck in rush hour with poor reception thanks to the thunder storm -  we went over the basic expectations and I put forth the proposal of building a face deteciton based smart locking / unlocking mechanism for main door. It would concist of arduino ESP Cam module, some wires, 12 V motor, and some styrofoam to host the circuitry and keep it intact with the frame of the door.

# Fri - 15 April :
Having realized that tolerances between the door and the floor or the wooden frame would end up 'squishing' or 'breaking' the wires, I realized the limmitations. More or less, I also realized that a much more 'mechanized' endeavour would allign closely with the object of the class, therefore I opted for cardboard based automata design - which will honour the historical clocktower monument of my city. This will be powered by a rubber belt, and cam shafts translaing vertical movements to horizontal and back to vertical. The idea was to simply aimate the clocktower, trees, and the birds suspended in air with the help of copper wire. The vertical movement would help the birds flap ther wings and turn the clock hands.
The following sketch sort of realizes the concept : 
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/69adaea4-8704-4337-b7bd-cd780d47623b" />

# THU - 21 April :
## Problems - Problems - Problems :
The one main problem I faced repeatedly was the bending of cardboard and no proper contact point between the cam and cardboard piece responsible for moving the birds. Aligning it and make it firm and rigid on the skewer was a challenge. Over time the cardboard would soften up and would lose its structure.

<img width="192" height="144" alt="image" src="https://github.com/user-attachments/assets/313c63a8-4e76-4d1e-aadf-3ad70cfc67ab" />

This left me a bit frustrated, as I spent most of my time re-arranging cardbord on a skewer. Before I could finish, I decided to reconsider the project. It wasn't that I kept on quitting because I couldn't figure out the solution to the problem, but rather I stared to find the project being 'basic'. For me machine lab was about metals, motors, movement, mix of multimedia in a nutshell. However, cardboard automata wasn't just there yet.  I wanted to make something firm, compact, and mechanically flawless. So once again I started digging again. After thinking heaviliy, I realized I wanted something to move around, and something that moves around without any support!

# Fri - 29 April :
Once again, I embarked on a journey of finding a new project / inspiration. This was the third time. I still couldn't find anything, so I resorted to taking a quick break and watching cartoons to wind up my energy. Well the protagonist of the show had poster of Da Vinci bird on his bedroom wall, and I asked to myself what if ...
I never officially constructed a Da Vinici bird like model, and after research I found the design of Ornithopter online. You can wind it up, and make it fly just like a real bird!
Nothing could beat the excitement of constructing this particular project!

<img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/01ced45f-b56b-4c10-9c30-80aff753e266" />

I went out of the store to buy popsicle sticks, rubber bands, paper clips, hair pins. I went through the tutorial but found the first roadblock immediately when the popsicle sticks would split as I would try punching a hole through them. Maybe the sticks were of not the best quality? I tried from sharpest to dullest tool, nothing worked.
Moreover, the popsicles were a bit heavy. I doubt it would ever fly or even glide. I therefore took like weight straws, put them together, and got a basic structure working. 
After meeting with professor Shiloh, he advised me on refining the linkages on the wing. I therefore made a small cut in the wings and passed another straw to construct a linkage. I introduced bends to help it better mimic the human arm :

<img width="4032" height="3024" alt="IMG_4231" src="https://github.com/user-attachments/assets/70a72b1d-0df3-4a70-ba60-6a33679120d3" />

The paper clips and pins kept on sliding out of the straws. I therefore made loops of tape at the end or inbetween to act like plugs. This ensured that the pin could rotate and not come off :

<img width="4032" height="3024" alt="IMG_4232" src="https://github.com/user-attachments/assets/5dd38446-b831-45f9-a713-5d64f18c09ed" />

Loop of rubber band were made and andchored with to paper clip. Single rubber not used since it would break and the rubber bands I got my hands on are not the best either. Every twist and turn would introduced wear and tear so I made loops between three rubber bands to replace using a single one!
The following is the final result achieved :

<img width="4032" height="3024" alt="IMG_4230" src="https://github.com/user-attachments/assets/a4aaa0cb-32e0-4440-8d42-9ada3210c7e2" />




# TUE - 05 May :
I had the presentation on me but couldn't present due to Power cut few minutes before the class. The power has been going out now regularly at this same time - 15 minutes before the startin of the class. It presented me quite some difficulty as immense heat and lack of proper lighting makes work across all 5 classes pile up into a huge heap!











