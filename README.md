# 개요
우리는 기존의 데이터 글래스(웨어러블 글래스)의 효율성 대비 높은 가격이라는 문제점을 해결하기위해 30000만원 정도의 낮은 가격으로도 괜찮은 데이터글래스를 제작할 수 있다는 것을 보여주기로 하였다. 안경에 데이터글래스를 부착해 데이터를 눈으로 확인할 수 있도록 만드는 프로젝트이다.

# 준비물
블루투스 모듈
OLED 디스플레이
아두이노 프로 마이크로
충전 회로
리튬  배터리
거울
렌즈
스위치
안경
3D 프린터

# sw 개발 환경
아두이노 스케치와 앱 인벤터2 사용
# dataglass 
#include <SPI.h>

#include <Wire.h>

#include <Adafruit_GFX.h>

#include <Adafruit_SSD1306.h>

#define OLED_RESET 4

Adafruit_SSD1306 display(OLED_RESET);

void setup() { 

Serial.begin(9600); 

display.begin(SSD1306_SWITCHCAPVCC, 0x3D);

display.display();

delay(2000);

display.clearDisplay(); 

}

void loop() {

while(Serial.available() > 0){

String Date = Serial.readStringUntil('|');

Serial.read();

String Time = Serial.readStringUntil('|');

Serial.read();

String Phone = Serial.readStringUntil('|');

Serial.read();

String Text = Serial.readStringUntil('\n');

Serial.read();

}

if(Text == "text" && Phone == "phone")

{ display.println(Date);

display.display();

display.println(Time);

display.display();

display.clearDisplay(); 

}

if (Text != "text" && Phone == "phone"){

display.println(Text);

display.display();

delay(5000);

display.clearDisplay();

}

if (Text == "text" && Phone != "phone"){

display.println(Phone);

display.display();

delay(5000);

display.clearDisplay();

}

}
