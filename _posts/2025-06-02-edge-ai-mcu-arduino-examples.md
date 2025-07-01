---
layout: post # 指定文章佈局，通常是 post
title: AMB82-mini 範例程式介紹
date: 2025-06-02 08:00:00 +0800 # 發表日期和時間 (請根據您當前的時區調整 +0800 代表 UTC+8)
categories: [邊緣運算] # 文章分類，您可以自訂
tags: [AMB82-mini] # 文章標籤，您可以自訂
description: AMB82-mini 範例程式介紹
mathjax: false # 如果這篇文章不需要顯示數學公式，請設false
comments: false # 如果這篇文章需要啟用評論，請設為 true
---
## Arduino 範例程式
### [微控制器界面簡介](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/MCU_interfaces.md)

### GPIO
**Examples> 01.Basics > Blink**<br>
  
![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/AMB82-mini_Arduino_examples_01.Basics_Blink.png?raw=true)
    
**Examples> 02.Digitial > GPIO > Button**<br>
  
![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/AMB82-mini_Arduino_examples_02.Digital_Button.png?raw=true)

程式碼修改：<br>
const int buttonPin = `1`;  // the number of the pushbutton pin<br>
const int ledPin = `LED_BUILTIN`;    // the number of the LED pin<br>

**Examples> 01.Basic > AnalogReadSerial**<br>

![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/AMB82-mini_Arduino_examples_01.Basics_AnalogReadSerial.png?raw=true)

程式碼修改：Serial.begin(`115200`);<br>


---
### WiFi
**Examples> WiFi > SimpleTCPServer**<br>
[WiFi - Simple TCP Server](https://www.amebaiot.com/en/amebapro2-arduino-server-client/)<br>

**Examples> WiFi > SimpleHttpWeb > ReceiveData**<br>
[WiFi - Simple Http Server to Receive Data](https://www.amebaiot.com/en/amebapro2-arduino-web-server-status/)<br>

**Examples> WiFi > SimpleHttpWeb > ControlLED**<br>
[WiFi - Simple Http Server to Control LED](https://www.amebaiot.com/en/amebapro2-arduino-ameba-web-server/)<br>

**Sketchbook> AMB82-mini > WebServer_ControlLED**<br>
[Sketchbook> WebServer_ControlLED](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/Arduino/AMB82-mini/WebServer_ControlLED/WebServer_ControlLED.ino)<br>
![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/AMB82-mini_Arduino_Sketch_WebServer_ControlLED.png?raw=true)

---
### BLE

**Exmples> AmebaBLE > BLEV7RC_CAR_VIDEO** <br>

[BLE V7RC](https://www.amebaiot.com/zh/amebad-arduino-ble-v7rc/)<br>

* [V7RC APP 介紹](https://hackmd.io/@accomdemy/v7rc)<br>
* 安裝[手機App V7RC](https://play.google.com/store/apps/details?id=com.v7idea.v7rcliteandroidsdkversion&hl=en)<br>
<p>
<img width="50%" height="50%" src="https://www.amebaiot.com/wp-content/uploads/2023/08/ble-v7rc/p1_zh.png">
<img width="50%" height="50%" src="https://www.amebaiot.com/wp-content/uploads/2023/08/ble-v7rc/p2_zh.png">
</p>

---
### [MQTT](https://mqtt.org/)
MQTT is an OASIS standard messaging protocol for the Internet of Things (IoT)<br>
[How MQTT Works -Beginners Guide](http://www.steves-internet-guide.com/mqtt-works/)<br>

**Examples> AmebaMQTTClient > MQTT_basic** <br>
[MQTT - Set up MQTT Client to Communicate with Broker](https://www.amebaiot.com/en/amebapro2-arduino-mqtt-upload-listen/)<br>
![](https://www.amebaiot.com/wp-content/uploads/2023/06/network/mqtt1-1.png)

`pip install paho.mqtt`<br>

**publish messages to AMB82-mini** <br>
```
import paho.mqtt.publish as publish
host = "test.mosquitto.org"
publish.single("ntou/edgeai/robot1", "go to the kitchen", hostname=host)
```

**subsribe messages from AMB82-mini** <br>
```
import paho.mqtt.subscribe as subscribe
host = "test.mosquitto.org"
msg = subscribe.simple("ntou/edgeai/robot1", hostname=host)
print("%s %s" % (msg.topic, msg.payload.decode("utf-8")))
```

---
### [MQTT IOT App](https://kittenbothk.readthedocs.io/en/latest/Wifibrick/AI2/ai2.html)

Download extension : [UrsAI2PahoMqtt](https://ullisroboterseite.de/android-AI2-MQTT-en.html)<br>

**[GeminiMQTT App](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/MQTT/GeminiMQTT.aia)**<br>
Download to PC, and import to ai2.appinventor2.mit.edu<br>
edit [Block] `global API_key` (get API key from https://aistudio.google.com/apikey)<br>

---
## 感測器與週邊裝置

### 紅外線測距模組
**[VL53L0X v2](https://www.ruten.com.tw/item/show?22425810394279)** , **[VL53L1X v2](https://www.ruten.com.tw/item/show?22425810394279)** <br>
<p><img width="50%" height="50%" src="https://esphome.io/_images/vl53l0x.png"></p>

**Datasheet**: [VL53L0X - Time-of-Flight ranging sensor](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/vl53l0x.pdf)<br>\
**Sketchbook> AMB82-mini > [IR_VL53L0X](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/IR_VL53L0X)** <br>

---
### 慣性感測
[慣性感測元件](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/IMU.md)<br>

**[MPU6050](https://www.ruten.com.tw/item/show?22428017261803)** <br>
![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/MPU6050.png?raw=true)

**Sketchbook > AMB82-mini > [MPU6050-DMP6v12](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/MPU6050_DMP6v12)** <br>

---
### PWM
[PWM - Servo Control](https://www.amebaiot.com/en/amebapro2-arduino-pwm-servo/) <br>

**Examples> AmebaAnalog > PWM_ServoControl** <br>
```
myservo.attach(8);
```

```
myservo.write(pos);
```
![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/Gripper.jpg?raw=true)

---
### H-bridge 全橋式馬達驅動
**TB6612** <br>
![](https://i0.wp.com/dronebotworkshop.com/wp-content/uploads/2019/12/TB6612FNG-pinout.jpeg?w=768&ssl=1)

**DRV8833** <br>
![](https://www.jsumo.com/drv8833-stepper-motor-driver-board-2-channel-4094-14-B.jpg)
![](https://jin-hua.com.tw/upload/images/2430000015663-902.jpg)

---
### ILI9341 TFT-LCD
![](https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/AMB82-mini_button_SPI_TFTLCD.jpg?raw=true)

**[SPI - LCD Screen ILI9341 TFT](https://www.amebaiot.com/en/amebapro2-arduino-spi-lcd/)** <br>

#### Interface signal names:
* MOSI: Standard SPI Pin
* MISO: Standard SPI Pin
* SLK: Standard SPI Pin
* CS: Standard SPI Pin
* RESET: Used to reboot LCD.
* D/C: Data/Command. When it is at LOW, the signal transmitted are commands, otherwise the data transmitted are data.
* LED (or BL): Adapt the screen backlight. Can be controlled by PWM or connected to VCC for 100% backlight.
* VCC: Connected to 3V or 5V, depends on its spec.
* GND: Connected to GND.

---
#### AMB82 MINI and QVGA TFT LCD Wiring Diagram:<br>
![](https://www.amebaiot.com/wp-content/uploads/2023/01/spi/lcdP01.png)

**Sketchbook> AMB82-mini > [HTTP_Post_ImageText_TFTLCD](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/HTTP_Post_ImageText_TFTLCD)** <br>

**Exmples> AmebaSPI > Camera_2_lcd** <br>
*Camera output , then Jpeg Decoder to TFT-LCD<br>*<br>
compilation error: need to modify `Libraries/TJpg_Decoder/src/User_Config.h`<br>
//#define TJPGD_LOAD_SD_LIBRARY<br>

**Exmples > AmebaSPI > Camera_2_Lcd_JPEGDEC** <br>
*Camera output, saved to SDcard, then Jpeg Decoder to read to TFT-LCD*<br>

**Exmples > AmebaSPI > LCD_Screen_ILI9341_TFT** <br>
*LCD Draw Tests*<br>

---
### 影像串流
**Examples> AmebaMultimedia > StreamRTSP > RTSP_VideoOnly** <br>
**Sketchbook> [RTSP_VideoOnly](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/RTSP_VideoOnly)** <br>
[![](https://markdown-videos-api.jorgenkh.no/youtube/OmAnWOmt6WQ)](https://youtu.be/OmAnWOmt6WQ)

* [Amebapro2 AMB82-mini Arduino Example Guides](https://www.amebaiot.com/en/amebapro2-amb82-mini-arduino-peripherals-examples)

---
### [動作偵測 (motion detection)](https://www.amebaiot.com/en/amebapro2-arduino-video-motion/)
**Examples> AmebaMultimedia > MotionDetection > LoopPostProcessing** <br>
* 修改ssid, passwd, 後燒錄到AMB82-mini,
* 按reset後程式即開始運行, 用serial-monitor 查看顯示串流網址
* 啟動手機或電腦上之VLC player, 設定RTSP串流網址
<p><img width="50%" height="50%" src="https://www.amebaiot.com/wp-content/uploads/2023/01/video/motionP06.png"></p>

---
### [Motion Detection Google Line Notify](https://www.amebaiot.com/en/amebapro2-arduino-motion-notify/)
**Examples> AmebaMultimedia > MotionDetection > MotionDetectGoogleLineNotify** <br>

[![](https://markdown-videos-api.jorgenkh.no/youtube/g_ZP023XCIw)](https://youtu.be/g_ZP023XCIw)

---
### 音頻環回測試
**Examples> AmebaMultimedia > Audio >LoopbackTest**<br>

![](https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/AMB82-mini_button_audiojack.jpeg?raw=true)

---
### MP3 播放
AMB82-mini + PAM8403 + 4ohm 3W speaker<br>
![](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/assets/AMB82-mini_PAM8403.jpg?raw=true)

**Sketchbook> AMB82-mini > [SDcardPlayMP3](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/Arduino/AMB82-mini/SDcardPlayMP3/SDcardPlayMP3.ino)** <br>
* .mp3 files stored under mp3 directory

**Sketchbook> AMB82-mini > [SDcardPlayMP3_All](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/Arduino/AMB82-mini/SDcardPlayMP3_All/SDcardPlayMP3_All.ino)** <br>
     
---
### 音頻串流範例
**Examples> AmebaMultimedia > Audio > RTSPAudioStream** <br>

[RTSP Audio Stream](https://www.amebaiot.com/en/amebapro2-arduino-audio-rtsp/)<br>

---
### MP4錄音範例
**Examples> AmebaMultimedia > RecordMP4 > AudioOnly** <br>

[Multimedia - MP4 Recording](https://www.amebaiot.com/en/amebapro2-arduino-video-mp4/)<br>

---
### 音頻分類範例
**Examples> AmebaNN > [AudioClassification](https://www.amebaiot.com/en/amebapro2-arduino-neuralnework-audio-classification/)** <br>

[YAMNet](https://codimd.mcl.math.ncu.edu.tw/s/hoOqEgBSf)<br>
[![](https://markdown-videos-api.jorgenkh.no/youtube/oi8ML6aJcvI)](https://youtu.be/oi8ML6aJcvI)

---
### [人臉辨識與識別介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/07/Face-Recognition.html)

---
### [人臉檢測範例](https://www.amebaiot.com/en/amebapro2-arduino-neuralnework-face-detection/)
**Examples> AmebaNN > RTSPFaceDetection** <br>

[![](https://markdown-videos-api.jorgenkh.no/youtube/KD95JH6gVew)](https://youtu.be/KD95JH6gVew)

<p><img width="50%" height="50%" src="https://www.amebaiot.com/wp-content/uploads/2023/01/neuralnetwork/facedetectP06.png"></p>

---
### [人臉識別範例](https://www.amebaiot.com/en/amebapro2-arduino-neuralnework-face-recognition/)
**Examples> AmebaNN > RTSPFaceRecognition** <br>

[![](https://markdown-videos-api.jorgenkh.no/youtube/GGOIQmMfeF8)](https://youtu.be/GGOIQmMfeF8)

Serial_monitor: `REG=RKUO`<br>
<p><img width="50%" height="50%" src="https://github.com/rkuo2000/EdgeAI-AMB82-mini/blob/main/assets/FaceRecognition_REG_RKUO.jpeg?raw=true"></p>

* Enter the command **REG=Name** to give the targeted face a name.
* Enter the command **DEL=Name** to delete a certain registered face. For example, `DEL=SAM`
* Enter the command **BACKUP** to save a copy of registered faces to flash.
* If a backup exists, enter the command **RESTORE** to load registered faces from flash.
* Enter the command **RESET** to forget all previously registered faces. 

---
### 影像分類 (Image Classification)
* **[Kaggle平台使用介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/02/Kaggle-Intro.html)**

* **[卷積層神經網路介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/03/CNN.html)**

* **[影像分類介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/04/Image-Classification.html)**

---
### 回收物分類
[RTSP_GarbageClassification.ino](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/RTSP_GarbageClassification)<br>
[![](https://markdown-videos-api.jorgenkh.no/youtube/c3XGkc9ShwQ)](https://youtu.be/c3XGkc9ShwQ)

---
### Garbage模型訓練與檔案轉換

#### 模型訓練： [kaggle.com/rkuo2000/garbage-cnn](https://www.kaggle.com/code/rkuo2000/garbage-cnn)
required in kaggle for AmebaPro2
1) pip install tensorflow==2.14.1
2) model.save('garbage_cnn.h5', include_optimizer=False)

#### 模型轉換：[AMB82 AI Model Conversion](https://www.amebaiot.com/en/amebapro2-ai-convert-model/)
1. Download garbage_cnn.h5 from [kaggle.com/rkuo2000/garbage-cnn](https://www.kaggle.com/code/rkuo2000/garbage-cnn) `Output`
2. Compress garbage_cnn.h5 to garbage_cnn.zip
3. Go to [Amebapro2 AI convert model](https://www.amebaiot.com/en/amebapro2-ai-convert-model/), fill up your E-mail
4. Upload garbage_cnn.zip
5. Upload one (.jpg) test picture (EX. glass100.jpg from [Garbage dataset](https://www.kaggle.com/datasets/asdasdasasdas/garbage-classification))
6. Email will be sent to you for the link of `network_binary.nb`

#### 程式範例：RTSP_GarbageClassification.ino
1. click the recieved Email link to download `network_binary.nb`
2. create NN_MDL folder in SDcard, save network_binary.nb under NN_MDL folder, and rename it to `imgclassification.nb`
3. plugin SDcard back to AMB82-MINI
4. modify Sketch RTSP_GarbageClassification.ino 
   1) modify SSID and PASSWD
   2) modify imgclass.modelSelect (change DEFAULT_IMGCLASS to CUSTOMIZED_IMGCLASS)
5. burn code into board AMB82-MINI, and run it with VLC player streaming
<p><img width="75%" height="75%" src="https://github.com/rkuo2000/EdgeAI-AmebaPro2/raw/main/assets/RTSP_GarbageClassification.png"><img width="25%" height="25%" src="https://github.com/rkuo2000/EdgeAI-AmebaPro2/raw/main/assets/RTSP_GarbageClassification_VLCplayer.jpeg"></p>

---
## 物件偵測 (Object Detection)

### Public Dataset
**[Roboflow](https://universe.roboflow.com/)** <br>

---
### [物件檢測介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/05/Object-Detection.html)
**Kaggle範例:** <br>
* [YOLOv7 Facemask detection](https://www.kaggle.com/code/rkuo2000/yolov7-facemask-detection)
* [YOLOv7 Pothole detection](https://www.kaggle.com/code/rkuo2000/yolov7-pothole)
* [YOLOv7 Sushi detection](https://www.kaggle.com/code/rkuo2000/yolov7-sushi-detection)
* [YOLOv7 refrigeratoryfood](https://www.kaggle.com/code/rkuo2000/yolov7-refrigeratoryfood)<br>
* [YOLOv7 reparm](https://www.kaggle.com/code/rkuo2000/yolov7-reparam)<br>

---
### Pothole模型訓練與檔案轉換

#### 模型訓練： [kaggle.com/rkuo2000/yolov7-pothole](https://www.kaggle.com/code/rkuo2000/yolov7-pothole)
1) repro [https://github.com/WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7)
2) create pothole.yaml
`%%writefile data/pothole.yaml`<br>
```
train: ./Datasets/pothole/train/images
val:  ./Datasets/pothole/valid/images
test: ./Datasets/pothole/test/images

# Classes
nc: 1  # number of classes
names: ['pothole']  # class names
```

3) YOLOv7-Tiny Fixed Resolution Training
```
!sed -i "s/nc: 80/nc: 1/" cfg/training/yolov7-tiny.yaml
!sed -i "s/IDetect/Detect/" cfg/training/yolov7-tiny.yaml
```

#### 模型轉換：[AMB82 AI Model Conversion](https://www.amebaiot.com/en/amebapro2-ai-convert-model/)
1. Download `best.pt` from [kaggle.com/rkuo2000/yolov7-pothole](https://www.kaggle.com/code/rkuo2000/yolov7-pothole)
2. Compress best.pt to `best.zip`
3. Go to [Amebapro2 AI convert model](https://www.amebaiot.com/en/amebapro2-ai-convert-model/), fill up your E-mail
4. Upload best.zip
5. Upload one (.jpg) test picture (EX. pothole_test.jpg from [Pothole dataset](https://www.kaggle.com/datasets/apoorvchaudhary/pothole))
6. Email will be sent to you for the link of `network_binary.nb`

#### 程式範例：RTSP_YOLOv7_Pothole_Detection.ino
1. click the recieved Email link to download `network_binary.nb`
2. create NN_MDL folder in SDcard, save network_binary.nb under NN_MDL folder, and rename it to `yolov7_tiny.nb`
3. plugin SDcard back to AMB82-MINI
4. modify Sketch RTSP_YOLOv7_Pothole_Detection.ino 
   1) modify SSID and PASSWD
   2) modify ObjDet.modelSelect(OBJECT_DETECTION, CUSTOMIZED_YOLOV7TINY, NA_MODEL, NA_MODEL);
5. burn code into board AMB82-MINI, and run it with VLC player streaming
<p><img width="50%" height="50%" src="https://github.com/rkuo2000/EdgeAI-AmebaPro2/raw/main/assets/RTSP_YOLOv7_Pothole.png"><img width="50%" height="50%" src="https://github.com/rkuo2000/EdgeAI-AmebaPro2/raw/main/assets/RTSP_YOLOv7_Pothole_VCplayer.jpeg"></p>

   
---
### AMB82 Mini 物件偵測範例
[![](https://markdown-videos-api.jorgenkh.no/youtube/EvryVoQyqqk)](https://youtu.be/EvryVoQyqqk)

[RTSP_YOLOv7_Pothole](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/RTSP_YOLOv7_Pothole)<br>
[RTSP_YOLOv7_Sushi](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/RTSP_YOLOv7_Sushi)<br>

---
### AMB82 Mini SD卡加載模型範例
[RTPS_ObjectDetection_AudioClassification.ino](https://github.com/rkuo2000/Arduino/tree/master/examples/AMB82-MINI/RTSP_ObjectDetection_AudioClassification/)<br>
[![](https://markdown-videos-api.jorgenkh.no/youtube/cVvdnXiCAa4)](https://youtu.be/cVvdnXiCAa4)

---
### Online NN Conversion Tool (客製化模型轉換工具)
[![](https://markdown-videos-api.jorgenkh.no/youtube/6cHC2cOKgQk)](https://youtu.be/6cHC2cOKgQk)

---
## 大型語言模型範例 (LLM)

* **[大型語言模型介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/15/LLM.html)**

---
### 語音辨識範例
#### ffmpeg.exe is needed for Windows to run Whisper!
* [AmebaPro2 Whisper server](https://github.com/rkuo2000/Arduino/tree/master/examples/AMB82-MINI/src/AmebaPro2_Whisper_server.py)
  
* [HTTP_Post_Audio.ino](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/HTTP_Post_Audio)

---
### 語音交談範例
#### ffmpeg.exe is needed for Windows to run Whisper!
Download [ffmpeg-master-latest-win64-gpl.zip](https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-win64-gpl.zip), extract & put ffmpeg.exe into  where you run Whisper server.<br>

#### [AmebaPro2 Whisper LLM_server](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/AmebaPro2_server/AmebaPro2_Whisper_LLM_server.py)

#### [AmebaPro2_Whisper_Gemini_server](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/AmebaPro2_server/AmebaPro2_Whisper_Gemini_server.py) 
* 到 https://aistudio.google.com/app/apikey 取得API_Key 填入GOOGLE_API_KEY, 再執行AmebaPro2_Whisper_Gemini_server.py

#### [HTTP_Post_Audio.ino](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/HTTP_Post_Audio)
* 修改server IP位址 in RecordMP4_HTTP_Post_Audio.ino server IP位址, then 燒錄到 AMB82-MINI
* reset AMB82-MINI 來啟動, 按鍵兩秒後即可錄音詢問 LLM/Gemini
  
---
## 視覺語言模型 (VLM)

**[視覺語言模型介紹](https://rkuo2000.github.io/AI-course/lecture/2024/08/16/VLM.html)** 

### 影像+語音交談範例
* [AmebaPro2_whisper_llava_server.py](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/AmebaPro2_server/AmebaPro2_Whisper_Llava_server.py)
  
* [HTTP_Post_ImageAudio](https://github.com/rkuo2000/EdgeAI-AMB82mini/tree/main/Arduino/AMB82-mini/HTTP_Post_ImageAudio)

---
## 生成式AI API

**Examples:** AmebaNN > MultimediaAI > GenAIVision<br>
**Examples:** AmebaNN > MultimediaAI > GenAISpeech_Gemini<br>
**Examples:** AmebaNN > MultimediaAI > TextToSpeech<br>

* [GenAIVision_TTS_Text_ReadWordCard](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/Arduino/AMB82-mini/GenAIVision_TTS_Text_ReadWordCard/GenAIVision_TTS_Text_ReadWordCard.ino)

* [GenAISpeech.ino](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/Arduino/AMB82-mini/GenAISpeech/GenAISpeech.ino)

* [TextToSpeech.ino](https://github.com/rkuo2000/EdgeAI-AMB82mini/blob/main/Arduino/AMB82-mini/TextToSpeech/TextToSpeech.ino)
  
---
## 專題實作

### Vaccum Robot
(trash classification, IR collision detection)<br>
[![](https://markdown-videos-api.jorgenkh.no/youtube/YHR3ZOmtcyU)](https://youtu.be/YHR3ZOmtcyU)

### RoboCar 
(voice-control, BLE remote-control, line-notify, object-detection)<br>
[![](https://markdown-videos-api.jorgenkh.no/youtube/vr_V1QnVMts)](https://youtu.be/vr_V1QnVMts)

### AI Door-Bell
[![](https://markdown-videos-api.jorgenkh.no/youtube/IumI-uAtkRU)](https://youtu.be/IumI-uAtkRU)

### Portable Chatbot with a local LLM/VLM models
[![](https://markdown-videos-api.jorgenkh.no/youtube/3PnHSE_8rRM)](https://youtu.be/3PnHSE_8rRM)

### Portable ChatGPT with a local LLM
[![](https://markdown-videos-api.jorgenkh.no/youtube/7rfmXPqyLF0)](https://youtu.be/7rfmXPqyLF0)

### [邊緣計算微控制器應用專題實作期末報告](https://itzorange.my.canva.site/edgiai01151022projectpresent/#%E7%B0%A1%E4%BB%8B) (Canva)

