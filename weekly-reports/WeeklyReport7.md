# Weekly Report 7 - 10/5/2023 - 10/12/2023

## Summary
This week, my primary focus was on Project 2, particularly the software interactive design component. Working with Unity, I successfully constructed an engaging interactive scenario, featuring a 3D cartoon island and a character capable of planting a tree in response to Arduino serial input. Other team members have made significant progress in writing VS code for Photon2 and 3D modeling. 

Moving forward, I'll continue to concentrate on refining the Unity interaction design. This step is crucial for effectively displaying the desired parameters, ensuring a seamless user experience. While there's still some work to be done in figuring out the connection between Photon2 and Unity, I'm confident that we'll overcome this hurdle.

## Project 2 Progress Report

**Software Interaction (Unity)** <p>
https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/603a7b18-2f75-4b48-b4d3-2091e7d28cf1
<p>
  <img width="500" alt="截屏2023-10-12 17 49 29" src="https://github.com/Berkeley-MDes/tdf-fa23-PikaG/assets/74200423/b6956c64-d37c-4bae-99dd-2ed18265f3e7">
</p>


**Hardware Interaction (Photon 2)**
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
Here are some speculations on how to use serial for communication between Photon2 and Unity:
1. **Direct Serial Connection:** Establishing a direct serial connection between Photon2 and Unity can be achieved using a USB cable or Bluetooth module. This would involve configuring both ends to send and receive data in a format that can be easily interpreted by both platforms.

2. **Custom Protocol Design:** Creating a custom communication protocol can streamline data transfer. This involves defining specific message formats, commands, and synchronization signals to ensure accurate and timely information exchange.

3. **Baud Rate Optimization:** Experimenting with different baud rates can help in finding the optimal speed for data transmission. Balancing speed with stability will be key to maintaining a reliable connection.

4. **Error Handling and Validation:** Implementing robust error-checking mechanisms will be crucial to ensure data integrity. This could involve checksums or other verification methods to confirm the accuracy of received data.


