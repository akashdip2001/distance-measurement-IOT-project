# Distance-measurement-IOT-project

https://github.com/user-attachments/assets/e4feb478-7727-4617-839e-8f4f69a669cc

![WhatsApp Image 2025-04-01 at 00 26 54_0361bb4b](https://github.com/user-attachments/assets/23872c8c-6b9c-4f30-a840-211c6a761ebe)

```c++
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
