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


For me I prefer to work on the Famous need for Speed Game . To me, the game is a core memory growing up and feels appropriate given the non-violent nature. At the sametime, the game-itself is based on racing and 
