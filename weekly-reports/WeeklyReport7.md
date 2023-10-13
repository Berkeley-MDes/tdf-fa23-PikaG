# Weekly Report 7 - 10/5/2023 - 10/12/2023

## Summary
This week, 

## Project 2 Progress Report




**Unity Interaction**
https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/603a7b18-2f75-4b48-b4d3-2091e7d28cf1








**Code**
```
#include <Photon.h>
#include <Adafruit_VC0706.h> // 用于摄像头控制的库
#include <SD.h> // 用于SD卡操作的库

// 定义引脚
int soilMoisturePin = A0; // 土壤湿度传感器连接的引脚
int sunlightPin = A1;     // 阳光传感器连接的引脚
int temperaturePin = A2;  // 温度传感器连接的引脚
int ledPin = D7;          // LED灯连接的引脚
int sdCardPin = SS;       // SD卡连接的引脚

// 初始化摄像头
Adafruit_VC0706 cam = Adafruit_VC0706(&Serial1);

void setup() {
  // 初始化串口通信
  Serial.begin(9600);
  
  // 设置LED引脚为输出
  pinMode(ledPin, OUTPUT);

  // 初始化SD卡
  if (!SD.begin(sdCardPin)) {
    Serial.println("SD卡初始化失败");
    return;
  }

  // 初始化摄像头
  if (cam.begin()) {
    Serial.println("摄像头初始化成功");
    cam.setImageSize(VC0706_640x480); // 设置图像分辨率
  } else {
    Serial.println("摄像头初始化失败");
  }
}

void loop() {
  // 读取土壤湿度值
  int soilMoistureValue = analogRead(soilMoisturePin);
  Serial.print("土壤湿度: ");
  Serial.println(soilMoistureValue);

  // 读取阳光值
  int sunlightValue = analogRead(sunlightPin);
  Serial.print("阳光强度: ");
  Serial.println(sunlightValue);

  // 读取温度值
  int temperatureValue = analogRead(temperaturePin);
  Serial.print("温度: ");
  Serial.println(temperatureValue);

  // 根据条件点亮LED灯
  if (soilMoistureValue < 500 && sunlightValue > 600 && temperatureValue > 500) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }

  // 检查SD卡是否满
  if (SD.card()->isFull()) {
    Serial.println("SD卡已满");
    // 亮另一个灯，提示SD卡已满
    // 你可以添加适当的代码来控制另一个LED灯
  }

  // 拍摄图像并保存到SD卡
  if (cam.takePicture()) {
    Serial.println("拍摄图像...");
    File imgFile = SD.open("image.jpg", FILE_WRITE);
    uint8_t *buffer;
    uint16_t jpglen;
    if (cam.readPicture(buffer, &jpglen)) {
      Serial.println("保存图像到SD卡...");
      imgFile.write(buffer, jpglen);
      imgFile.close();
      cam.resumeVideo();
    } else {
      Serial.println("图像捕获失败");
    }
  }

  // 延迟一段时间，以便观察数据
  delay(1000);
}
```



## Seculation
