# การทดลองที่ 5 เรื่อง การเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์

## วัตถุประสงค์
1.	เพื่อศึกษาการเขียนโปรแกรมเว็บเซอร์เวอร์ผ่าน Wifi

## อุปกรณ์ที่ใช้
1. Microcontroller (ESP01) 
2. อุปกรณ์เชื่อมต่อ USB (USB to Serial)
3. คอมพิวเตอร์ใช้รันโปรแกรม

## ศึกษาข้อมูลเบื้องต้น
1. 05 run wifi : https://youtu.be/VX-QNQcO-b4
2. src code ของตัวอย่างโปรแกรม 05 run wifi : https://github.com/choompol-boonmee/lab63b/blob/master/examples/05_Wifi-Web-Server/src/main.cpp

## วิธีการทำการทดลอง
1. เข้า command prompt เพื่อดูตัวอย่างโปรแกรมที่โฟลเดอร์ pattani
- พิมพ์ **cd pattani** เพื่อเข้าไปในโฟลเดอร์ 

2. เลือกใช้โปรแกรมตัวอย่างที่ 5
- พิมพ์ **cd 05_Wifi-Web-Server**
- พิมพ์ **vi src/main.cpp** เพื่อดูเนื้อหาในโปรแกรม จะขึ้นข้อมูลดังนี้
```javascript
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "HI_BMFWIFI_2.4G";
const char* password = "0819110933";

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid, password);
	while (WiFi.status() != WL_CONNECTED) {
		delay(500);
		Serial.print(".");
	}
	Serial.print("\n\nIP address: ");
	Serial.println(WiFi.localIP());

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
เนื่องจากโปรแกรมนี้ต้องต่อกับ Wifi ดังนั้นต้องเขียนระบุชื่อ Wifi และ password  ซึ่งตัวโปรแกรมจะแบ่งเป็น 2 ส่วนคือ
- ส่วน set up โปรแกรมจะ connect กับ Wifi ที่เลือกไว้ หลังจากนั้นจะ set up ตัว Web server โดยจะแสดงผล Hello cnt โดย cnt จะบวก 1 ขึ้นเรื่อยๆ
- ส่วน loop โปรแกรมจะสั่งให้วนลูปไปเรื่อยๆ

3. ทำการ upload โปรแกรม 04_Input-Port เข้าไปยัง Microcontroller โดยการพิมพ์คำสั่ง **pio run -t upload** เพื่อรันโปรแกรม

![รูป](https://user-images.githubusercontent.com/80879886/112263929-a2de4b80-8ca2-11eb-9aa2-411886e6d367.JPG)

4. เสียบตัว Microcontroller เข้ากับ USB to Serial และกดปุ่มอัพโหลด(สีดำ) และ ปุ่มรีเซ็ต(สีแดง) บน Serial port เพื่อให้ Microcontroller รับโปรแกรมใหม่เข้าไป

5. เมื่อโปรแกรมอัพโหลดเสร็จจะแสดงผลลัพธ์โดย พิมพ์คำสั่ง **pio device monitor** โดยจะเริ่มแสดงผลด้วยการหา Wif, connect Wifi และบอกตัว IP address 

6. นำ ID address ไปทดสอบในเว็บเบราว์เซอร์

## การบันทึกผลการทดลอง
เมื่ออัพโหลดโปรแกรมลงบน Microcontroller เสร็จแล้ว พิมพ์คำสั่ง pio device monitor เพื่อแสดงผลโปรแกรม จะแสดงผลของ IP address แล้วนำไปทดสอบในเว็บเบราว์เซอร์จะขึ้น Hello 1, Hello 2, … โดยจะเปลี่ยนตัวแปร count ไปเรื่อยๆ

## อภิปรายผลการทดลอง
จากการทดลองเขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์ โดยเลือกโปรแกรม 05_Wifi-Web-Server มาเขียน โดยผลลัพธ์ที่แสดงออกมาสามารถนำ IP address ไปทดสอบในเว็บเบราว์เซอร์แล้วขึ้นแสดงผล Hello 1, Hello 2, … โดยเปลี่ยนตัวแปร count ไปเรื่อยๆ ตามโปรแกรมที่เขียนลงไป

## คำถามหลังการทดลอง
