<a name="readme-top"></a>

<h1 align="center">🎵 DrawSound ｜電・紙樂器 🎵</h1>
<p align="center">用導電墨水將畫作變成電子樂器（聲音藝術互動裝置）</p>
<p align="center">👨‍🏫 Instructor: Andio Lai</p>


<details>
  <summary>📖 Table of Contents</summary>
  <ol>
    <li> 
      <a href="#about-the-project"> About The Project</a>
    </li>
    <li>
      <a href="#getting-started"> Getting Started</a>
      <ul>
        <li><a href="#installation">Installation</a></li>
        <li><a href="#knowing-the-tool-kit">Knowing the Tool Kit</a></li>
      </ul>
    </li>
    <li><a href="#lesson-1">Lesson 1</a></li>
    <li><a href="#lesson-2">Lesson 2</a></li>
    <li><a href="#lesson-3">Lesson 3</a></li>
    <li><a href="#review">Review</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>


## About The Project

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

### Installation
### Knowing the Tool Kit
<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Lesson 1
在本課程中，你將學習到關於合成器（Synthesizer或Synth）的基礎知識，並使用Audacity設計自己的聲音。

網絡App Web App - 合成器音樂 Synth Music -Ableton Learn Synth: https://learningsynths.ableton.com/en/playground

Audacity : https://www.audacityteam.org/download/


<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Lesson 2

電路連接手冊 Connection Manual：[connection manual.pdf](https://github.com/nixhehehe/testing1/files/10908029/connection.manual.pdf)
<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Lesson 3
基本軟件 Basic software : 
Arduino IDE (1.8.19) : https://www.arduino.cc/en/software

組裝指南 Assembly Guide：
[revised.guide.lesson3.pdf](https://github.com/nixhehehe/testing1/files/10908037/revised.guide.lesson3.pdf)


如何加入編碼庫 How to add library: SerialMP3：
[library.pdf](https://github.com/nixhehehe/testing1/files/10908040/library.pdf)

```sh
#include "SerialMP3Player.h"// 使用MP3版的編碼庫library

#include <CapacitiveSensor.h>// 使用可感應導電墨水的CAP SENSE編碼庫library

#define TX 11 //to MP3 board RX //定義ARDUINO TX到MP3 RX引腳連接
#define RX 10 //to MP3 board TX //定義ARDUINO RX到MP3 TX引腳連接

SerialMP3Player mp3(RX, TX);// 定義起動MP3相關的TX， RX

CapacitiveSensor sensor1 = CapacitiveSensor(4, 2); 
//定義CAP SENSE導電感應引腳連接，兩者使用ARDUINO的DIGITAL引腳，並配合電阻達到感應運作 
//前者為SEND PIN,後者為RECIEVE PIN要連接到紙上


//設定：有電源起動時執行一次的程序
void setup() {
  Serial.begin(9600);     // 起動serial介面
  mp3.begin(9600);        // 開始MP3版的連接
  delay(500);             // 等待起動
  mp3.sendCommand(CMD_SEL_DEV, 0, 2);   //選取 sd-card
  delay(500);             // 等待起動
  mp3.setVol(15);// 設定音量
}

//迴圈: 處理器不停執行的程序

void loop() {

  long measurement =  sensor1.capacitiveSensor(10);//讀取SENSOR的數值

  Serial.print(measurement);//SERIAL PRINT SENSOR的數值以方便MAPPING
  Serial.println("\t");

if (measurement >= 400){//決定觸發起動歌曲的條件(值)
    mp3.play(1);     //歌曲於SD CARD內的次序
  }
  
  delay(50);//迴圈再執行的中間位
}
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Review

## Acknowledgments
