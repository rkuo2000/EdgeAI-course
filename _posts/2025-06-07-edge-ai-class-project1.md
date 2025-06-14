---
layout: post # 指定文章佈局，通常是 post
title: AI 輔助分類回收系統
date: 2025-06-07 15:40:00 +0800 # 發表日期和時間 (請根據您當前的時區調整 +0800 代表 UTC+8)
categories: [1131邊緣運算課] # 文章分類，您可以自訂
tags: [入門,學習,blog] # 文章標籤，您可以自訂
description: 這篇文章會講解我邊緣運算的第一個專案 AI 輔助分類回收系統
mathjax: false # 如果這篇文章不需要顯示數學公式，請設false
comments: false # 如果這篇文章需要啟用評論，請設為 true
permalink: /AI-Class/project1/
---


本報告旨在介紹一個基於邊緣 AI 技術的輔助回收系統。該系統利用 Realtek AMB82_mini 微控制器作為核心處理單元，整合影像辨識與語音互動功能，旨在實現對回收物品的自動識別與語音指引，從而提升回收效率與正確性。

- [功能](#功能)
- [GenAI程式碼設計流程](#genai程式碼設計流程)
- [程式碼](#程式碼)
  - [程式重點 \<**提示字:** *請問這個回收物是什麼?請用中文回答*\>](#程式重點-提示字-請問這個回收物是什麼請用中文回答)
- [實作成果](#實作成果)
  - [照片](#照片)
  - [影片](#影片)

## 功能

    1. 按下按鈕即可拍攝影像
    2. 將圖像發送至 Google-Gemini 並回覆訊息
    3. 發送訊息到 Google-TTS 並播放 mp3 檔案進行說話 

## GenAI程式碼設計流程

```mermaid
graph TD
    A[開始] --> B(用戶按下按鈕);
    B --> C{拍攝圖像};
    C --> D[圖像數據];
    D --> E[發送圖像至 Google Gemini];
    E --> F{Gemini 圖像辨識};
    F -- 返回回應 --> G[接收 Gemini 回應 - 文字];
    G --> H[發送回應文字至 Google TTS];
    H --> I{TTS 生成 MP3 語音};
    I -- 返回 MP3 --> J[接收 TTS MP3 語音檔];
    J --> K[播放 MP3 語音];
    J --> L[顯示結果於 LCD - 選用];
    K --> M[結束];
    L --> M;
```


## 程式碼

### 程式重點 <**提示字:** *請問這個回收物是什麼?請用中文回答*>

```c
String Gemini_key = "";               // paste your generated Gemini API key here
char wifi_ssid[] = "";    // your network SSID (name)
char wifi_pass[] = "";        // your network password

#include <WiFi.h>
#include <WiFiUdp.h>
#include "GenAI.h"
#include "VideoStream.h"
#include "SPI.h"
#include "AmebaILI9341.h"
#include "TJpg_Decoder.h" // Include the jpeg decoder library
#include "AmebaFatFS.h"

WiFiSSLClient client;
GenAI llm;
GenAI tts;

AmebaFatFS fs;
String mp3Filename = "test_play_google_tts.mp3";

VideoSetting config(768, 768, CAM_FPS, VIDEO_JPEG, 1);
#define CHANNEL 0

uint32_t img_addr = 0;
uint32_t img_len = 0;
const int buttonPin = 1;          // the number of the pushbutton pin

//String prompt_msg = "What type and name of the recyclables in the picture?";
String prompt_msg = "請問這個回收物是什麼?請用中文回答";

#define TFT_RESET 5
#define TFT_DC    4
#define TFT_CS    SPI_SS

AmebaILI9341 tft = AmebaILI9341(TFT_CS, TFT_DC, TFT_RESET);

#define ILI9341_SPI_FREQUENCY 20000000

bool tft_output(int16_t x, int16_t y, uint16_t w, uint16_t h, uint16_t *bitmap)
{
    tft.drawBitmap(x, y, w, h, bitmap);

    // Return 1 to decode next block
    return 1;
}

void initWiFi()
{
    for (int i = 0; i < 2; i++) {
        WiFi.begin(wifi_ssid, wifi_pass);

        delay(1000);
        Serial.println("");
        Serial.print("Connecting to ");
        Serial.println(wifi_ssid);

        uint32_t StartTime = millis();
        while (WiFi.status() != WL_CONNECTED) {
            delay(500);
            if ((StartTime + 5000) < millis()) {
                break;
            }
        }

        if (WiFi.status() == WL_CONNECTED) {
            Serial.println("");
            Serial.println("STAIP address: ");
            Serial.println(WiFi.localIP());
            Serial.println("");
            break;
        }
    }
}

void init_tft()
{
    tft.begin();
    tft.setRotation(2);

    tft.clr();
    tft.setCursor(0, 0);

    tft.setForeground(ILI9341_GREEN);
    tft.setFontSize(2);
}

void setup()
{
    Serial.begin(115200);

    SPI.setDefaultFrequency(ILI9341_SPI_FREQUENCY);
    initWiFi();

    config.setRotation(0);
    Camera.configVideoChannel(CHANNEL, config);
    Camera.videoInit();
    Camera.channelBegin(CHANNEL);
    Camera.printInfo();
    
    pinMode(buttonPin, INPUT);
    pinMode(LED_B, OUTPUT);

    init_tft();
    tft.println("GenAIVision_TTS_LCD");

    TJpgDec.setJpgScale(2); // The jpeg image can be scaled by a factor of 1, 2, 4, or 8    
    TJpgDec.setCallback(tft_output);
}

void loop()
{
    tft.setCursor(0,1);
    tft.println("press button to capture image");
     if ((digitalRead(buttonPin)) == 1) {
        tft.println("Capture Image");       
        // Start MP4 recording after 3 seconds of blinking
        for (int count = 0; count < 3; count++) {
            digitalWrite(LED_B, HIGH);
            delay(500);
            digitalWrite(LED_B, LOW);
            delay(500);
        }
    // Camera take image
        Camera.getImage(0, &img_addr, &img_len); 

    // JPEG decode image & display
        TJpgDec.getJpgSize(0, 0, (uint8_t *)img_addr, img_len);
        TJpgDec.drawJpg(0, 0, (uint8_t *)img_addr, img_len);

    // LLM Vision
        String text = llm.geminivision(Gemini_key, "gemini-2.0-flash", prompt_msg, img_addr, img_len, client);
        Serial.println(text);

    // Text-To-Speech & play mp3 file
        tft.clr();
        tft.setCursor(0, 0);    
        tft.println("Text-To-Speech");
        //tts.googletts(mp3Filename, text, "en-US");
        tts.googletts(mp3Filename, text, "zh-TW");
        delay(500);
        sdPlayMP3(mp3Filename);       
    }
}

void sdPlayMP3(String filename)
{
    fs.begin();
    String filepath = String(fs.getRootPath()) + filename;
    File file = fs.open(filepath, MP3);
    file.setMp3DigitalVol(175);
    file.playMp3();
    file.close();
    fs.end();
}
```

## 實作成果

### 照片

1. 設備照
![imag](/blog/assets/photo/Edge-Ai-Class-Project/AI回收/178615_0.jpg)

![imag](/blog/assets/photo/Edge-Ai-Class-Project/AI回收/178616_0.jpg)

### 影片

2. Damo影片

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/lom80A3G_54/0.jpg)](https://www.youtube.com/watch?v=lom80A3G_54)
點擊圖片播放
