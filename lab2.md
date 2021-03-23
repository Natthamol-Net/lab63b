# การทดลองที่ 2 เรื่อง การเขียนโปรแกรมค้นหาไวไฟ

## วัตถุประสงค์
1. เพื่อศึกษาวิธีการรันโปรแกรมลงบน Microcontroller (ESP01) ชนิดที่มี Wifi อยู่ในตัว

## อุปกรณ์ที่ใช้
1.	Microcontroller (ESP01) ชนิดที่มี Wifi อยู่ในตัว
2.	Serial port
3.	อุปกรณ์เชื่อมต่อ USB (USB to Serial)

## ศึกษาข้อมูลเบื้องต้น
1. 02 run example 2 : https://youtu.be/yBjab0UNuB8
2. src code ของตัวอย่างโปรแกรม 01_Serial-Monitor : https://github.com/choompol-boonmee/lab63b/blob/master/examples/02_Scan-Wifi/src/main.cpp

## วิธีการทำการทดลอง
1. ต่อตัว  Microcontroller เข้ากับ  Serial port

2. ดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
- พิมพ์ **cd pattani** เพื่อเข้าไปในโฟลเดอร์ 

3. เลือกใช้โปรแกรมตัวอย่างที่ 2
- พิมพ์ **cd 02_Scan-Wifi**
- พิมพ์ **vi src/main.cpp** เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
```javascript
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	WiFi.mode(WIFI_STA);
	WiFi.disconnect();
	delay(100);
	Serial.println("\n\n\n");
}

void loop()
{
	Serial.println("========== เริ่มต้นแสกนหา Wifi ===========");
	int n = WiFi.scanNetworks();
	if(n == 0) {
		Serial.println("NO NETWORK FOUND");
	} else {
		for(int i=0; i<n; i++) {
			Serial.print(i + 1);
			Serial.print(": ");
			Serial.print(WiFi.SSID(i));
			Serial.print(" (");
			Serial.print(WiFi.RSSI(i));
			Serial.println(")");
			delay(10);
		}
	}
	Serial.println("\n\n");
}
```
จากโปรแกรมที่ 2 จะแสดงข้อมูลแบ่งเป็น 2 ส่วนคือ 
-	ส่วน set up จะ set Wifi ให้พร้อมทำงาน
-	ส่วน loop คือ วนลูปไปเรื่อยๆ โดยแสดงผลเริ่มต้นว่า ‘เริ่มต้นค้นหา Wifi’ เมื่อค้นหาได้แล้วจะแสดงผลว่า รอบๆตัว Microcontroller มี Wifi อะไรบ้าง 

5. ทำการ upload โปรแกรม 02_Scan-Wifi เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม

![รูป 1](https://user-images.githubusercontent.com/80879886/112187786-fb76ff80-8c34-11eb-856d-1caa35024b92.JPG)

6. ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

![รูป 2](https://user-images.githubusercontent.com/80879886/112187791-fc0f9600-8c34-11eb-904c-9d8b30db0ca4.JPG)

![รูป 3](https://user-images.githubusercontent.com/80879886/112187793-fca82c80-8c34-11eb-9861-5960e05978ce.JPG)

7. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor** จะแสดงผลได้ดังรูป

![รูป 4](https://user-images.githubusercontent.com/80879886/112187796-fd40c300-8c34-11eb-8e12-ac99ddfc7e73.JPG)

## การบันทึกผลการทดลอง
เมื่อทำการอัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว จะแสดงผลลัพธ์ด้วยการพิมพ์คำสั่ง **pio device monitor** 
เพื่อให้ตัว Microcontroller แสกนหา Wifi รอบๆตัว และแสดงผลออกมา ถ้ากดปุ่มรีเซ็ต (สีแดง) ตัว Microcontroller จะเริ่มทำการแสกนหา Wifi ใหม่

![รูป 5](https://user-images.githubusercontent.com/80879886/112190317-76d9b080-8c37-11eb-9806-538a039431c8.JPG)

## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมเพื่อค้นหาไวไฟ โดยเลือกโปรแกรม 02_Scan-Wifi มาเขียน ซึ่งเป็นโปรแกรมค้นหาไวไฟรอบๆตัว ผลลัพธ์ที่แสดงออกมาจะแสดงจำนวนและชื่อไวไฟ ตามโปรแกรมที่เขียนลงไป
ซึ่งสามารถนำไปประยุกต์ใช้กับอุปกรณ์ภายในโทรศัพท์หรือคอมพิวเตอร์ เพื่อค้นหา Wifi รอบๆตัวว่า มี Wifi กี่ตัวที่สามารถใช้ได้

## คำถามหลังการทดลอง
