# การทดลองที่ 3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล

## วัตถุประสงค์
1.	เพื่อศึกษาวิธีการรันโปรแกรมบน Microcontroller ที่ทดลองส่งสัญญาณ output ออกไปสู่ภายนอก
2.	เพื่อนำ Microcontroller ที่ถูกเขียนโปรแกรมแล้วไปประยุกต์ใช้กับอุปกณ์อื่น 

## อุปกรณ์ที่ใช้
1.	Microcontroller (ESP01) 
2.	Serial port
3.	อุปกรณ์เชื่อมต่อ USB (USB to Serial)
4.	Adapter 
5.	Relay
6.	ขั้วชาร์จ หรือ Power Bank

## ศึกษาข้อมูลเบื้องต้น
1. 03 run example 3 : https://youtu.be/CCnN1WJsXQY
2. src code ของตัวอย่างโปรแกรม 03_Output-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/03_Output-Port/src/main.cpp
3. Relay คืออะไร? : https://bedroomlearning.blogspot.com/2016/10/relay.html

## วิธีการทำการทดลอง
1. เสียบตัว Adapter เข้า Serial port แล้วค่อยเสียบตัว Microcontroller บน Adapter

![รูป 1](https://user-images.githubusercontent.com/80879886/112192943-01231400-8c3a-11eb-9bed-7735d867c49d.JPG)

2. ดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
- พิมพ์ **cd pattani** เพื่อเข้าไปในโฟลเดอร์ 

3.เลือกใช้โปรแกรมตัวอย่างที่ 3
- พิมพ์ **cd 03_Output-Port**
- พิมพ์ **vi src/main.cpp** เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
```javascript
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	cnt++;
	if(cnt % 2) {
		Serial.println("========== ON ===========");
		digitalWrite(0, HIGH);
	} else {
		Serial.println("========== OFF ===========");
		digitalWrite(0, LOW);
	}
	delay(500);
}
```
จากโปรแกรมที่ 3 จะแสดงข้อมูลแบ่งเป็น 2 ส่วนคือ 
- ส่วน set up โปรแกรมจะ set ให้ Port 0 เป็น Port Output 
- ส่วน loop โปรแกรมจะสั่งให้วนลูป ทุกครึ่งวินาที และนับ cnt++ (นับ count) ไปเรื่อยๆ เมื่อ count เป็นเลขคี่ ให้ ON หมายความว่า ส่งค่า 1 ไปที่ Port 0 แต่ถ้า count เป็นเลขคู่ ให้ OFF ค่าของ Port จะเป็น Port 0

4. ทำการ upload โปรแกรม 02_Scan-Wifi เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม
ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

![รูป 2](https://user-images.githubusercontent.com/80879886/112192949-02544100-8c3a-11eb-9bff-e4e8ba1b2ede.JPG)

![รูป 3](https://user-images.githubusercontent.com/80879886/112192953-02ecd780-8c3a-11eb-8cdd-6b583c8b505e.JPG)


6. 
