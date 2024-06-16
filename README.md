# Practica5
## Part A
### Codi en Línea
```cpp
#include <Arduino.h>
#include <Wire.h>
void setup()
{
  Wire.begin(8, 9);
  Serial.begin(115200);
  while (!Serial); // Leonardo: wait for serial monitor
    Serial.println("\nI2C Scanner");
}
void loop()
{
  byte error, address;
  int nDevices;
  Serial.println("Scanning...");
  nDevices = 0;
  for(address = 1; address < 127; address++ )
  {
  // The i2c_scanner uses the return value of
  // the Write.endTransmisstion to see if
  // a device did acknowledge to the address.
    Wire.beginTransmission(address);
    error = Wire.endTransmission();
    Serial.println (address);
    if (error == 0)
    {
      Serial.print("I2C device found at address 0x");
      if (address<16)
        Serial.print("0");
      Serial.print(address,HEX);
      Serial.println(" !");
      nDevices++;
    }
    else if (error==4)
    {
      Serial.print("Unknown error at address 0x");
      if (address<16)
        Serial.print("0");
      Serial.println(address,HEX);
    }
  }
  if (nDevices == 0)
    Serial.println("No I2C devices found\n");
  else
    Serial.println("done\n");
  delay(5000); // wait 5 seconds for next scan
}
```
### Explicació del codi
`1.Inclusió de llibreries`
```cpp
#include <Arduino.h>
#include <Wire.h>
```
Aquí s'inclouen les llibreries per utilitzar les funcions bàsiques d'Arduino i comunicació I2C.

`2.Setup`
```cpp
void setup() {
  Wire.begin(8, 9);
  Serial.begin(115200);
  while (!Serial); // Leonardo: wait for serial monitor
  Serial.println("\nI2C Scanner");
}
```
- **'Wire.begin(8, 9);:'** Aquí s'inicialitza la comunicació I2C al ESP32 utilitzant els pins GPIO 8 (SDA) i 9 (SCL). 
- **'Serial.begin(115200);:'** Aquí s'inicia la comunicació serial a 115200 bauds.
- **'while (!Serial);:'** Aquí espera fins que el port serial estigui llest.
- **'Serial.println("\nI2C Scanner");:'** Mostra per pantalla el missatge "I2C Scanner" al monitor serial.

`3.Loop`
```cpp
void loop() {
  byte error, address;
  int nDevices;
  Serial.println("Scanning...");
  nDevices = 0;
  for (address = 1; address < 127; address++) {
    // The i2c_scanner uses the return value of
    // the Write.endTransmission to see if
    // a device did acknowledge to the address.
    Wire.beginTransmission(address);
    error = Wire.endTransmission();
    Serial.println(address);
    if (error == 0) {
      Serial.print("I2C device found at address 0x");
      if (address < 16)
        Serial.print("0");
      Serial.print(address, HEX);
      Serial.println(" !");
      nDevices++;
    } else if (error == 4) {
      Serial.print("Unknown error at address 0x");
      if (address < 16)
        Serial.print("0");
      Serial.println(address, HEX);
    }
  }
  if (nDevices == 0)
    Serial.println("No I2C devices found\n");
  else
    Serial.println("done\n");
  delay(5000); // wait 5 seconds for next scan
}
```
En aquest loop, sent la part principal del programa, es fa un escaneig per veure els dispositius connectats al bus I2C, dintre d'aquest loop es diferencien diverses parts:
1. **Variables:**
  - **'byte error, address;:'** Declara variables per guardar errors y direccions I2C.
  - **'int nDevices;:'** Declara una altra variable per portar el conteig del número de dispositius I2C trobats.

2. **Inicio del escaneo:**
  - **'Serial.println("Scanning...");:'** Mostra per pantalla "Scanning..." al monitor serial.
  - **'nDevices = 0;:'** Inicialitza el conteig de dispositius a 0.


## Part B
### Codi en Línea
```cpp
#include <Arduino.h>

//YWROBOT
//Compatible with the Arduino IDE 1.0
//Library version:1.1
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,20,4);  // set the LCD address to 0x27 for a 16 chars and 2 line display

void setup()
{
  Wire.begin(8,9);
  lcd.init();                      // initialize the lcd 
  // Print a message to the LCD.
  lcd.backlight();
  lcd.setCursor(3,0);
  lcd.print("Hello, world!");
  lcd.setCursor(2,1);
  lcd.print("Ywrobot Arduino!");
   lcd.setCursor(0,2);
  lcd.print("Arduino LCM IIC 2004");
   lcd.setCursor(2,3);
  lcd.print("Power By Ec-yuan!");
}


void loop()
{
}
```
