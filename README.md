# arduino-serial-string-oled


This Script is built for the esp8266 development board, you can simply send String data through the serial port and your data is going to be printed on the OLED display



![ESP8266 with OLED Display](https://www.makershop.de/wp-content/uploads/2018/06/nodemcu-esp8266-dev-board-3.jpg)
```
#include <ESP8266WiFi.h>
#include "SSD1306.h"
SSD1306 display(0x3c, 5, 4);

String myData;

int port = 9600;

void setup() {
  display.init();

  Serial.begin(long(port));
  Serial1.setTimeout(100);
  
  display.clear();
  display.setFont(ArialMT_Plain_16);
  display.drawString(0, 0, "Serial to Display");
  display.setFont(ArialMT_Plain_10);
  String StringPort = "Port: " + String(port);
  display.drawString(0, 20, "Max Walter (c) 2018");
  display.drawString(0, 30, StringPort);
  display.drawString(0, 45, "Waiting.....");
  display.display();
}

void loop() {
  while (Serial.available() > 0) {
    char data = Serial.read();
    myData += data;
    if(data == '\n'){
      display.clear();
      display.drawString(0, 0, myData);
      display.display();
      myData = "";
    }
    
  }
}
```
