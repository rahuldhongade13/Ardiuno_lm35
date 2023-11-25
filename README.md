// Include necessary libraries
#include <Arduino.h>

// Define constants
const int temperaturePin = A0;   // LM35 temperature sensor pin
const int ledPin = 13;           // Arduino onboard LED pin

// Define variables
float temperature = 0.0;         // Variable to store temperature value
unsigned long previousMillis = 0; // Variable to store the last time LED was updated

void setup() {
  pinMode(ledPin, OUTPUT);       // Set LED pin as output
  Serial.begin(9600);            // Initialize serial communication
}

void loop() {
  // Read temperature from LM35 sensor
  temperature = analogRead(temperaturePin) * 0.48828125; // Convert analog reading to Celsius

  // Check temperature conditions and control LED
  if (temperature < 30.0) {
    blinkLED(250); // Blink LED every 250 milliseconds
  } else {
    blinkLED(500); // Blink LED every 500 milliseconds
  }
}

void blinkLED(int interval) {
  unsigned long currentMillis = millis(); // Get the current time

  // Check if the specified interval has passed since the last LED update
  if (currentMillis - previousMillis >= interval) {
    // Save the current time for the next interval
    previousMillis = currentMillis;

    // Toggle the LED state
    digitalWrite(ledPin, !digitalRead(ledPin));
  }
}
