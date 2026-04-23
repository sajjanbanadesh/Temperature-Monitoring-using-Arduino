# 🌡️ Temperature Monitoring System using Arduino

## 📌 Description

This project demonstrates a simple Temperature Monitoring System using Arduino Uno and LM35 sensor. The system reads analog temperature data from the sensor, converts it into Celsius, and displays the real-time value on a 16x2 I2C LCD. Additionally, the temperature readings are logged to the Serial Monitor for observation and debugging.

The project highlights basic concepts of sensor interfacing, analog-to-digital conversion, and real-time data visualization using Arduino.

---

## 🚀 Features

* Real-time temperature display on LCD
* Serial monitoring for debugging and logging
* Stable readings using averaging technique
* Simple and low-cost implementation

---

## 🧰 Components Used

* Arduino Uno
* LM35 Temperature Sensor
* 16x2 I2C LCD
* Breadboard
* Connecting Wires

---

## 🔌 Circuit Connections

## LM35 Sensor

* VCC → 5V
* GND → GND
* OUT → A0

## I2C LCD

* VCC → 5V
* GND → GND
* SDA → A4
* SCL → A5

---

## ⚙️ Working Principle

The LM35 sensor outputs an analog voltage proportional to temperature (10mV per °C). The Arduino reads this voltage using analog pin A0, converts it into temperature in Celsius, and displays it on the LCD. The same data is also printed to the Serial Monitor.

---

## 💻 Arduino Code

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);
int lm35Pin = A0;

float getTemperature() {
  int sum = 0;
  for (int i = 0; i < 10; i++) {
    sum += analogRead(lm35Pin);
    delay(10);
  }
  float avg = sum / 10.0;
  float voltage = avg * (5.0 / 1023.0);
  return voltage * 100.0;
}

void setup() {
  Serial.begin(9600);
  lcd.init();
  lcd.backlight();
  lcd.print("Temp Monitor");
  delay(2000);
  lcd.clear();
}

void loop() {
  float temperature = getTemperature();

  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperature, 1);
  lcd.print((char)223);
  lcd.print("C");

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" C");

  delay(1000);
}
```

---

## 📊 Output

* LCD displays real-time temperature (°C)
* Serial Monitor logs temperature every second

---

## 📸 Screenshots

(Add your images here)

```md
![Circuit](circuit.jpg)
![LCD Output](lcd.jpg)
![Serial Monitor](serial.jpg)
```

---

## 🎥 Demonstration

Video not included. Screenshots are provided as proof of working.

---

## 🛠️ Technologies Used

* Arduino IDE (C/C++)
* Embedded Systems
* Sensor Interfacing

---

## ✅ Conclusion

This project demonstrates basic Arduino programming, sensor interfacing, and real-time display. It is a beginner-friendly project useful for learning embedded systems.
