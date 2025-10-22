#include <LiquidCrystal.h>

// Define the pins for the LCD
// (RS, E, D4, D5, D6, D7)
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

// Define the pins for the Ultrasonic Sensor
const int trigPin = 9;
const int echoPin = 10;

// Define variables to store duration and distance
long duration;
float distance;

void setup() {
  // Set the sensor pin modes
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
  pinMode(echoPin, INPUT);  // Sets the echoPin as an Input
  
  // Initialize the LCD (16 columns and 2 rows)
  lcd.begin(16, 2);
}

void loop() {
  // Clear the LCD screen
  lcd.clear();
  
  // --- Start Ultrasonic Sensor Pulse ---
  // Set the trigPin on LOW state for 2 microseconds
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  // Set the trigPin on HIGH state for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // --- End Ultrasonic Sensor Pulse ---

  // Read the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  
  // Calculate the distance
  // Speed of sound = 0.034 cm/microsecond
  // The sound travels there and back, so we divide by 2
  distance = duration * 0.034 / 2;
  
  // --- Print to the LCD ---
  // Set the cursor to the first column, first row
  lcd.setCursor(0, 0);
  // Print the label "Distance:"
  lcd.print("Distance:");
  
  // Set the cursor to the first column, second row
  lcd.setCursor(0, 1);
  // Print the calculated distance
  lcd.print(distance);
  // Print the units
  lcd.print(" cm");

  // Wait 250 milliseconds before the next reading
  delay(250);
}
