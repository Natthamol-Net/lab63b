# การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์

## วัตถุประสงค์
1. เพื่อศึกษาวิธีการเขียนโปรแกรมด้วย PlatformIO ลงบน Microcontroller (ESP01)
2. เพื่อให้เข้าใจการทำงานของโปรแกรมที่รันลงไปใน Microcontroller (ESP01)

## อุปกรณ์ที่ใช้
1. Microcontroller (ESP01)
2. Serial port
3. อุปกรณ์เชื่อมต่อ USB (USB to Serial)

## ศึกษาข้อมูลเบื้องต้น
1. 01 run example 1 : https://youtu.be/NLIUsWLEpmg
2. src code ของตัวอย่างโปรแกรม 01_Serial-Monitor : https://github.com/choompol-boonmee/lab63b/blob/master/examples/01_Serial-Monitor/src/main.cpp
3. ศึกษาใน https://platformio.org/ ว่าตัว Microcontroller สามารถใช้ได้หลากหลาย และมีวิธีการเขียน ภาษาที่ใช้เขียนโปรแกรมที่แตกต่างกัน

## วิธีการทำการทดลอง
1. ต่อ Microcontroller เข้าทาง Serial port

![รูป 1](https://user-images.githubusercontent.com/80879886/112181282-dda69c00-8c2e-11eb-8f3f-1da73447626e.JPG)

2. ดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
-	พิมพ์ cd pattani เพื่อเข้าไปในโฟลเดอร์ 
-	พิมพ์ Is แสดงโปรแกรมตัวอย่าง ในโฟลเดอร์นี้มีโปรแกรมอยู่ 9 โปรแกรม

![รูป 2](https://user-images.githubusercontent.com/80879886/112181768-4aba3180-8c2f-11eb-80ea-9dbb0eafad7b.jpg)

3. เลือกใช้โปรแกรมตัวอย่างที่ 1
-	พิมพ์ cd 01_Serial-Monitor
-	พิมพ์ vi src/main.cpp เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
```javascript
#include <Arduino.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
}

void loop()
{
	cnt++;
	Serial.printf("PATTANI :%d\n",cnt);
	delay(1000);
}

