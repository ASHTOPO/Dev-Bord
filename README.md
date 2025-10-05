// Define the pin connected to the sensor's data/analog output
const int sensorPin = A0;
// Define the pin to power the sensor (can be any digital pin)
const int sensorPowerPin = 7; // Example: Digital Pin 7

void setup() {
  // Initialize serial communication to see readings on the Serial Monitor
  Serial.begin(9600);
  // Set the power pin as an output and ensure it's off initially
  pinMode(sensorPowerPin, OUTPUT);
  digitalWrite(sensorPowerPin, LOW);
}

void loop() {
  // Turn the sensor on
  digitalWrite(sensorPowerPin, HIGH);
  // Wait a brief moment for the sensor to power on and stabilize
  delay(300); 

  // Read the analog value from the sensor
  int sensorValue = analogRead(sensorPin); 

  // Turn the sensor off to prevent corrosion
  digitalWrite(sensorPowerPin, LOW);
  // A brief delay after turning off helps the sensor settle
  delay(10); 

  // Print the raw analog reading to the Serial Monitor
  Serial.print("Analog Moisture Reading: ");
  Serial.println(sensorValue);

  // Wait before taking the next reading to avoid overwhelming the sensor or serial monitor
  delay(1000); // Delay for 1 second
}
