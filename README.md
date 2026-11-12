# sonicrange-lcd
🛠️ Tech Stack & Hardware
Microcontroller: Arduino Uno (ATmega328P)   
media-88431984-5AB2-402E-837C-EC1003BB1C08.jpg

Sensor: HC-SR04 Ultrasonic Distance Sensor   
media-88431984-5AB2-402E-837C-EC1003BB1C08.jpg

Display: 16x2 Character LCD Module   
media-88431984-5AB2-402E-837C-EC1003BB1C08.jpg

Language: C++ (Arduino Framework)

Libraries: LiquidCrystal.h   
IMG_7793.heic

✨ Features
Real-Time Distance Tracking: Accurately calculates distances using high-frequency sound waves.

Dual Output Mode: Displays metrics simultaneously on a physical/simulated LCD screen and logs data to the Serial Monitor.   
IMG_7794.heic
+ 1

Beginner-Friendly Architecture: Clean implementation of pin configurations, pulse timing, and math conversions.

💻 Firmware Code
C++
#include <LiquidCrystal.h>
LiquidCrystal lcd(10,9,8,7,6,5); // Create an LCD object. Parameters: (RS, E, D4, D5, D6, D7)
const int trigPin = 12;[cite: 1]
const int echoPin = 11;[cite: 1]
float time, distance;[cite: 1]

void setup()
{[cite: 1]
  lcd.begin(16, 2); // Specify the LCD's number of columns and rows. Change to (20, 4) for a 20x4 LCD
  pinMode(trigPin, OUTPUT);[cite: 1]
  pinMode(echoPin, INPUT);[cite: 1]
  Serial.begin(9600);[cite: 1]
}[cite: 1]

void loop()
{[cite: 1]
  digitalWrite(trigPin, LOW);[cite: 1]
  delayMicroseconds(2);[cite: 1]
  digitalWrite(trigPin, HIGH);[cite: 1]
  delayMicroseconds(10);[cite: 1]
  digitalWrite(trigPin, LOW);[cite: 1]
  
  time = pulseIn(echoPin, HIGH);[cite: 1]
  
  distance = (time*.0343)/2;[cite: 1]
  
  // For Serial Monitor[cite: 1]
  Serial.print("Distance:CM ");[cite: 1]
  Serial.println(distance);[cite: 1]
  
  // For LCD Display
  lcd.setCursor(0,0);[cite: 2]
  lcd.print("Distance in CM");[cite: 2]
  lcd.setCursor(0,1);[cite: 2]
  lcd.print(distance);[cite: 2]
}
⚙️ How It Works
Trigger Phase: The Arduino sets the trigger pin low, then high for 10 microseconds to emit an ultrasonic burst[cite: 1].

Echo Capture: The pulseIn() function waits for the echo pin to go high and measures how long the sound wave takes to return[cite: 1].

Calculation: The travel time is converted into centimeters using the speed of sound formula: 
Distance= 
2
Time×0.0343
​
 [cite: 1].

Display Phase: The final value is printed to the serial console[cite: 1] and rendered on line 1 of the LCD panel[cite: 2].
