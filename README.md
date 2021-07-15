# IOT-Arduino-Radar-Project
In this project, I will show you how to design a simple Radar Application using Arduino and Processing. This Arduino Radar Project is implemented with the help of Processing Application.  

 #include <Servo.h>
 
 const int trigPin = 10;  
 const int echoPin = 9;
 
 // Variables for the duration and the distance  
 long duration;  
 int distance;
 
 Servo myServo; // Creates a servo object for controlling the servo motor
   
 void setup() {  
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output  
  pinMode(echoPin, INPUT); // Sets the echoPin as an Input  
  pinMode(11, OUTPUT);
  Serial.begin(9600);  
  myServo.attach(3); // Defines on which pin is the servo motor attached  
 }
 
 void loop()
 {  
  for(int i=0;i<=165;i++){   
  myServo.write(i);  
  delay(15);  
  distance = calculateDistance();// Calls a function for calculating the distance measured by the Ultrasonic sensor for each degree  
  Serial.print(i);  
  Serial.print(",");  
  Serial.print(distance);  
  Serial.print(".");
  }  
  // Repeats the previous lines from 165 to 15 degrees  
  for(int i=180;i>0;i--){   
  myServo.write(i);  
  delay(15);  
  distance = calculateDistance();   
  Serial.print(i);  
  Serial.print(",");  
  Serial.print(distance);  
  Serial.print(".");
 
  }  
   if(distance<=1000)
  {
    digitalWrite(11,HIGH);
    delay(1000);
    digitalWrite(11,LOW);
    delay(1000);
  }
  
 }
 
 int calculateDistance()
 {   
  digitalWrite(trigPin, LOW);   
  delayMicroseconds(2);  
  // Sets the trigPin on HIGH state for 10 micro seconds  
  digitalWrite(trigPin, HIGH);   
  delayMicroseconds(10);  
  digitalWrite(trigPin, LOW);  
  duration = pulseIn(echoPin, HIGH); // Reads the echoPin, returns the sound wave travel time in microseconds  
  distance= duration*0.034/2;  
  return distance;  
 }  
