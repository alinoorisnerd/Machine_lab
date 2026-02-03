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


## Thursday - 3 Feb

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



