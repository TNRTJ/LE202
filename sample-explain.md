# sample-explain
## LAB 1
### Code 

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
	       int s = cnt % 5 + 1;
	       int d = s * 1000;
	       delay(d);
       }	
1. ส่วน set up (run ครั้งเดียว)
set serial port ที่ความเร็ว 115200 B/s

2. ส่วนฟังก์ชัน loop (run ไปเรื่อยๆ)
จะให้เพิ่มตัวแปร cnt ขึ้นที่ละ 1  แล้วแสดงผลออกมาแล้วเปลี่ยนบรรทัด ซึ่งจะ delay ห่างกัน 1 วินาที

## LAB 2
### Code 

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
			       Serial.print(WiFi.channel(i));
			       delay(10);
		       }
	       }
	       Serial.println("\n\n");
	       delay(10 * 1000);
       }
	
1. ส่วน set up (run ครั้งเดียว)
set serial port ที่ความเร็ว 115200 B/s ,การตั้งค่า WiFi เป็นโหมดสถานี ,ตัดการเชื่อมต่อจากเครื่อข่ายที่เชื่อมต่อไว้ก่อนหน้านี้ ,delay ห่างกัน 100 ms และเว้นบรรทัด 3 บรรทัด

2. ส่วนฟังก์ชัน loop (run ไปเรื่อยๆ)
เริ่มแสกนหา Wifi ,สร้างตัวแปร n ให้แสดงจำนวนเครื่อยข่ายที่พบ ,ถ้าไม่เจอ Wifi ให้แสดงคำว่า NO NETWORK FOUND ,ถ้าเจอก็จะทำการแสดง SSID และ RSSI ซึ่งจะเป็นชื่อและความแรงสัญญาณที่เจอ และ delay การหาห่างกัน 10 ms

## LAB 3
### Code 

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
	
1. ส่วน set up (run ครั้งเดียว)
set serial port ที่ความเร็ว 115200 B/s ,set port 0 เป็น port output และเว้นบรรทัด 3 บรรทัด

2. ส่วนฟังก์ชัน loop (run ไปเรื่อยๆ)
จะให้เพิ่มตัวแปร cnt ขึ้นที่ละ 1 ,ถ้า cnt หารด้วย 2 ลงตัวให้แสดง ON และที่ขา digital ของบอร์ดเป็น HIGH ไฟจะติด ,ถ้าหาก cnt หารด้วย 2 ไม่ลงตัวให้แสดง OFF และที่ขา digital ของบอร์ดเป็น LOW ไฟจะดับและ delay การหาห่างกัน 500 ms

## LAB 4
### Code 

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
	
1. ส่วน set up (run ครั้งเดียว)
set serial port ที่ความเร็ว 115200 B/s ,set port 0 เป็น input ,set port 2 เป็น output และเว้นบรรทัด 3 บรรทัด

2. ส่วนฟังก์ชัน loop (run ไปเรื่อยๆ)
ทำการอ่านค่าจาก port 0 ไปเก็บในตัวแปร val ซึ่งจะมีค่าเป็น 0 หรือ 1 เท่านั้น ,แสดงตัวแปร val แล้วเว้นบรรทัด ,ถ้า val เป็น 1 ให้่ port 2 เป็น LOW ไฟจะดับ ,ถ้าหาก val ไม่ใช่ 1 ให้่ port 2 เป็น HIGH ไฟจะติดและ
delay การหาห่างกัน 100 ms

## LAB 5
### Code 

        	#include <ESP8266WiFi.h>
	       	#include <ESP8266WiFiMulti.h>
       		#include <ESP8266WebServer.h>

	       	const char* ssid = "HI_BMFWIFI_2.4G";		//ชื่อ SSID   ที่สร้างไว้
       		const char* password = "0819110933";		//ชื่อ Password ที่สร้างไว้

	       	ESP8266WebServer server(80);           //เปิดweb server ที่ port 80

	       	int cnt = 0;

	       	void setup(void){
		       	Serial.begin(115200);		
		       	wifiMulti.addAP(ssid, password);

		       	Serial.println("Connecting ...");
		       	int i = 0;
		       	while (wifiMulti.run() != WL_CONNECTED) { 			
	       			delay(1000);			
		       		Serial.print(++i); Serial.print(' ');
	       		}
		       	Serial.println("");
		       	Serial.print("IP address: ");
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
	
1. ส่วน set up (run ครั้งเดียว)
set serial port ที่ความเร็ว 115200 B/s และทำการ connect กับ Wifi ที่เราเลือกไว้ ,set up กับ Web server ถ้ามีการเชื่อมโยงให้แสดงผลออกมาว่า Hello cnt และเพิ่ม cnt ที่ละ 1 ไปเรื่อยๆ

2. ส่วนฟังก์ชัน loop (run ไปเรื่อยๆ)
ตรวจสอบว่ามีคนเรียกหน้าเว็ปแล้วหรือยัง

## LAB 6
### Code 

       #include <ESP8266WiFi.h>
       #include <WiFiClient.h>
       #include <ESP8266WebServer.h>

       const char* ssid = "MY-ESP8266";        //ชื่อ SSID   ที่สร้างไว้
       const char* password = "choompol";      //ชื่อ Password ที่สร้างไว้

       IPAddress local_ip(192, 168, 1, 1);     //กำหนดค่าตัวแปร local_ip
       IPAddress gateway(192, 168, 1, 1);      //กำหนดค่าตัวแปร gateway
       IPAddress subnet(255, 255, 255, 0);     //กำหนดค่าตัวแปร subnet

       ESP8266WebServer server(80);            //เปิดweb server ที่ port 80

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

	
1. ส่วน set up (run ครั้งเดียว)
set serial port ที่ความเร็ว 115200 B/s ,สร้าง Access Point โดยรันคำสั่ง WiFi.softAP() และกำหนด ssid กับ password แล้วบอกว่า IP ตั้งไว้เป็นอะไร

2. ส่วนฟังก์ชัน loop (run ไปเรื่อยๆ)
ตรวจสอบว่ามีคนเรียกหน้าเว็ปแล้วหรือยัง
