# การทดลองที่ 4 เรื่อง การเขียนโปรแกรมอินพุทสัญญาณดิจิทัล

## วัตถุประสงค์
1.	เพื่อศึกษาการรันโปรแกรม Input ที่มาจากภายนอกเข้ามาภายในตัว Microcontroller 
2.	เพื่อนำ Microcontroller ที่ถูกเขียนโปรแกรมแล้วไปประยุกต์ใช้กับอุปกณ์อื่น 

## อุปกรณ์ที่ใช้
1.	Microcontroller (ESP01) 
2.	อุปกรณ์เชื่อมต่อ USB (USB to Serial)
3.	คอมพิวเตอร์ใช้รันโปรแกรม
4.	Adapter ที่ต่อด้วยสาย Port 0 (สายสีขาว) กับสาย Port 2 (สายสีเหลือง)
5.	หลอดไฟ LED
6.	เซ็นเซอร์แสงที่ต่ออยู่กับตัวต้านทาน

## ศึกษาข้อมูลเบื้องต้น
1. 04 run example 4 : https://youtu.be/nFqoZT26U5k
2. src code ของตัวอย่างโปรแกรม 04_Input-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/04_Input-Port/src/main.cpp


## วิธีการทำการทดลอง
1. เสียบตัว Adapter เข้ากับ USB to Serial แล้วค่อยเสียบตัวMicrocontroller บน Adapter

![รูป](https://user-images.githubusercontent.com/80879886/112273121-92809d80-8caf-11eb-94e9-bd9395e1861f.JPG)

2. เข้า command prompt เพื่อดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
- พิมพ์ **cd pattani** เพื่อเข้าไปในโฟลเดอร์ 

3.เลือกใช้โปรแกรมตัวอย่างที่ 4
- พิมพ์ **cd 04_Input-Port**
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
จากโปรแกรมที่ 4 จะแสดงข้อมูลแบ่งเป็น 2 ส่วนคือ 
- ส่วน set up โปรแกรมจะ set ให้ Port 0 (สายสีขาว) เป็น Port Input และ Port 2 (สายสีเหลือง) เป็น Port Output
- ส่วน loop โปรแกรมจะสั่งให้วนลูป อ่านข้อมูลจาก Port 0 ข้อมูลที่อ่านได้จะเป็นสัญญาณดิจิตอล (แสดงผล 0 หรือ 1) ถ้าแสดงผลเป็น 1 ให้ LOW ไปที่ Port 2 คือหลอดไฟ LED จะดับ ถ้าแสดงผลเป็น 0 ให้ HIGH ไปที่ Port 2 คือหลอดไฟ LED จะติด


4. ทำการ upload โปรแกรม 04_Input-Port เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม
ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

![รูป](https://user-images.githubusercontent.com/80879886/112273278-bf34b500-8caf-11eb-8823-5fe4e9af2bea.JPG) 
![รูป](https://user-images.githubusercontent.com/80879886/112273281-c065e200-8caf-11eb-899e-bae8385e2f63.JPG)

5. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor** จะแสดงผลได้ดังรูป

![รูป](https://user-images.githubusercontent.com/80879886/112273410-e68b8200-8caf-11eb-9a3e-934c02f0f361.JPG)

6. นำสายไฟเส้นสีขาว (Port 0)  ไปจิ้มเข้าช่องเดียวกันกับสายสีดำที่ให้สัญญาณ Input เป็น 0  Output ที่ได้จะแสดงผล read 0 (ไฟติด) ถ้านำไปจิ้มเข้าช่องเดียวกันกับสายสีแดงที่ให้สัญญาณ Input เป็น 1 Output ที่ได้จะแสดงผล read 1 (ไฟไม่ติด)

![รูป](https://user-images.githubusercontent.com/80879886/112277082-fad17e00-8cb3-11eb-9553-7f3daeffcbb3.jpg)
![รูป](https://user-images.githubusercontent.com/80879886/112277077-f9a05100-8cb3-11eb-8365-ffa5d42b58bb.jpg)

7.เมื่อกดปุ่มอัพโหลด จะทำให้ Port 0 เป็น read 0 (ไฟติด) ถ้าไม่กดปุ่ม Port 0 จะเป็น read 1 (ไฟไม่ติด)

![รูป](https://user-images.githubusercontent.com/80879886/112277083-fb6a1480-8cb3-11eb-8015-f6f702fa11fd.jpg) 
![รูป](https://user-images.githubusercontent.com/80879886/112277088-fc02ab00-8cb3-11eb-9aa2-aa2897823b0a.jpg)

8. นำขาของตัวต้านทานที่ไม่ได้ต่อกับเซ็นเซอร์แสง มาต่อเข้ากับไฟเลี้ยง 3 V.(ตรงสายสีแดง) และนำขาตัวต้านทานที่ต่ออยู่กับเซ็นเซอร์แสง มาต่อเข้าไปใน Port 0 ส่วนขาที่เหลือต่อเข้ากับเส้นสีดำ(Ground) และนำสายไฟเส้นสีขาว (Input) ไปต่อเข้ากับ Port 0 

![รูป](https://user-images.githubusercontent.com/80879886/112277090-fc02ab00-8cb3-11eb-9e50-c22e261ea124.jpg) 
![รูป](https://user-images.githubusercontent.com/80879886/112277091-fc9b4180-8cb3-11eb-8114-b75489c9076e.jpg) 
![รูป](https://user-images.githubusercontent.com/80879886/112277095-fd33d800-8cb3-11eb-9b04-484d2d9bcb8c.jpg) 
![รูป](https://user-images.githubusercontent.com/80879886/112277099-fdcc6e80-8cb3-11eb-8493-69a7f4fc3fe0.jpg)

9. เมื่อนำหน้าเซ็นเซอร์แสง โดนแสงสว่าง Output จะแสดงผล read 0 (ไฟติด) แต่ถ้านำนิ้วไปปิดหน้าเซ็นเซอร์แสง ไม่ให้โดนแสง Output จะแสดงผล read 1 (ไฟไม่ติด)


![รูป](https://user-images.githubusercontent.com/80879886/112277101-fdcc6e80-8cb3-11eb-8c7f-412281f6b625.jpg) 
![รูป](https://user-images.githubusercontent.com/80879886/112277103-fe650500-8cb3-11eb-948a-844130197974.jpg)



## การบันทึกผลการทดลอง
1. เมื่ออัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** เพื่อแสดงผลโปรแกรมและสังเกตุผลจากการส่องสว่างของหลอด LED จะเห็นว่า
เมื่อนำสายไฟเส้นสีขาว (Port 0) ไปจิ้มเข้าช่องเดียวกันกับสายสีดำที่ให้สัญญาณ Input เป็น 0 Output ที่ได้จะแสดงผล read 0 (ไฟติด)
ถ้านำไปจิ้มเข้าช่องเดียวกันกับสายสีแดงที่ให้สัญญาณ Input เป็น 1 Output ที่ได้จะแสดงผล read 1 (ไฟไม่ติด)
และเมื่อกดปุ่มอัพโหลด จะทำให้ Port 0 แสดงผลเป็น read 0 (ไฟติด) ถ้าไม่กดปุ่ม Port 0 จะแสดงผลเป็น read 1 (ไฟไม่ติด) เพราะปุ่มอัพโหลดถูกต่อเข้าอยู่กับ Port 0
2. เมื่อนำ Microcontroller มาต่อเข้ากับเซ็นเซอร์แสง จะเห็นว่าหน้าเซ็นเซอร์แสงที่โดนแสงสว่าง ไฟจะติด แต่ถ้านำนิ้วไปปิดหน้าเซ็นเซอร์แสงไม่ให้โดนแสง ไฟจะดับ


## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมอินพุทสัญญาณดิจิทัล โดยเลือกโปรแกรม 04_Input-Port มาเขียน ผลลัพธ์ที่แสดงออกมาจะดูได้จาก Input ที่ Port 0 ถ้า Input เป็น 1 ไฟจะติด และถ้า Input เป็น 0 ไฟจะดับ ดังนั้น สัญญาณ Input จาก Port 0 จะเป็นตัวควบคุมการติด - ดับของหลอดไฟ และเมื่อนำตัว Microcontroller ที่ถูกเขียนโปรแกรมแล้ว ไปต่อเข้ากับเซ็นเซอร์แสง จะสังเกตุได้ว่าถ้าเอานิ้วไปปิดหน้าเซ็นเซอร์แสงไม่ให้โดนแสง จะทำให้ค่า Input เป็น 1 ไฟจะดับ และเมื่อไม่มีอะไรมาบังเซ็นเซอร์แสง จะทำให้ค่า Input เป็น 0 ไฟจะติด

## คำถามหลังการทดลอง
 



