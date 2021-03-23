# การทดลองที่ 3 เรื่อง การเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล

## วัตถุประสงค์
1.	เพื่อศึกษาวิธีการรันโปรแกรมบน Microcontroller ที่ทดลองส่งสัญญาณ output ออกไปสู่ภายนอก
2.	เพื่อนำ Microcontroller ที่ถูกเขียนโปรแกรมแล้วไปประยุกต์ใช้กับอุปกณ์อื่น 

## อุปกรณ์ที่ใช้
1.	Microcontroller (ESP01) 
2.	อุปกรณ์เชื่อมต่อ USB (USB to Serial)
3.	Adapter ที่ต่อด้วยสาย Port 0 (สายสีขาว) กับสาย Port 1 (สายสีเหลือง)
4.	หลอดไฟ LED
5.	Relay
6.	ขั้วชาร์จ หรือ Power Bank

## ศึกษาข้อมูลเบื้องต้น
1. 03 run example 3 : https://youtu.be/CCnN1WJsXQY
2. 03 run relay : https://youtu.be/6JnhaUILGuw
3. src code ของตัวอย่างโปรแกรม 03_Output-Port : https://github.com/choompol-boonmee/lab63b/blob/master/examples/03_Output-Port/src/main.cpp
4. Relay คืออะไร? : https://bedroomlearning.blogspot.com/2016/10/relay.html

## วิธีการทำการทดลอง
1. เสียบตัว Adapter เข้ากับ USB to Serial แล้วค่อยเสียบตัว Microcontroller บน Adapter

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
- ส่วน loop โปรแกรมจะสั่งให้วนลูป ทุกครึ่งวินาที และนับ cnt++ (นับ count) ไปเรื่อยๆ เมื่อ count เป็นเลขคี่ให้ ON แต่ถ้า count เป็นเลขคู่ให้ OFF 

4. ทำการ upload โปรแกรม 02_Scan-Wifi เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม
ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

![รูป 2](https://user-images.githubusercontent.com/80879886/112192949-02544100-8c3a-11eb-9bff-e4e8ba1b2ede.JPG)

![รูป 3](https://user-images.githubusercontent.com/80879886/112192953-02ecd780-8c3a-11eb-8cdd-6b583c8b505e.JPG)


5. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor** จะแสดงผลได้ดังรูป

![รูป 4](https://user-images.githubusercontent.com/80879886/112192956-03856e00-8c3a-11eb-9a3f-7273d08b3249.JPG)

8.ซึ่งจะสังเกตุได้จากการส่องสว่างของหลอดไฟ LED

![รูป](https://user-images.githubusercontent.com/80879886/112196638-cf13b100-8c3d-11eb-9f2a-0daf8c8bef6c.JPG) ![รูป](https://user-images.githubusercontent.com/80879886/112196647-cfac4780-8c3d-11eb-930e-c27a0d276acb.JPG)

6. นำตัว Microcontroller ที่เขียนโปรแกรมไว้แล้วถอดออกจาก Adapter และนำตัว Microcontroller มาเสียบเข้ากับตัว Relay 
 และนำขั้วชาร์จ หรือ Power Bank ต่อเข้ากับ Relay เพื่อจ่ายไฟเข้า Relay และ Microcontroller
 
![รูป](https://user-images.githubusercontent.com/80879886/112192968-05e7c800-8c3a-11eb-8d1b-ab03e1cef970.JPG) 

7. Microcontroller จะควบคุม Relay ให้เปิด - ปิด

## การบันทึกผลการทดลอง
1. เมื่ออัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว พิมพ์ pio device monitor เพื่อแสดงผลโปรแกรม จะเห็นว่าทุกๆ 500 ms. จะแสดงผล ON สลับกับ OFF และเมื่อดูที่หลอด LED จะส่องสว่างที่ Port 0 ในตอนที่แสดงผลเป็น ON และจะดับที่ Port 1 ในตอนที่แสดงผลเป็น OFF
2. เมื่อนำ Microcontroller มาต่อเข้ากับ Relay พร้อมกับทำการจ่ายไฟเข้าไปตัว Microcontroller จะควบคุม การเปิด - ปิด สวิตซ์ของ Relay และได้ยินเสียงหน้าสัมผัสของสวิตช์ไฟ

## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมเอ้าพุทสัญญาณดิจิทัล โดยเลือกโปรแกรม 03_Output-Port มาเขียน ซึ่งเป็นโปรแกรมแสดงผล output โดยผลลัพธืที่แสดงออกมาจะแสดงผล ON สลับกับ OFF ทุกๆ 500 ms. ตามโปรแกรมที่เขียนลงไป และจากการสังเกตุหลอดไฟ LED จะเห็นว่า หลอดไฟจะส่องสว่างที่ Port 0 ในตอนที่แสดงผลเป็น ON สลับกับดับที่ Port 1 ในตอนที่แสดงผลเป็น OFF และเมื่อนำตัว Microcontroller ที่ถูกเขียนโปรแกรมแล้ว ไปต่อเข้ากับ Relay จะเห็นว่า Microcontroller จะเป็นตัวควบคุม การเปิด - ปิด สวิตซ์ของ Relay ที่เป็นไปตามโปรแแกรมที่เราเขียนลงไปในตัว Microcontroller ซึ่งสามารถนำไปประยุกต์ใช้ได้กับวงจรไฟกระพริบเตือนให้ระวังอันตราย, ไฟเลี้ยวรถ และนำไปใช้ในการควบคุมการเปิด - ปิด สวิตช์ของไฟได้ 

## คำถามหลังการทดลอง




