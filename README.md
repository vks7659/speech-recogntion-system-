# speech-recogntion-system-
#include <SoftwareSerial.h>
SoftwareSerial vr(2, 3); // RX, TX

#define LIGHT_PIN 8
#define FAN_PIN 9

int command = 0;

void setup() {
  Serial.begin(9600);
  vr.begin(9600);

  pinMode(LIGHT_PIN, OUTPUT);
  pinMode(FAN_PIN, OUTPUT);

  digitalWrite(LIGHT_PIN, LOW);
  digitalWrite(FAN_PIN, LOW);

  Serial.println("Speech Recognition System Initialized");
  Serial.println("Listening for commands...");
}

void loop() {
  if (vr.available()) {
    command = vr.read();
    Serial.print("Command received: 0x");
    Serial.println(command, HEX);
    processCommand(command);
  }
  delay(100);
}

void processCommand(int cmd) {
  switch(cmd) {
    case 0x11:
      digitalWrite(LIGHT_PIN, HIGH);
      Serial.println("Turning ON Light");
      break;
    case 0x12:
      digitalWrite(LIGHT_PIN, LOW);
      Serial.println("Turning OFF Light");
      break;
    case 0x13:
      digitalWrite(FAN_PIN, HIGH);
      Serial.println("Turning ON Fan");
      break;
    case 0x14:
      digitalWrite(FAN_PIN, LOW);
      Serial.println("Turning OFF Fan");
      break;
    default:
      Serial.println("Invalid command");
      break;
  }
}

#output

![Image](https://github.com/user-attachments/assets/3986ea6d-6f04-4dc7-a624-fa644d33e49e)
