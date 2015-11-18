
11/16/15
Began coding experiments. I first started out simple: isolate the three colors in an RGB LED. In the code below, I defined a brightness variable after establishing my connections on the arduino and breadboard. In void loop, I experimented with combining the values to understand how the LED worked. Right now, the LED would shine red, as the green and blue values are set to 0.
--------------------------------------------------------------RGB ISOLATION
int redPin = 11;
int greenPin = 10;
int bluePin = 9;
int brightness = 75;

void setup() {

  Serial.begin(9600);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {

analogWrite(redPin, brightness); //turn off red pin
analogWrite(greenPin, 0); //turn off green pin
analogWrite(bluePin, 0); //75 to blue pin
}
--------------------------------------------------------------

I then wanted to experiment with an easier way to view the color blending. Attaching three potentiometers to the A0, A1, and A2 pins, I took code that assigns each potentiometer to a color, an experimented with the more hands on approach to the changing colors. I still don't fully understand the extra variables in the code below, so I hope to study up on those to utilize them later in this project.
http://www.silvinopresa.com/arduino/rgb-led-common-annode-controlled-by-potentiometers-and-arduino/


--------------------------------------------------------------THREE POT RGB CONTROLLER
int redPin = 11;
int greenPin = 10;
int bluePin = 9;
int brightness = 75;

int redPot = A0;
int greenPot = A1;
int bluePot = A2;

int readValue_red; //declare variable to store the read value from the potentiometer which controls the red LED
int readValue_green;
int readValue_blue;

int writeValue_red; //declare variable to send to the red LED
int writeValue_green; 
int writeValue_blue; 

void setup() {
  // put your setup code here, to run once:
  pinMode(redPot, INPUT); //set potentiometer for red LED as input
  pinMode(greenPot, INPUT);
  pinMode(bluePot, INPUT);


  Serial.begin(9600);
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
//
//  analogWrite(redPin, 30); //turn off red pin
//  analogWrite(greenPin, 30); //turn off green pin
//  analogWrite(bluePin, 30); //75 to blue pin

  readValue_red = analogRead(redPot); //Read voltage from potentiometer to control red LED
  readValue_green = analogRead(greenPot); 
  readValue_blue = analogRead(bluePot);

  writeValue_red = (5. / 255.) * readValue_red; //Calculate the value to write on the red LED (add point to change to float point)
  writeValue_green = (5. / 255.) * readValue_green;
  writeValue_blue = (5. / 255.) * readValue_blue;

  analogWrite(redPin, writeValue_red); //write value to set the brightness of the red LED
  analogWrite(greenPin, writeValue_green); 
  analogWrite(bluePin, writeValue_blue);
}
--------------------------------------------------------------

Next steps:

- Write code to read the values each of the three potentiometers output values.
- Create exercises for blinking LED's and color changing.
- LED matrix?
- Bring in ceramic prototype and experiment with what brightness values are needed to shine through.
- 



11/18/15

9:35am

"avrdude: stk500_recv(): programmer is not responding"
"avrdude: stk500_getsync() attempt 10 of 10: not in sync: resp=0x00"

Code is failing to upload to the arduino. I expected it to upload with no problem but something seems to be in the way. I'm working with an Arduino mini so I assume that the problem lies with it not hooking up properly with the breadboard- as they are now one piece.
-Solved problem by specifying that the arduino is a micro, not a standard.

10:59am
Arduino finished uploading but the lights on the board won't turn on. Looking at the board I think I haven't specified the LED's to the right pins. Looking at the board, my LED's turned on after I switched them around. The power was connected to ground!!! !
