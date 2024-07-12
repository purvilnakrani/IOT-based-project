# IOT-based-project sem-5

int inputPin = 0;
int pirState = LOW;
int val = 0;
void setup() {
pinMode(inputPin, INPUT);
Serial.begin(9600);
}
void loop() {
val = digitalRead(inputPin);
if (val == HIGH) {
if (pirState == LOW) {
Serial.println("Motion detected!");
pirState = HIGH;
}
}
else {
if (pirState == HIGH){
Serial.println("Motion ended!");
pirState = LOW;
}
}
}

int inputPin = A0;
int val = 0;
void setup() {
pinMode(inputPin, INPUT);
Serial.begin(9600);
}
void loop() {
val = analogRead(inputPin);
if (val < 900) {
Serial.println("Object detected!");
}
else {
Serial.println("Object detected!");
}
delay(500);
}

#include<ESP8266WiFi.h>
#include<ThingSpeak.h>
#include<dht.h>
#define sensorPin A0;
char* ssid="realme narzo 20 pro";
char* pass="abcd1234";
WiFiClient client;
char ip[] = "184.106.153.149";
long id = 1887845;
char* api = "MY_API_KEY";
dht DHT;
void setup() {
Serial.begin(9600);
Serial.println("Connecting to WiFi...");
WiFi.begin(ssid, pass);
while(WiFi.status() != WL_CONNECTED){
Serial.print(".");
delay(500);
}
Serial.println("Wifi Connected!");
ThingSpeak.begin(client);
DHT.begin();
}

9

Purvil Nakrani (190420116039)

void loop() {
if(client.connect(ip, 80)){
DHT.read11(sensorPin);
h = DHT.readHumidity();
t = DHT.readTemperature();
Serial.print("Temperature: ");
Serial.println(t);
Serial.print("Humidity: ");
Serial.println(h);
ThingSpeak.setField(1, t);
ThingSpeak.setField(2, h);
ThingSpeak.writeFields(id, api);
}
client.stop();
delay(1500);
}
