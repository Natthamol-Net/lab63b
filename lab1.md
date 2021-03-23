# การทดลองที่ 1 เรื่อง การเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์

## วัตถุประสงค์
1. เพื่อศึกษาวิธีการเขียนโปรแกรมด้วย PlatformIO ลงบน Microcontroller (ESP01)
2. เพื่อให้เข้าใจการทำงานของโปรแกรมที่รันลงไปใน Microcontroller (ESP01)

## อุปกรณ์ที่ใช้
1. Microcontroller (ESP01)
2. อุปกรณ์เชื่อมต่อ USB (USB to Serial)

## ศึกษาข้อมูลเบื้องต้น
1. 01 run example 1 : https://youtu.be/NLIUsWLEpmg
2. src code ของตัวอย่างโปรแกรม 01_Serial-Monitor : https://github.com/choompol-boonmee/lab63b/blob/master/examples/01_Serial-Monitor/src/main.cpp
3. ศึกษาใน https://platformio.org/ ว่าตัว Microcontroller สามารถใช้ได้หลากหลาย และมีวิธีการเขียน ภาษาที่ใช้เขียนโปรแกรมที่แตกต่างกัน

## วิธีการทำการทดลอง
1. ต่อ Microcontroller เข้ากับ USB to Serial

![รูป 1](https://user-images.githubusercontent.com/80879886/112181282-dda69c00-8c2e-11eb-8f3f-1da73447626e.JPG)

2. ดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
- พิมพ์ **cd pattani** เพื่อเข้าไปในโฟลเดอร์ 
- พิมพ์ Is แสดงโปรแกรมตัวอย่าง ในโฟลเดอร์นี้มีโปรแกรมอยู่ 9 โปรแกรม

![รูป 2](https://user-images.githubusercontent.com/80879886/112181768-4aba3180-8c2f-11eb-80ea-9dbb0eafad7b.jpg)

3. เลือกใช้โปรแกรมตัวอย่างที่ 1
- พิมพ์ **cd 01_Serial-Monitor**
- พิมพ์ **vi src/main.cpp** เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
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
```

จากโปรแกรมที่ 1 จะแสดงข้อมูลแบ่งเป็น 2 ส่วนคือ 
- ส่วน set up จะ set Serial port ที่ความเร็ว 115200
- ส่วน loop จะมีตัวแปร cnt++ (ตัวแปร count) แสดงผลเพิ่มไปเรื่อยๆ และให้หน่วงเวลา 1 วินาที 

4. แสดง configuration file ของโปรแกรมที่ 1 
- พิมพ์ **vi platformio.ini** เพื่อเข้าไปยัง configuration file ของโปรแกรมนั้น

![รูป 3](https://user-images.githubusercontent.com/80879886/112181816-54439980-8c2f-11eb-81b6-d09e6b81b0de.jpg)

ซึ่งจะแสดงข้อมูลว่าตัว Microcontroller เป็นผลิตภัณฑ์ของบริษัทใด บอร์ดชื่ออะไร ใช้วิธีเขียนโปรแกรมแบบไหน พอร์ตที่ใช้ติดต่อเป็นพอร์ตอะไร 

5. ทำการ upload โปรแกรม 01_Serial-Monitor เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม

![รูป 4](https://user-images.githubusercontent.com/80879886/112181835-586fb700-8c2f-11eb-98dc-0f203cf14230.jpg)

6. ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

![รูป 5](https://user-images.githubusercontent.com/80879886/112181876-61f91f00-8c2f-11eb-9095-ed3736448c66.JPG)

7. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor** จะแสดงผลได้ดังรูป

![รูป 6](https://user-images.githubusercontent.com/80879886/112185010-6410ad00-8c32-11eb-8030-456cc853de8c.JPG)

## การบันทึกผลการทดลอง
เมื่อทำการอัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว จะแสดงผลลัพธ์ด้วยการพิมพ์คำสั่ง **pio device monitor** 
จะเห็นว่าตัวแปร count ที่เริ่มตั้งแต่ 0 จะถูก increment และถูกแสดงผลทุกๆ 1 วินาที และเมื่อลองกดปุ่มรีเซ็ต (สีแดง) Microcontroller จะถูกรีเซ็ตและเริ่มนับ 1 ใหม่

![รูป 7](https://user-images.githubusercontent.com/80879886/112186517-c9b16900-8c33-11eb-9064-003e2b1fc8b0.JPG)

## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมเพื่อรันบนไมโครคอนโทรเลอร์ โดยเลือกโปรแกรม 01_Serial-Monitor มาเขียน ซึ่งจะเป็นโปรแกรมเพิ่มจำนวนตัวแปร count ในทุกๆ 1 วินาที ผลลัพธ์ที่แสดงออกมาตัวแปร count จะเปลี่ยนแปลงทุกๆ 1 วินาที ตามโปรแกรมที่เขียนลงไป ซึ่งสามารถนำโปรแกรมนี้ไปประยุกต์ใช้กับการนับค่าตัวเลขที่เพิ่มขึ้นและมีเวลาเข้ามาเกี่ยวข้อง เช่น นาฬิกาจับเวลา 

## คำถามหลังการทดลอง


