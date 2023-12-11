# Report 13 - Week of 11/23/2023 
### 🪐 Brief: This week, I tested the metallic thread and conductive thread with Visual Studio Code.###
> 
A major challenge was ensuring distinct data sets from each hoop to Max/MSP. This required multiple code refinements in Visual Studio and adjustments in Max/MSP, transforming basic outputs into a sophisticated process of data handling.

```
#define FOIL1   A4 //FOILgroup1
#define FOIL2   A0
#define FOIL3   A2 //FOILgroup2

#define FOIL4   A5
#define FSRPIN  A3 //FSR

#include "Particle.h"

SYSTEM_MODE(AUTOMATIC);
SYSTEM_THREAD(ENABLED);

void setup() {
  Serial.begin(9600);
  pinMode(FOIL1, INPUT);
  pinMode(FOIL2, INPUT);
  pinMode(FOIL3, INPUT);
  pinMode(FOIL4, INPUT);
  pinMode(FSRPIN, INPUT); 
}

void loop() {

  int sensorValue1 = analogRead(FOIL1);
  int sensorValue2 = analogRead(FOIL2);
  int sensorValue3 = analogRead(FOIL3);
  int sensorValue4 = analogRead(FOIL4);
  int fsrValue = analogRead(FSRPIN);

  int conduct_1 =  map(sensorValue1, 0, 4096, 10, 50);
  int conduct_2 = map(sensorValue2, 0, 4096, 100, 150);
  int conduct_3 = map(sensorValue3, 0, 4096, 200, 250);
  int conduct_4 = map(sensorValue4, 0, 4096, 0, 149);
  int fsr_map = map(fsrValue, 0, 4096, 0, 200);

  //s is "small hoop"
  String data = String::format("%s %d", "s1", conduct_1);
  Serial.write(data);
  Serial.write(" ");
  data = String::format("%s %d", "s2", conduct_2);
  Serial.write(data);
  Serial.write(" ");
  data = String::format("%s %d", "s3", conduct_3);
  Serial.write(data);
  Serial.write(" ");
  
// b is "big hoop" and c is "conductive fabric"
  data = String::format("%s %d", "bc", conduct_4);
  Serial.write(data);
  Serial.write(" ");
  data = String::format("%s %d", "bf", fsr_map);
  Serial.write(data);
  Serial.write(" ");

  delay(10);
}
```
