//for soil moisture
const int AirValue = 810;    //edit later
const int WaterValue = 390;  //edit later
int SoilMoistureValue = 390;
int SoilMoisturePercent = 100;
const int SMrelay = 8;
int lastnightshadestate;
int lastcruciferstate;
int lastbeanstate;
int currentnightshadestate;
int currentcruciferstate;
int currentbeanstate;

void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600);


  pinMode(51, INPUT);
  pinMode(52, INPUT);
  pinMode(53, INPUT);

  pinMode(A4, INPUT);
  pinMode(8, OUTPUT);

  currentnightshadestate = digitalRead(51);
  currentcruciferstate = digitalRead(52);
  currentbeanstate = digitalRead(53);
}

void loop() {
  digitalWrite(8, HIGH);
  lastnightshadestate = currentnightshadestate;
  lastcruciferstate = currentcruciferstate;
  lastbeanstate = currentbeanstate;
  currentnightshadestate = digitalRead(51);
  currentcruciferstate = digitalRead(52);
  currentbeanstate = digitalRead(53);
  SoilMoistureValue = analogRead(A4);  //SM sensor
  SoilMoisturePercent = map(SoilMoistureValue, AirValue, WaterValue, 0, 100);

  if (lastnightshadestate == HIGH && currentnightshadestate == LOW) {
    Serial.print("Nightshade");
    for (int i = 0; i < i + 1; i++) {
      Serial.println(SoilMoistureValue);
      if (SoilMoisturePercent <= 70) {

        Serial.print(SoilMoisturePercent);
        Serial.print("%");
        digitalWrite(SMrelay, LOW);  //water pump on
        delay(700);
      } else if (SoilMoisturePercent > 70) {

        Serial.print(SoilMoisturePercent);
        Serial.print("%");
        digitalWrite(SMrelay, HIGH);  //water pump off
        delay(700);
      }
      Serial.println();
    }
  }


  if (lastcruciferstate == HIGH && currentcruciferstate == LOW) {
    Serial.print("Crucifers");
    for (int i = 0; i < i + 1; i++) {
      Serial.println(SoilMoistureValue);
      if (SoilMoisturePercent <= 70) {

        Serial.print(SoilMoisturePercent);
        Serial.print("%");
        digitalWrite(SMrelay, LOW);  //water pump on
        delay(700);
      } else if (SoilMoisturePercent > 70) {

        Serial.print(SoilMoisturePercent);
        Serial.print("%");
        digitalWrite(SMrelay, HIGH);  //water pump off
        delay(700);
      }
      Serial.println();
    }
  }

  if (lastbeanstate == HIGH && currentbeanstate == LOW) {
    Serial.print("Beans");
    for (int i = 0; i < i + 1; i++) {
      Serial.println(SoilMoistureValue);
      if (SoilMoisturePercent <= 60) {

        Serial.print(SoilMoisturePercent);
        Serial.print("%");
        digitalWrite(SMrelay, LOW);  //water pump on
        delay(700);
      } else if (SoilMoisturePercent > 60) {

        Serial.print(SoilMoisturePercent);
        Serial.print("%");
        digitalWrite(SMrelay, HIGH);  //water pump off
        delay(700);
      }
      Serial.println();
    }
  } else {
  }
}
