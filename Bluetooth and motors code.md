# Robotic-Trash-Collector

#include <SoftwareSerial.h>


SoftwareSerial bluetooth(11, 10); // Define the RX and TX pins for Bluetooth


const int MA1 = 5; // Pin 5 is connected to the AI1 pin of the motor driver for Motor A
const int MA2 = 4; // Pin 4 is connected to the AI2 pin of the motor driver for Motor A
const int PWMA = 9; // Pin 9 is connected to the PWMA pin of the motor driver for Motor A


const int MB1 = 3; // Pin 3 is connected to the BI1 pin of the motor driver for Motor B
const int MB2 = 2; // Pin 2 is connected to the BI2 pin of the motor driver for Motor B
const int PWMB = 6; // Pin 6 is connected to the PWMB pin of the motor driver for Motor B


void setup() {
 // Setting pinModes for Motor A
 bluetooth.begin(9600); // Initialize Bluetooth communication
 pinMode(MA1, OUTPUT);
 pinMode(MA2, OUTPUT);
 pinMode(PWMA, OUTPUT);


 // Setting pinModes for Motor B
 pinMode(MB1, OUTPUT);
 pinMode(MB2, OUTPUT);
 pinMode(PWMB, OUTPUT);
 pinMode(12,OUTPUT);
}


void loop() {
 digitalWrite(12,HIGH);
 if (bluetooth.available() > 0) {
   char command = bluetooth.read();


   if (command == '1') { // Forwards
     forward(255);
   }


   if (command == '2') { // Right
     right(255);
   }


   if (command == '3') { // Left
     left(255);
   }


   if (command == '4') { // Backward
     reverse(255);
   }


   if (command == '5') { // Stop
     stop();
   }
 }
}


void forward(int speed) {
  digitalWrite(MA1, HIGH);
  digitalWrite(MA2, LOW);
  analogWrite(PWMA, speed);


  digitalWrite(MB1, HIGH);
  digitalWrite(MB2, LOW);
  analogWrite(PWMB, speed);
}


void reverse(int speed) {
  digitalWrite(MA1, LOW);
  digitalWrite(MA2, HIGH);
  analogWrite(PWMA, speed);


  digitalWrite(MB1, LOW);
  digitalWrite(MB2, HIGH);
  analogWrite(PWMB, speed);
}


void left(int speed) {
  digitalWrite(MA1, HIGH);
  digitalWrite(MA2, LOW);
  analogWrite(PWMA, speed);


  digitalWrite(MB1, LOW);
  digitalWrite(MB2, HIGH);
  analogWrite(PWMB, speed);
}


void right(int speed) {
  digitalWrite(MA1, LOW);
  digitalWrite(MA2, HIGH);
  analogWrite(PWMA, speed);


  digitalWrite(MB1, HIGH);
  digitalWrite(MB2, LOW);
  analogWrite(PWMB, speed);
}


void stop() {
  digitalWrite(MA1, LOW);
  digitalWrite(MA2, LOW);
  analogWrite(PWMA, 0);


  digitalWrite(MB1, LOW);
  digitalWrite(MB2, LOW);
  analogWrite(PWMB, 0);
}
