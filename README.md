# TURN-ON-BUZZER-WITH-ULTRASONIC-SENSOR-AND-GIVE-SMS-THROUGH
# ABSTRACT
Nowadays, problem of insecurity it is big issues which face with society in this days we already knows that many problem related with insecurity, robberies, terrorism and other problem related with it occurs many times in our society.
In order to overcome with these problem of low security in our society or at our home we need to install a small devices namely ultrasonic sensor with buzzer in case there is any one around our home or our properties in a certain distance we set that sensor can detect the person around it and turn on buzzer with sound and also directly send sms to GSM as a notification which indicate that there is something passing through our home.
# PROBLEM STATEMENT
Turning on  buzzer and ultrasonic  it is the most important  in society  because it help us to measure distance  of object  motion and also it is used  to  control  the home  security  in case there is any one is around our home or any particular places that sensor (ultrasonic sensor)  it detect  if there is something  around there this gives us full security, it is better use  digital  technology  like ; understand  particular case  when   people  enter your home  that can send  message in the telephone   it depend  you  distance setting on the system

# BLOCK DIAGRAM
![image](https://user-images.githubusercontent.com/104190703/166159404-3f7809f2-312d-4124-bbcd-a63c4f23e45b.png)

# DESCRIPTION 
Arduino  uno is  microcontroller board  based  on the  ATMEGA 328p it has  14 digital  in put  pins ( of which 6 can be used as PWM) ‘;ultrasonic  sensor  is an instrument that  measure the distance  to on object using  ultrasonic sound waves ;GSM  global system  for mobile  communication   is standard developed by the (ITSI)
ABUZZER audio signaling device which may be mechanical or piazo electric 
At the step we are going to store the first distance as distance as “distance” later in the loop we are going to check every time if the if the distance is equal to the distance we got now if the distance is less than the distance we stored at the initial setup the trigger will goes on and the buzzer will start buzzing and at the same time GSM module will send a message to the mobile number we given.  

# FRITZING CIRCUIT 
![image](https://user-images.githubusercontent.com/104190703/166159427-cd49f150-6a83-471d-bf3f-b20efc70a80d.png)
 
# PROTEUS CIRCUIT
 ![image](https://user-images.githubusercontent.com/104190703/166159448-cb7941c8-e0fd-4c4a-b31a-d17914242ea5.png)
# ARDUINO SOURCE CODES
#include<SoftwareSerial.h>

int trigPin = 8;

int echoPin = 7;

int buzzer=5;

int distance;

int duration;

int normalDistance;

SoftwareSerial mySerial(2,3);
boolean triggered=false;

void setup() 

{

mySerial.begin(9600);

Serial.begin(9600);

delay(100);

pinMode(8,OUTPUT);

pinMode(7, INPUT);

pinMode(5, HIGH);

long duration, distance;

while(millis()<5000)

{

digitalWrite(5, HIGH);

digitalWrite(8,LOW);

delayMicroseconds(100);

digitalWrite(8, HIGH);

delayMicroseconds(10);

digitalWrite(8, LOW);

duration=pulseIn(7,HIGH);

distance=duration*0.034/2;

normalDistance=distance;

Serial.print("Distance:");

Serial.println(distance);
digitalWrite(5, LOW);
}
}

void loop() 

{

  digitalWrite(8,LOW);
  
  delayMicroseconds(2);
  
  digitalWrite(8, HIGH);
  
  delayMicroseconds(10);
  
  digitalWrite(8, LOW);
  
  duration=pulseIn(7, HIGH);
  
  distance=duration*0.034/2;
  
  Serial.print("Distance:");
  
  Serial.println(distance);
  
  if(distance<normalDistance-5)
  
  {
  
    triggered=true;
    
  }
  
  else
  
  {
  
    triggered=false;
    
   
  }
  
  if(triggered)
  
  {
  
    digitalWrite(5, HIGH);
    
    delay(500);
    
  }
  
  else
  
  {
  
    digitalWrite(5,LOW);
    
    delay(250);
    
  mySerial.println("AT+CMGF=1");//set the GSM module in text mode
  delay(1000);//delay of 1000 milliseconds or 1 second
  
  mySerial.println("AT+CMGS=\+250785053229\"\r");//mobile number where the SMS will be sent
  delay(1000);
  
  mySerial.println("Buzzer ON");//text to be sent
  delay(100);
  
  mySerial.println((char)26);
  
  delay(1000);
  
}

}
Done by:
-MWUMVANEZA Callixte

-DUSHIMIMANA Placide

