# วัตถุประสงค์
เขียนโปรแกรมเพื่อสั่งงานรีเลย์บนบอร์ด ESP32 AC Power ProtoAutomation

# ระดับความยาก
พื้นฐาน

# ความต้องการพื้นฐาน

- พื้นฐานการเขียนโปรแกรมด้วย Arduino framework
- โปรแกรม Arduino IDE Version 1.8.1+

# อธิบายโค๊ดโปรแกรม

กำหนดตัวแปรเพื่อตั้งค่า GPIO

````
int relay1 = 26;
int relay2 = 25;
int relay3 = 33;
int relay4 = 32;
````

กำหนด GPIO เป็น OUTPUT เพื่อสั่งงาน Relay ทั้ง 4 ตัว

``````
void setup() {
  pinMode(relay1, OUTPUT);
  pinMode(relay2, OUTPUT);
  pinMode(relay3, OUTPUT);
  pinMode(relay4, OUTPUT);
}
``````

เขียนลูปเพื่อทดลองสั่งงาน Relay ทั้ง 4 ตัว
```````````````
void loop() {
  digitalWrite(relay1, HIGH);
  delay(200);
  digitalWrite(relay1, LOW);
  digitalWrite(relay2, HIGH);
  delay(200);
  digitalWrite(relay2, LOW);
  digitalWrite(relay3, HIGH);
  delay(200);
  digitalWrite(relay3, LOW);
  digitalWrite(relay4, HIGH);
  delay(200);
  digitalWrite(relay4, LOW);
  delay(500);
}
```````````````

[Download โค๊ดโปรแกรมสั่งงานรีเลย์บนบอร์ด ESP32 AC Power ProtoAutomation](https://gist.githubusercontent.com/imiconsystem/4746abf2e34db8418fd130536bcb9f39/raw/8a0512d8327e7d5882d0b2d669075caed19a72ce/protoautomation%20-%20test%20relay)
