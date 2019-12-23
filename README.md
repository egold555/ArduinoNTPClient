# ArduinoNTPClient
Arduino NTPClient for ESP8266

Code used, based on and modified from:
  - https://github.com/taranais/NTPClient
  - https://github.com/arduino-libraries/NTPClient 
  - https://github.com/PaulStoffregen/Time/blob/master/Time.cpp

I have added my own modifications to suit my own project(s).

## Example code
```c++
#include "NTPClient.h"
#include <ESP8266WiFi.h>
#include <WiFiUdp.h>

const char *ssid     = "YOUR_SSID_HERE";
const char *password = "YOUR_PASSWORD_HERE";

const long utcOffsetInSeconds = -28800;

// Define NTP Client to get time
WiFiUDP ntpUDP;
NTPClient timeClient(ntpUDP, "pool.ntp.org", utcOffsetInSeconds);

void setup(){
  Serial.begin(115200);

  WiFi.begin(ssid, password);

  while ( WiFi.status() != WL_CONNECTED ) {
    delay ( 500 );
    Serial.print ( "." );
  }

  timeClient.begin();
}

void loop() {
  timeClient.update();

  Serial.println(timeClient.getFormattedDay());
  Serial.println(timeClient.getFormattedTime12());
  Serial.println(timeClient.getFormattedDate());
  Serial.println();

  delay(1000);
}
```
Example Output:
```
Sunday
11:42:43 PM
12-22-2019
```
