# project-1
Traffic light temperature sensor using arduino

Our project is a heat detection sensor that will visually broadcast whether the temperature inside a designated area is unsuitable for working conditions.
We believe that this sensor if implemented into working factories in both ireland and across the globe could benefit working conditions for both employees and employers alike.
This would help aid the UN Sustainability Development Goals (SDGs) in there actions towards a healthier generation of workers and may cut down on the amount of mistreated employees across the world. 
We believe that using our design we may be able to change the working world forever.
As a group we are appauled that working conditions in some countries and in the past is not acceptable and we decided that we may be able to make a change to this environment.


Arduino Code
#include <math.h>

const int B = 4275;              
const int R0 = 100000;           
const int pinTempSensor = A0;     

#if defined(ARDUINO_ARCH_AVR)

#define debug  Serial

#elif defined(ARDUINO_ARCH_SAMD) ||  defined(ARDUINO_ARCH_SAM)

#define debug  SerialUSB

#else

#define debug  Serial

#endif

#include <Wire.h>

  #include "rgb_lcd.h"
  
void setup()
{
    Serial.begin(9600);
}

void loop()
{
    int a = analogRead(pinTempSensor);

    float R = 1023.0/a-1.0;
    R = R0*R;

    float temperature = 1.0/(log(R/R0)/B+1/298.15)-273.15; // convert to temperature via datasheet

    Serial.print("temperature = ");
    Serial.println(temperature);

    delay(100);

    if (temperature<16)
{
  

  rgb_lcd lcd;

  const int colorR = 255;
  const int colorG = 0;
  const int colorB = 0;

  void setup() 
  {
    
    lcd.begin(16, 2);
    
    lcd.setRGB(colorR, colorG, colorB);
    
    
    lcd.print("UNSAFE EVACUATE!!");

    delay(1000);
  }

  void loop() 
  {
    lcd.setCursor(0, 1);
    lcd.print(millis()/1000);

    delay(100);
  }
}
else if (temperature>16)
[
  #include <Wire.h>
  #include "rgb_lcd.h"

  rgb_lcd lcd;

  const int colorR = 0;
  const int colorG = 255;
  const int colorB = 0;

  void setup() 
  {
    
    lcd.begin(16, 2);
    
    lcd.setRGB(colorR, colorG, colorB);
    
    
    lcd.print("SAFE CONTINUE WORK");

    delay(1000);
  }

  void loop() 
  {
    lcd.setCursor(0, 1);
    lcd.print(millis()/1000);

    delay(100);
  }
}

