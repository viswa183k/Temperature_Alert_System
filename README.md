# Temperature_Alert_System
Arduino project that monitors temperature using a DHT11 sensor and triggers a buzzer if the temperature exceeds 30°C. Useful for early heat alerts.
// Temperature Alert System using DHT11 and Buzzer

#include <DHT.h>

#define DHTPIN 2
#define DHTTYPE DHT11
#define buzzerPin 9

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
  dht.begin();
  Serial.println("Temperature Alert System Initialized");
}

void loop() {
  float temp = dht.readTemperature();

  if (isnan(temp)) {
    Serial.println("Failed to read temperature.");
    return;
  }

  Serial.print("Temperature: ");
  Serial.print(temp);
  Serial.println(" °C");

  if (temp > 30) {
    digitalWrite(buzzerPin, HIGH);
    Serial.println("⚠️ High Temperature! Buzzer ON");
  } else {
    digitalWrite(buzzerPin, LOW);
    Serial.println("Temperature Normal.");
  }

  delay(2000);
}
