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

![Uploading image.png…]()



