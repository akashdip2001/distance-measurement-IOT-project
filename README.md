# Distance-measurement-IOT-project

https://github.com/user-attachments/assets/e4feb478-7727-4617-839e-8f4f69a669cc

![WhatsApp Image 2025-04-01 at 00 26 54_0361bb4b](https://github.com/user-attachments/assets/23872c8c-6b9c-4f30-a840-211c6a761ebe)

---

### ✅ Library need to install for Display : `Liquid Crystal I2C`
### ✅ Code : 

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

#define TRIG_PIN 9
#define ECHO_PIN 10

// Initialize LCD with I2C address 0x27, 16 columns, and 2 rows
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
    Serial.begin(9600);  
    lcd.init();   // Correct function to initialize LCD
    lcd.backlight();
    
    pinMode(TRIG_PIN, OUTPUT);
    pinMode(ECHO_PIN, INPUT);

    lcd.setCursor(0, 0);
    lcd.print("Distance Sensor");
    delay(2000);
    lcd.clear();
}

void loop() {
    long duration;
    float distance_cm;

    // Clear TRIG_PIN
    digitalWrite(TRIG_PIN, LOW);
    delayMicroseconds(2);

    // Send 10µs pulse to TRIG_PIN
    digitalWrite(TRIG_PIN, HIGH);
    delayMicroseconds(10);
    digitalWrite(TRIG_PIN, LOW);

    // Read ECHO_PIN and calculate distance
    duration = pulseIn(ECHO_PIN, HIGH);
    distance_cm = (duration * 0.0343) / 2; // Convert to cm

    // Print to Serial Monitor
    Serial.print("Distance: ");
    Serial.print(distance_cm);
    Serial.println(" cm");

    // Print to LCD
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Distance:");
    lcd.setCursor(0, 1);
    lcd.print(distance_cm);
    lcd.print(" cm");

    delay(500);
}
```

---

<img align="right" alt="Library need to install for Display" width="300" src="https://github.com/user-attachments/assets/969a76dc-07a1-4a08-b2ac-65ca8f16a881">

### **Connections:**
- **HC-SR04 Ultrasonic Sensor:**
  - **VCC** → **5V**
  - **GND** → **GND**
  - **TRIG** → **D9**
  - **ECHO** → **D10**
  
- **16x2 LCD with I2C Module:**
  - **VCC** → **5V**
  - **GND** → **GND**
  - **SDA** → **A4** (Arduino UNO)
  - **SCL** → **A5** (Arduino UNO)

---

![01](https://github.com/user-attachments/assets/7fb5e90a-f2fd-4e65-9a3b-c94e4cb909a7)
![02](https://github.com/user-attachments/assets/7c8fabec-0520-4ad7-853c-f2bdd06fe4a0)
![03](https://github.com/user-attachments/assets/c86ca56d-92bd-4479-b28c-91ee35e74cf4)
![04](https://github.com/user-attachments/assets/e2c38784-dddf-40cd-8ac4-2fc58ef11a49)
![05](https://github.com/user-attachments/assets/2791fcc1-566c-4cd1-b186-b0899fac7de6)
