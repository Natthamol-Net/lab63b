# การทดลองที่ 6 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)

## วัตถุประสงค์
1.	เพื่อศึกษาการเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์

## อุปกรณ์ที่ใช้
1. Microcontroller (ESP01) 
2. อุปกรณ์เชื่อมต่อ USB (USB to Serial)
3. คอมพิวเตอร์ใช้รันโปรแกรม

## ศึกษาข้อมูลเบื้องต้น
1. 06 run wiri AP : https://youtu.be/T26DVHePlTs
2. src code ของตัวอย่างโปรแกรม 06_Wifi-AP-Web-Server : https://github.com/choompol-boonmee/lab63b/blob/master/examples/06_Wifi-AP-Web-Server/src/main.cpp

## วิธีการทำการทดลอง
1. ต่อตัว Microcontroller เข้ากับ USB to Serial

2. เข้า command prompt เพื่อดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
- พิมพ์ cd pattani เพื่อเข้าไปในโฟลเดอร์

3. เลือกใช้โปรแกรมตัวอย่างที่ 6
- พิมพ์ cd 06_Wifi-AP-Web-Server
- พิมพ์ vi src/main.cpp เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
```javascript
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "MY-ESP8266";
const char* password = "choompol";

IPAddress local_ip(192, 168, 1, 1);
IPAddress gateway(192, 168, 1, 1);
IPAddress subnet(255, 255, 255, 0);

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.softAP(ssid, password);
	WiFi.softAPConfig(local_ip, gateway, subnet);
	delay(100);

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
  server.handleClient();
}
```
เนื่องจากเป็นโปรแกรมที่ต้องการสร้างไวไฟด้วยตัวเอง ดังนั้นต้องกำหนดชื่อ Wifi และ password และก่อนที่จะปล่อยให้คนอื่นมา connect จะต้องกำหนด IP address local_ip, gateway, subnet และเตรียมเว็บเซอร์เวอร์

4. ทำการ upload โปรแกรม 06_Wifi-AP-Web-Server เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม
ขณะที่รันโปรแกรม ให้กดปุ่มอัพโหลด (สีดำ) และ ปุ่มรีเซ็ต (สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

![รูป](https://user-images.githubusercontent.com/80879886/112267109-8e508200-8ca7-11eb-8b51-4b969c28a266.jpg) 

![รูป](https://user-images.githubusercontent.com/80879886/112267794-9230d400-8ca8-11eb-8c69-3118c859e3ba.JPG)

5. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor** จะแสดงผลได้ดังรูป

![รูป](https://user-images.githubusercontent.com/80879886/112267113-8f81af00-8ca7-11eb-9a20-8a8dacfba91d.jpg)

6. ลองใช้คอมพิวเตอร์หรือโทรศัพท์มือถือค้นหา Wifi ที่สร้าง

![รูป](https://user-images.githubusercontent.com/80879886/112267116-901a4580-8ca7-11eb-9a8f-b997b29e38b1.jpg)

## การบันทึกผลการทดลอง
เมื่ออัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว พิมพ์คำสั่ง **pio device monitor** เพื่อแสดงผลโปรแกรม จะขึ้นว่า HTTP server started และลองใช้โทรศัพท์มือถือค้นหา Wifi ที่สร้าง จะพบกับไวไฟที่ได้สร้างขึ้นมาจากการเขียนโปรแกรม

## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP) โดยเลือกโปรแกรม 06_Wifi-AP-Web-Server มาเขียน ผลลัพธ์ที่ได้ เราสามารถสร้างไวไฟแอคเซสพอยต์ (Wifi AP) ขึ้นมาเพื่อให้อุปกร์อื่นๆสามารถ connect กับไวไฟได้

## คำถามหลังการทดลอง



