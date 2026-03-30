# Robotics-// Pin definitions
int tempPin = A0;      // Temperature sensor pin
int ledPin = 8;        // LED or fan (via relay)
float temperature; 

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(tempPin);

  // Convert to voltage
  float voltage = sensorValue * (5.0 / 1023.0);

  // Convert voltage to temperature (LM35: 10mV per °C)
  temperature = voltage * 100;

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  // Control system
  if (temperature > 30) {
    digitalWrite(ledPin, HIGH); // Turn ON fan/LED
  } else {
    digitalWrite(ledPin, LOW);  // Turn OFF
  }

  delay(1000);
}
