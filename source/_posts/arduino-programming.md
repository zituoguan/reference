---
title: Arduino 编程
date: 2024-05-29 8:58:31
background: bg-[#387f83]
label:
tags: -cpp
  -I/O
categories:
  - 编程
intro: |
  Arduino I/O 编程和 Arduino 板编程速查表。

plugins:
  - copyCode
---

## 入门指南

### 准备必要材料

- Arduino 板：任何型号，如 Arduino Uno、Mega、Nano 等。
- USB 数据线：与您的 Arduino 板兼容（Uno 通常使用 USB Type-A 转 Type-B）。
- 电脑：Windows、macOS 或 Linux。

### 安装 Arduino IDE

- Windows/Mac/Linux
- 前往 Arduino 软件页面。
- 下载对应操作系统的安装程序。
- 运行安装程序并按照说明操作。

### 连接您的 Arduino 板

- 使用 USB 数据线将 Arduino 板连接到您的计算机。
- Arduino 上的电源 LED 应亮起，表示已通电。

### 配置 Arduino IDE

- 打开 Arduino IDE。
- 选择您的电路板：
- 前往 工具 > 开发板 并选择您的 Arduino 板型号（例如 Arduino Uno）。

- 选择端口：

- 前往 工具 > 端口 并选择 Arduino 连接的端口（在 Windows 上通常显示为 COMx，在 macOS 上显示为 /dev/cu.usbmodemxxxx，在 Linux 上显示为 /dev/ttyUSBx）。

## 基本结构

### Setup 和 Loop

```cpp
void setup() {
  // 此处的代码运行一次
}

void loop() {
  // 此处的代码重复运行
}
```

### 注释

```cpp
// 单行注释

/*
多行
注释
*/
```

### 变量

```cpp
int ledPin = 13; // 整数
float voltage = 5.0; // 浮点数
char letter = 'A'; // 字符
String text = "Hello"; // 字符串
```

### 引脚模式

```cpp
pinMode(pin, mode);
```

### 数字 I/O

```cpp
digitalWrite(pin, value);
int value = digitalRead(pin);

```

### 模拟 I/O

```cpp
analogWrite(pin, value);
int value = analogRead(pin);

```

## 串行通信

### 开始串行通信

```cpp
Serial.begin(baudRate);
```

### 打印到串行监视器

```cpp
Serial.print(data);
Serial.println(data);
```

### 从串行监视器读取

```cpp
if (Serial.available()) {
  char data = Serial.read();
}
```

## 控制结构

### If 语句

```cpp
if (condition) {
  // 条件为真时执行的代码
} else {
  // 条件为假时执行的代码
}
```

### For 循环

```cpp
for (initialization; condition; increment) {
  // 要执行的代码
}
```

### While 循环

```cpp
while (condition) {
  // 要执行的代码
}
```

### 函数

```cpp
returnType functionName(parameters) {
  // 要执行的代码
  return value;
}
```

## 库

### 包含库

```cpp
#include <LibraryName.h>
```

### 使用库

```cpp
#include <Servo.h>

Servo myServo;

void setup() {
  myServo.attach(9); // 将舵机连接到引脚 9
}

void loop() {
  myServo.write(90); // 将舵机设置到 90 度
  delay(1000);
  myServo.write(0); // 将舵机设置到 0 度
  delay(1000);
}
```

## 常用函数

### Delay

```cpp
delay(milliseconds);

```

### Millis

```cpp
unsigned long currentTime = millis();

```

### Map

```cpp
long outputValue = map(inputValue, fromLow, fromHigh, toLow, toHigh);

```

### Random

```cpp
long randomValue = random(max);
long randomValue = random(min, max);

```

### Random Seed

```cpp
randomSeed(analogRead(0)); // 从模拟引脚 0 获取种子

```

## 传感器和模块

### 使用 DHT 传感器读取温度

```cpp
#include <DHT.h>

#define DHTPIN 2     // DHT 传感器连接的引脚
#define DHTTYPE DHT11   // DHT 11

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();

  Serial.print("湿度: ");
  Serial.print(humidity);
  Serial.print(" %\t");
  Serial.print("温度: ");
  Serial.print(temperature);
  Serial.println(" *C");

  delay(2000);
}
```

### LED 闪烁

```cpp
const int ledPin = 13;

void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);  // 打开 LED
  delay(1000);                 // 等待 1 秒
  digitalWrite(ledPin, LOW);   // 关闭 LED
  delay(1000);                 // 等待 1 秒
}

```

### 读取按钮输入

```cpp
const int buttonPin = 2;  // 按钮连接的引脚
const int ledPin = 13;    // LED 连接的引脚

void setup() {
  pinMode(buttonPin, INPUT);  // 将按钮引脚设置为输入
  pinMode(ledPin, OUTPUT);    // 将 LED 引脚设置为输出
}

void loop() {
  int buttonState = digitalRead(buttonPin);  // 读取按钮状态

  if (buttonState == HIGH) {
    digitalWrite(ledPin, HIGH);  // 打开 LED
  } else {
    digitalWrite(ledPin, LOW);   // 关闭 LED
  }
}


```

### 模拟输入

```cpp
const int potPin = A0;    // 电位器连接的引脚
const int ledPin = 9;     // LED 连接的引脚

void setup() {
  pinMode(ledPin, OUTPUT);  // 将 LED 引脚设置为输出
}

void loop() {
  int potValue = analogRead(potPin);  // 读取电位器值
  int ledBrightness = map(potValue, 0, 1023, 0, 255);  // 将值映射到 0 到 255 的范围

  analogWrite(ledPin, ledBrightness);  // 设置 LED 亮度
  delay(10);  // 短暂延迟使 LED 平滑变化
}


```

### 串行通信

```cpp
void setup() {
  Serial.begin(9600);  // 以 9600 波特率启动串行通信
}

void loop() {
  Serial.println("Hello, world!");  // 向串行监视器发送消息
  delay(1000);  // 等待 1 秒
}


```

### 温度传感器

```cpp
const int tempPin = A0;  // TMP36 传感器连接的引脚

void setup() {
  Serial.begin(9600);  // 以 9600 波特率启动串行通信
}

void loop() {
  int tempValue = analogRead(tempPin);  // 读取传感器值
  float voltage = tempValue * (5.0 / 1023.0);  // 将值转换为电压
  float temperatureC = (voltage - 0.5) * 100;  // 将电压转换为摄氏温度

  Serial.print("温度: ");
  Serial.print(temperatureC);
  Serial.println(" C");
  delay(1000);  // 等待 1 秒
}


```

### RGB LED 控制

```cpp
const int redPin = 9;
const int greenPin = 10;
const int bluePin = 11;

const int potRedPin = A0;
const int potGreenPin = A1;
const int potBluePin = A2;

void setup() {
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {
  int redValue = analogRead(potRedPin);
  int greenValue = analogRead(potGreenPin);
  int blueValue = analogRead(potBluePin);

  analogWrite(redPin, map(redValue, 0, 1023, 0, 255));
  analogWrite(greenPin, map(greenValue, 0, 1023, 0, 255));
  analogWrite(bluePin, map(blueValue, 0, 1023, 0, 255));

  delay(10);
}

```

### 超声波传感器

```cpp
const int trigPin = 9;
const int echoPin = 10;

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
}

void loop() {
  long duration;
  int distance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("距离: ");
  Serial.print(distance);
  Serial.println(" cm");
  delay(1000);
}
```

### 控制舵机

```cpp
#include <Servo.h>

Servo myServo;
const int potPin = A0;

void setup() {
  myServo.attach(9);  // 将舵机连接到引脚 9
}

void loop() {
  int potValue = analogRead(potPin);  // 读取电位器值
  int angle = map(potValue, 0, 1023, 0, 180);  // 将值映射到 0 到 180 度的角度

  myServo.write(angle);  // 设置舵机位置
  delay(15);  // 短暂延迟让舵机到达位置
}

```

### 在 LCD 上显示文本

```cpp
#include <LiquidCrystal.h>

// 使用接口引脚编号初始化库
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup() {
  // 设置 LCD 的列数和行数
  lcd.begin(16, 2);
  // 向 LCD 打印消息
  lcd.print("Hello, World!");
}

void loop() {
  // 将光标设置到第 0 列，第 1 行（第二行）
  lcd.setCursor(0, 1);
  // 打印自复位以来的秒数
  lcd.print(millis() / 1000);
}
```

## 使用 NRF24L01 进行无线通信

### 发射器代码

```cpp
#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>

RF24 radio(9, 10);  // CE, CSN 引脚

const byte address[6] = "00001";  // 地址

void setup() {
  radio.begin();
  radio.openWritingPipe(address);
  radio.setPALevel(RF24_PA_MIN);
  radio.stopListening();
}

void loop() {
  const char text[] = "Hello";
  radio.write(&text, sizeof(text));
  delay(1000);
}
```

### 接收器代码

```cpp
#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>

RF24 radio(9, 10);  // CE, CSN 引脚

const byte address[6] = "00001";  // 地址

void setup() {
  Serial.begin(9600);
  radio.begin();
  radio.openReadingPipe(0, address);
  radio.setPALevel(RF24_PA_MIN);
  radio.startListening();
}

void loop() {
  if (radio.available()) {
    char text[32] = "";
    radio.read(&text, sizeof(text));
    Serial.println(text);
  }
}

```

## 另请阅读

- [Arduino 官网](https://www.arduino.cc/en/software)
