Serial Communication using SoftwareSerial

#include <SoftwareSerial.h>
#define tx 8
#define rx 9
SoftwareSerial mySerial(rx, tx); //RX, TX
void setup()
{
 Serial.begin(9600);
 mySerial.begin(9600);

}
void loop()
{
 if(mySerial.available())
6
 {
 Serial.println(mySerial.readString());
 }
 if(Serial.available()){
 mySerial.write(Serial.read());
 }
}

Slave Module Configuration with SoftwareSerial

#include <SoftwareSerial.h>
#define BT_NAME "BT_Slave"
SoftwareSerial mySerial(8, 9); // RX, TX
void setup()
{
 Serial.begin(38400);
 mySerial.begin(38400);
 Serial.println("Arduino receiver");
 mySerial.print("AT\r\n");
 delay(200);
 mySerial.print("AT+RMAAD\r\n");
 delay(200);
 mySerial.print("AT+ADDR?\r\n");
 delay(200);
 mySerial.print("AT+NAME="+String(BT_NAME)+"\r\n");
 delay(200);
 mySerial.print("AT+PSWD=\"1234\"\r\n");
7
 delay(200);
 mySerial.print("AT+ROLE?\r\n");
 delay(200);
 mySerial.print("AT+UART=9600,0,0\r\n");
 delay(500);
}
void loop()
{
}

Master Module Configuration with SoftwareSerial

#include <SoftwareSerial.h>
#define BT_NAME "BT_Master"
#define SLAVE_ADDRESS "0000,13,0AA5EB" //0:13:AA5EB
SoftwareSerial mySerial(2, 3); // RX, TX
void setup()
{
 Serial.begin(38400);
 mySerial.begin(38400);
 Serial.println("Arduino Sender");
 mySerial.print("AT\r\n");
 updateSerial();
 delay(200);
 mySerial.print("AT+RMAAD\r\n");
 updateSerial();
 delay(200);
 mySerial.print("AT+ROLE=1\r\n");
 updateSerial();
 delay(200);
 mySerial.print("AT+NAME="+String(BT_NAME)+"\r\n");
 updateSerial();
 delay(200);
 mySerial.print("AT+PSWD=\"1234\"\r\n");
 updateSerial();
 delay(200);
 mySerial.print("AT+BIND="+String(SLAVE_ADDRESS)+"\r\n");
 updateSerial();
 delay(200);
 mySerial.print("AT+UART=38400,0,0\r\n");
 updateSerial();
 delay(500);
 mySerial.print("AT+UART?\r\n");
 updateSerial();
 delay(200);
8
}
void loop()
{
}