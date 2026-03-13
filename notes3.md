Up counter
Down counter
Up/down counter

-Power electronic basics


Inverter


TRansformer
Step-up voltage
Step-down voltage

ISR

# Arduino / Embedded Programming Commands (Interview Revision)

Important Arduino functions commonly asked in embedded / Arduino interviews.

| Command | What It Does | Where Used | Example | Explanation |
|-------|-------------|-----------|--------|-------------|
| `pinMode()` | Configures a pin as INPUT or OUTPUT | Usually in `setup()` | `pinMode(8, OUTPUT);` | Sets pin 8 as output so it can control devices like LEDs or relays |
| `digitalWrite()` | Sends HIGH or LOW signal to digital pin | `loop()` | `digitalWrite(8, HIGH);` | Turns ON a device connected to pin 8 |
| `digitalRead()` | Reads HIGH or LOW signal from digital pin | `loop()` | `buttonState = digitalRead(2);` | Reads state of button connected to pin 2 |
| `analogRead()` | Reads analog voltage from sensor using ADC | `loop()` | `value = analogRead(A0);` | Reads sensor value from analog pin A0 (range 0–1023) |
| `analogWrite()` | Generates PWM signal to control power | `loop()` | `analogWrite(9,128);` | Controls LED brightness or motor speed |
| `delay()` | Pauses program execution for given time | `loop()` | `delay(1000);` | Stops program for 1 second |
| `Serial.begin()` | Starts serial communication with PC | `setup()` | `Serial.begin(9600);` | Initializes communication with Serial Monitor |
| `Serial.print()` | Prints data to Serial Monitor | `loop()` | `Serial.print(value);` | Displays data without new line |
| `Serial.println()` | Prints data with new line | `loop()` | `Serial.println(value);` | Displays data and moves to next line |
| `attachInterrupt()` | Executes function when interrupt occurs | `setup()` | `attachInterrupt(0, ISR, RISING);` | Triggers function when external event occurs |
| `map()` | Converts value from one range to another | `loop()` | `map(sensor,0,1023,0,255);` | Converts sensor value to PWM range |
| `constrain()` | Limits value within range | `loop()` | `constrain(speed,0,255);` | Ensures value stays between min and max |
| `millis()` | Returns time since Arduino started | `loop()` | `if(millis()>1000)` | Used for timing without blocking program |

---

# Core Arduino Program Structure

| Function | Purpose | Example |
|--------|--------|--------|
| `setup()` | Runs once when Arduino starts | `void setup(){ pinMode(8, OUTPUT); }` |
| `loop()` | Runs continuously | `void loop(){ digitalWrite(8,HIGH); }` |

---

# Example Program (Fire Detection System)

```cpp
int sensor = A0;
int relay = 8;

void setup(){
  pinMode(relay, OUTPUT);
  Serial.begin(9600);
}

void loop(){

  int value = analogRead(sensor);

  Serial.println(value);

  if(value > 500){
    digitalWrite(relay, HIGH);
  }
  else{
    digitalWrite(relay, LOW);
  }

}


```
Explanation:

Sensor connected to A0

Arduino reads sensor value using analogRead()

If fire detected → digitalWrite() activates relay

Relay turns pump ON

----

2️⃣ ISR (Interrupt Service Routine)

ISR is related to interrupts.

First Understand Interrupt

Normally a microcontroller runs code line by line.

Example:
```
loop()
  read sensor
  check condition
  delay
```
But sometimes an event happens suddenly.

Example:

button pressed

sensor triggered

timer event

Instead of constantly checking, we use interrupts.

Interrupt Concept

When an event occurs:

CPU stops current program
↓
executes special function
↓
returns to main program

This special function is called:

ISR (Interrupt Service Routine)
Example

Imagine a fire alarm system.

Normal program running.

Suddenly flame detected.

Interrupt triggers:
```
ISR runs immediately
Example Code (Arduino)
void setup(){
  attachInterrupt(0, fireDetected, RISING);
}

void fireDetected(){
  digitalWrite(8, HIGH);
}
```
Why Interrupts Are Useful

Interrupts are used when:

quick response required

real-time systems

avoid constant polling

Example:

emergency systems

timers

communication systems



On Arduino Nano (ATmega328P):

# Digital Pins D0–D13 → GPIO

# Analog Pins A0–A5 → Also usable as GPIO

# Analog Pins A6–A7 → Analog input only (NOT GPIO)

So the correct understanding:

## GPIO (General Purpose Input Output)

GPIO are configurable pins of a microcontroller that can act as **input or output** to interact with external hardware such as sensors, LEDs, relays, or motors.

### GPIO Pins in Arduino Nano

| Pin Type | Pins | Usage |
|------|------|------|
| Digital GPIO | D0 – D13 | Used for digital input/output |
| Analog Pins (also GPIO) | A0 – A5 | Used for analogRead(), but can also act as digital pins |
| Analog Only Pins | A6 – A7 | Only analog input, cannot be used as digital GPIO |

### Example

Sensor reading:

```cpp
int sensorValue = analogRead(A0);
```

The primary languages for hardware and embedded programming are
C and C++. While other languages like Rust are gaining traction for safety, C and C++ remain the industry standards. 
Why C and C++ are the "Standard"
These languages are dominant because they are designed to work as "portable assembly". 

    Direct Hardware Access: They allow programmers to manipulate specific memory addresses and hardware registers directly using pointers and bitwise operations. This is essential for controlling pins, timers, and communication protocols like SPI or I2C.
    Minimal Resource Usage: Embedded systems often have extremely limited RAM (sometimes only a few kilobytes). C and C++ are compiled directly into machine code with minimal "runtime bloat," making them highly memory-efficient.
    Deterministic Performance: In real-time systems (like car brakes or medical devices), a program must respond within a precise timeframe. Unlike Java or Python, which have "garbage collectors" that can randomly pause the program to clean up memory, C and C++ give the developer full control over when and how memory is used.
    Universal Support: Almost every microcontroller ever made comes with a C or C++ compiler. This makes code highly portable across different hardware 
    ```

    7️⃣ Interview Explanation

If interviewer asks:

“What is setup() used for?”

You say:

setup() runs once when the microcontroller starts and is used to initialize hardware such as configuring pin modes and starting serial communication.

void setup(){

  pinMode(A0, INPUT);
  pinMode(8, OUTPUT);

  Serial.begin(9600);

}

pinMode which is which pin is output whic is input
serial.begin monitor sensor value, serail comm. with pc

setup ke sath bhi void aayega

Your Code
void setup(){
pinMode(A1, INPUT);
pinMode(9, OUTPUT);
Serial.begin(sensor number);
}
Mistake

Serial.begin() does not take text or variable names.

It takes a baud rate.

# Baud rate = communication speed between Arduino and computer.

Most common value:

# 9600


3️⃣ Why Variables Are Declared Above setup()

Because they must be visible to both setup() and loop().

int sensorValue;
int relayPin = 8;
int threshold = 500;


5️⃣ Analog vs Digital Pin Naming

You asked a very good question.

Analog Pins

Must use:

A0 A1 A2 A3 A4 A5

Example:

analogRead(A0);

Because these pins are connected to ADC hardware.

# Analog Pins, useA with it
# Digital Pins, Just use the number.

Example:

digitalWrite(8, HIGH);

Not:

D8

Arduino internally knows it is digital pin 8.


# Variabel declaration

Hum jin pin ko use karte hain ya variable for storing data to ue in a if condition,
we declare them before


# we can do
analogRead(A0);

but we declare ,
int sensor = A0;


in loop,
sensorValue = analogRead(sensor);


[sensorValue also decalred bfore btw]

int Button= 2;
int LED= 13;

void setup(){
pinMode(Button,INPUT );
pinMode(LED,OUTPUT);
Serial.begin(9600);
}

void loop(){
if(Button=HIGH){
LED=HIGH;
}else{
LED=LOW;
}
Serial.print("Done monitoring")
}


----
int Button = 2;
int LED = 13;

void setup(){

  pinMode(Button, INPUT);
  pinMode(LED, OUTPUT);

  Serial.begin(9600);

}

void loop(){

  if(digitalRead(Button) == HIGH){
    digitalWrite(LED, HIGH);
  }
  else{
    digitalWrite(LED, LOW);
  }

  Serial.print("Done monitoring");

}


Assignment operator, semicolon,not using read write whihc is essential


Nice try 👍 — but here you misunderstood how delay() works.
delay is not a condition, it is a function that pauses the program.

So this part:

if(delay>1)

is not valid.

How delay() Actually Works

delay(time) simply stops the program for given milliseconds.

Example:

delay(1000);

means:

wait 1000 ms = 1 second


Correct logic for blinking using loop

int LED = 13;

void setup(){

  pinMode(LED, OUTPUT);
  Serial.begin(9600);

}

void loop(){

  digitalWrite(LED, HIGH);
  delay(1000);

  digitalWrite(LED, LOW);
  delay(1000);



}


delay (1000);--provides me delay of 1 second
then write another state

delay() blocks the CPU
microcontroller cannot do other tasks

int LED = 5;

void setup(){

  pinMode(LED, OUTPUT);

}

void loop(){

  analogWrite(LED, 125);

}

Half brightness code kyonki analgwrite ki value 0 se 255 aur red ki 0-1023 tak



Imp baat jo bhul gaya that

3
5
6
9
10
11

digital pins , d0-13
analog a0-aa5  6,7 only analgo
baki sab gpio

d3,5,6,9,10,11  ye PWM only

int Button = 2;
int Relay = 8;

void setup(){

  pinMode(Button, INPUT);
  pinMode(Relay, OUTPUT);

  Serial.begin(9600);

}

void loop(){

  if(digitalRead(Button) == HIGH){
    digitalWrite(Relay, HIGH);
  }
  else{
    digitalWrite(Relay, LOW);
  }

  Serial.println("Monitoring button");

}

assiging ke braicket dhyan se close, jo declare kiya vahi use


3️⃣ Why millis() is Used Instead of delay()
delay()
delay(1000)

Problem:

Arduino stops everything for 1 second

CPU cannot do other tasks.


unsigned long previousTime = 0;

void setup(){
  Serial.begin(9600);
}

void loop(){

  if(millis() - previousTime >= 1000){

    Serial.println("1 second passed");

    previousTime = millis();
  }

}

6️⃣ Why We Use unsigned long

Because time values become very large numbers.

int cannot store large values.

So we use:

unsigned long


!digitalRead(LED)
Toggle LED with help
of previous time, unsigned long pv= 0l


and in llop
if(millis()- pv >=1000){
digitalWrite(LED,!digitalRead(LED));

}


unsigned long pT = 0;
int LED = 10;

void setup(){

  pinMode(LED, OUTPUT);
  Serial.begin(9600);

}

void loop(){

  if(millis() - pT >= 2000){

    digitalWrite(LED, !digitalRead(LED));

    Serial.println("LED toggled");

    pT = millis();

  }

}

yahan maine pichle timer ko millis dubara zero nahi kiya that




| Memory Type | Size      | Purpose                           |
| ----------- | --------- | --------------------------------- |
| Flash       | **32 KB** | stores program code               |
| SRAM        | **2 KB**  | stores variables during execution |
| EEPROM      | **1 KB**  | stores persistent data            |


Pins

Digital pins:

14 digital pins (D0–D13)

PWM pins:

6 PWM pins
3,5,6,9,10,11

Analog pins:

8 analog pins (A0–A7)

But important:

A6 and A7 → analog only
Power Pins

Common ones:

VIN
5V
3.3V
GND (multiple)

Also:

RESET
AREF


16 MHz-clock speed
