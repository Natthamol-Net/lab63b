# การทดลองที่ 7 เรื่อง การประยุกต์ใช้โปรแกรม

## วัตถุประสงค์
1. เพื่อศึกษาวิธีการประยุกต์ใช้โปรแกรมให้มีความซับซ้อนมากขึ้น
2. เพื่อให้เข้าใจการทำงานโดยรวมของโปรแกรมที่รันลงไปใน Microcontroller (ESP01)

## อุปกรณ์ที่ใช้
1.	Microcontroller (ESP01) 
2.	อุปกรณ์เชื่อมต่อ USB (USB to Serial)
3.	คอมพิวเตอร์ใช้รันโปรแกรม
4.	Adapter ที่ต่อด้วยสาย Port 0, Port 1, Port 2, Port 3
5.	หลอดไฟ LED 2 หลอด

## ศึกษาข้อมูลเบื้องต้น
1. 04 run example 4 : https://youtu.be/nFqoZT26U5k
2. src code ของตัวอย่างโปรแกรม 04_Input-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/04_Input-Port/src/main.cpp


## วิธีการทำการทดลอง
1. เสียบตัว Adapter เข้ากับ USB to Serial แล้วค่อยเสียบตัว Microcontroller บน Adapter
2. เลือกใช้โปรแกรมตัวอย่างที่ 4
- พิมพ์ **vi src/main.cpp** เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
```javascript
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, INPUT);
	pinMode(2, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	int val = digitalRead(0);
	Serial.printf("======= read %d\n", val);
	if(val==1) {
		digitalWrite(2, LOW);
	} else {
		digitalWrite(2, HIGH);
	}
	delay(100);
}
```
3.จากโปรแกรมที่ 4 ได้ทำการเพิ่ม Port และเปลี่ยน delay ให้มีการกระพริบไฟในแต่ละครั้งในเวลาที่ไม่เท่ากัน
```javascript
#include <Arduino.h>
#include <ESP8266WiFi.h>

int cnt = 0;

void setup()
{
	Serial.begin(115200);
	pinMode(0, INPUT);
  pinMode(1, INPUT);
	pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
	Serial.println("\n\n\n");
}

void loop()
{
	int val = digitalRead(0);
  int a = digitalRead(1);
  Serial.printf("======= read %d\n", val);
	if(val==1) and (a==1) {
		digitalWrite(2, LOW);
    digitalWrite(3, HIGH);
	} else {
		digitalWrite(2, HIGH);
    digitalWrite(3, LOW);
	}
  
  for cnt in range(1,2+1);
  Serial.printf("PATTANI :%d\n",cnt);
  int b = cnt ;
  int d = b * 1000;
	delay(d);
}
```
จากโปรแกรมที่ 4 ที่ได้ทำการปรับเปลี่ยน จะแสดงข้อมูลแบ่งเป็น 2 ส่วนคือ 
- ส่วน set up โปรแกรมจะ set ให้ Port 0, Port 1 เป็น Port Input และ Port 2, Port 3 เป็น Port Output
- ส่วน loop โปรแกรมจะสั่งให้วนลูป โดยอ่านข้อมูลจาก Port 0 และ Port 1 ข้อมูลที่อ่านได้จะเป็นสัญญาณดิจิตอล(แสดงผล 0 หรือ 1) ถ้าแสดงผลเป็น 1 ให้ LOW ไปที่ Port 2 คือหลอดไฟ LED หลอดแรกจะดับและให้ HIGH ไปที่ Port 3 คือหลอดไฟ LED อีกหลอดจะติดโดยใช้เวลา delay คือ 1 วินาที ถ้าแสดงผลเป็น 0 ให้ HIGH ไปที่ Port 2 คือหลอดไฟ LED หลอดแรกจะติดและให้ LOW ไปที่ Port 3 คือหลอดไฟ LED อีกหลอดจะดับโดยใช้เวลา delay คือ 2 วินาที

4. ทำการ upload โปรแกรม 04_Input-Port เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม
ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

5. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor**

6. นำสายไฟของ Port 0 และ Port 1 ไปจิ้มเข้าช่องเดียวกันกับสายสีดำที่ให้สัญญาณ Input เป็น 0 และลองนำสายไฟของ Port 0 และ Port 1 ไปจิ้มเข้าช่องเดียวกันกับสายสีแดงที่ให้สัญญาณ Input เป็น 1 และสังเกตุผลจากความสว่างของหลอด LED

7.ลองกดปุ่มอัพโหลดจะทำให้ Port 0 และ Port 1 อ่านเป็น read 0 และไม่กดปุ่มอัพโหลดจะทำให้ Port 0 และ Port 1 อ่านเป็น read 1 และสังเกตุผลจากความสว่างของหลอด LED

## การบันทึกผลการทดลอง
เมื่ออัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว พิมพ์คำสั่ง pio device monitor เพื่อแสดงผลโปรแกรมและสังเกตุผลจากการส่องสว่างของหลอด LED จะเห็นว่า เมื่อนำสายไฟของ Port 0 และ Port 1 ไปจิ้มเข้าช่องเดียวกันกับสายสีดำที่ให้สัญญาณ Input เป็น 0 Output ที่ได้ใน Port 2 จะแสดงผล read 0 ไฟจะติด แต่ใน Port 3 เมื่อแสดงผล read 0 ไฟจะดับ ถ้านำสายไฟของ Port 0 และ Port 1 ไปจิ้มเข้าช่องเดียวกันกับสายสีแดงที่ให้สัญญาณ Input เป็น 1 Output ที่ได้ใน Port 2 จะแสดงผล read 1 ไฟจะดับ แต่ใน Port 3 เมื่อแสดงผล read 1 ไฟจะติด
และเมื่อกดปุ่มอัพโหลดจะทำให้ Port 0 และ Port 1 อ่านเป็น read 0 ที่ Port 2 ไฟจะติด และที่ Port 3 ไฟจะไม่ติด ถ้าไม่กดปุ่มอัพโหลดจะทำให้ Port 0 และ Port 1 อ่านเป็น read 1 ที่ Port 2 ไฟจะไม่ติด และที่ Port 3 ไฟจะติด

## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมอินพุทสัญญาณดิจิทัล โดยเลือกโปรแกรม 04_Input-Port มาเขียน ผลลัพธ์ที่แสดงออกมาจะดูได้จาก Input ที่ Port 0 และ Port 1 ถ้า Input เป็น 1 Output ที่ Port 2 ไฟจะติด แต่ที่ Port 3 ไฟจะดับ และถ้า Input เป็น 0 ที่ Port 2 ไฟจะดับ แต่ที่ Port 3 ไฟจะติด ดังนั้น สัญญาณ Input จาก Port 0 และ Port 1 จะเป็นตัวควบคุมการติด - ดับของหลอดไฟ ซึ่งสามารถนำไปประยุกต์ใช้ได้กับการควบคุมการเปิด - ปิด หลอดไฟหลายๆดวงได้พร้อมกัน หรือควบคุมการเปิด - ปิดอุปกรณ์ไฟฟ้าหลายๆเครื่องได้พร้อมกัน


