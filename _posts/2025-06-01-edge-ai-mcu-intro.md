---
layout: post # 指定文章佈局，通常是 post
title: EdgeAI MCU 簡介
date: 2025-06-01 08:00:00 +0800 # 發表日期和時間 (請根據您當前的時區調整 +0800 代表 UTC+8)
categories: [邊緣運算] # 文章分類，您可以自訂
tags: [EdgeAI-MCU, AMB82-mini] # 文章標籤，您可以自訂
description: AMB82-mini 簡介與開發環境介紹
mathjax: false # 如果這篇文章不需要顯示數學公式，請設false
comments: false # 如果這篇文章需要啟用評論，請設為 true
---

## AMB82-mini 
```
開發板教材網址：https://github.com/rkuo2000/EdgeAI-AMB82mini
```

```
LLM服務器程式範例： [AmebaPro2_server/*.py](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/AmebaPro2_server)
Arduino 程式範例： [Arduino/AMB82-mini/](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini)
```

自強基金會 WiFi 
```
SSID: TCFSTWIFI.ALL
Pass: 035623116
```

---
## AI 簡介

### [AI 簡介](https://rkuo2000.github.io/AI-course/lecture/2024/08/01/AI-Brief.html)

### [AI 硬體介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/01/AI-Hardwares.html)

---
## 開發板介紹

### RTL8735B晶片簡介
32-bit Arm v8M, up to 500MHz, 768KB ROM, 512KB RAM, 16MB Flash (MCM embedded DDR2/DDR3L up to 128MB)<br>
802.11 a/b/g/n WiFi 2.4GHz/5GHz, BLE 5.1, *NN Engine 0.4 TOPS*, Crypto Engine, Audio Codec, ...<br>

---
### [HUB 8735 Ultra](https://robotkingdom.com.tw/product/hub-8735-ultra/)
#### [https://github.com/ideashatch/HUB-8735](https://github.com/ideashatch/HUB-8735)

![](http://winstouch.com.tw/Util/GetPicture.aspx?PicturePath=/UploadFile/IMG_17188933653479.jpg&QueryWidth=400)
![](http://winstouch.com.tw/Util/GetPicture.aspx?PicturePath=/UploadFile/IMG_172407964226684.jpg&QueryWidth=800)

[![](https://markdown-videos-api.jorgenkh.no/youtube/-_NMUnY0kK4)](https://youtu.be/-_NMUnY0kK4)

---
### [AMB82-mini](https://www.icshop.com.tw/products/368030501864)
#### [Ameba Arduino](https://www.amebaiot.com/en/ameba-arduino-summary/)

![](https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/AMB82-mini.png?raw=true)
![](https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/AMB82-mini_kit.png?raw=true)
<p><img src="https://github.com/rkuo2000/EdgeAI-MCU/blob/main/assets/AMB82-MINI_pinout.png?raw=true"></p>

---
## Arduino IDE使用介紹

### [Arduino IDE 2.3.6](https://www.arduino.cc/en/software) 下載 & 安裝
<p><img width="50%" height="50%" src="https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/Arduino_IDE.png?raw=true"></p>

---
### 偏好設定 (Preferences)
**Hub8735 ultra**<br>
`https://raw.githubusercontent.com/ideashatch/HUB-8735/main/amebapro2_arduino/Arduino_package/ideasHatch.json`<br>

**AMB82-mini**<br>
**main** `https://github.com/Ameba-AIoT/ameba-arduino-pro2/raw/main/Arduino_package/package_realtek_amebapro2_index.json`<br>
**dev** `https://github.com/Ameba-AIoT/ameba-arduino-pro2/raw/dev/Arduino_package/package_realtek_amebapro2_early_index.json`<br>

![](https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/AMB82-mini_Arduino_IDE_preference.png?raw=true)

### [Ameba AIoT 影片](https://www.youtube.com/@amebaiot7033)
[![](https://markdown-videos-api.jorgenkh.no/youtube/-jQDpDFX2ao)](https://youtu.be/-jQDpDFX2ao)
---
### 選定開發板 AMB82-MINI
Tools > Board Manager > AMB82 package > 4.0.9<br>
<p><img width="75%" height="75%" src="https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/AMB82-mini_Arduino_IDE_BoardManager.png?raw=true"></p>

Serial-monitor = `115200` baud <br>

---
### [Getting Started](https://www.amebaiot.com/en/amebapro2-amb82-mini-arduino-getting-started/)
首先將AMB82-mini板子用MicroUSB線 連接至電腦的USB port<br>
確認UART com port (Ubuntu OS需 `sudo chown usrname /dev/ttyUSB0`)

<p><img width="50%" height="50%" src="https://www.amebaiot.com/wp-content/uploads/2022/12/amb82-mini/P03.png"></p>

**燒錄程式碼：** <br>
* 按下UART_DOWNLOAD按鈕, 再按下RESET按鈕, 放開RESET按鈕, 再放開UART_DOWNLOAD按鈕,板子就進入燒錄模式.
* 然後于Arduino IDE上按下燒錄按鍵`Upload`

---
### [下載 AMB82-Mini 程式範例](https://github.com/rkuo2000/EdgeAI-AmebaPro2/tree/main/Arduino/AMB82-mini)

1. 瀏覽器打開 [EdgeAI-AMB82mini](https://github.com/rkuo2000/EdgeAI-AMB82mini), 點[Code]並選 [Download ZIP]
2. 解壓縮.zip, 並將 Arduino/AMB82-mini 複製到 文件/Arduino下, 成為 `文件/Arduino/AMb82-mini`


