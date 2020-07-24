###### tags: `國立金門大學`、`專題`、`LoRa`
<details><summary>Outline</summary>

- [以 LoRa 為基礎之失之老人定位系統](#以-lora-為基礎之失之老人定位系統)
  - [專題成員](#專題成員)
  - [致謝](#致謝)
  - [研究動機](#研究動機)
  - [使用到的硬體](#使用到的硬體)
    - [硬體](#硬體)
    - [軟體](#軟體)
  - [功能介紹](#功能介紹)
    - [失智老人輔助裝置](#失智老人輔助裝置)
    - [管理平台網站](#管理平台網站)
  - [Demo 影片](#demo-影片)
    - [網頁 Demo 影片](#網頁-demo-影片)
    - [實際 Demo 情境影片](#實際-demo-情境影片)
  - [專題紀錄](#專題紀錄)
</details>

# 以 LoRa 為基礎之失之老人定位系統
## 專題成員
- 指導教授：[趙于翔 教授](http://yxzhao-0429.appspot.com/)
- 學生：[蘇家禹](https://github.com/ChiaYuSu)、[馮志揚](https://github.com/zxc22273146)、[陳憲億](https://github.com/chullin)、[王岳駿](https://github.com/sjkry505)、陳佳駿
> 另外，感謝地下組員[林柏億](https://github.com/istar0me)及學姊吳家瑄的指導與協助

## 致謝
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本專題之所以可以順利完成，首先要感謝負責指導我們的專題教授趙于翔老師，因為有他細心的指導我們，並提供我們寶貴的意見，製作專題近一年半的時間，我們獲得許多的知識，在我們遭遇挫折時，給予我們鼓勵、加油、打氣，才得以讓本研究順利完成。 
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;另外要感謝的是本組所有參與專題研究的組員：蘇家禹、馮志揚、陳憲億、王岳駿、陳佳駿同學，利用空堂的時間及課後時間參與和討論，同學彼此切磋討論、相互勉勵扶持，並且不斷的重複檢討，致使本研究可以順利完成。 
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;再一次的感謝所有參與本研究教授、同學以及國立金門大學的學生們，都是因為有你們熱心的幫忙與協助，在此獻上最誠摯的感謝，謝謝大家！大家辛苦了！ 

## 研究動機
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;隨著少子化問題的日趨嚴重，老年人口比例明顯提升，社會照顧問題逐漸受人重視，然而隨著老年人口越來越多的情況下，失智症人口也隨之增長。失智症最大的特點就是對於自己說過的話、做過的事，完全忘記。因此我們設計出一套以 LoRa 為基礎的輔助裝置，其主要目的是希望能夠解決失智老人在外面走失的問題，此裝置透過 GPS 定位技術，將失智老人的 GPS 座標傳回雲端資料庫，並透過雲端監控管理平台來呈現與管理這些資訊，我們希望此裝置的提出，可以即時的偵測到老人家是否忘記回家的路，並透過 GPS座標位置快速找出其位置，並減少其意外的發生。 
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本論文中，我們嘗試利用 LoRa 傳輸技術結合 GPS 定位技術，設計出一套以 LoRa 為基礎之失智老人輔助裝置設計，其主要目的是希望能夠解決失智老人在外面走失的問題，其中裝置包含了即時定位系統，不僅可以透過定位了解老人家是否忘記回家的路，且當有異狀發生時，也可以透過座標位置快速找出其位置，並減少意外發生。

## 使用到的硬體
### 硬體
| 硬體名稱           | 功能                         | 備註                          |
| ------------------ | ---------------------------- | ----------------------------- |
| Seeeduino Lotus    | 中央處理模組                 | 可完美兼容 Arduino Uno 開發板 |
| Grove LoRa Radio   | LoRa 無線傳輸模組            | 採用低頻 433MHz，繞射較強     |
| 35dBi 低頻增益天線 | 增加訊號強度，降低封包掉包率 |                               |
| V.KEL GPS 定位模組 | 精準定位                     | 水平誤差值 < 2.5 公尺         |

### 軟體
| 軟體名稱           |
| ------------------ |
| Arduino            |
| Visual Studio 2019 |
| Azure              |

## 功能介紹
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;本系統主要包含了兩大部分，分別為失智老人輔助裝置與管理平台網站，失智老人輔助裝置主要是負責失智老人的即時定位，並透過 LoRa 傳輸方式將數據上傳至雲端監控管理平台，管理者可以在平台上設定失智老人的安全區域範圍，當失智老人超出安全區域時會提出相對應之警示。

### 失智老人輔助裝置
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;失智老人輔助裝置包含了中央處理模組、無線傳輸模組、低頻增益天線、GPS 定位模組以及協尋提示模組。Client 端的中央處理模組負責接收 GPS 模組並利用 LoRa 傳輸模組傳給 Server 端的 LoRa 傳輸模組，收到數據後寫入資料庫中。若判定失智老人走出警戒範圍時，則會透過 Server 端的喇叭撥出一段警示音樂。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;失智老人輔助裝置分為使用者端與伺服器端兩種，使用者端負責將失智老人的 GPS 座標傳回伺服器端，伺服器端則負責接收使用者端的所有裝置資訊，並透過網際網路上傳至雲端資料庫中。


![系統架構](https://i.imgur.com/Z633HCu.png)
<center>▲ 失智老人管理系統架構</center>

<br>
<br>

### 管理平台網站
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;透過我們自行架設的網站，萬一失智老人不小心走失，社工單位或是老人家的家屬可以第一時間透過我們的平台找到失智老人的即時位置。此外，平日也可以透過平台看到老人家過去的活動紀錄，了解老人家活動範圍。

![網站首頁](https://i.imgur.com/ASZQReX.jpg)
<center>▲ 失智老人管理平台網站</center>

<br>
<br>

![即時位置](https://i.imgur.com/TEpefnw.png)
<center>▲ 失智老人所在即時位置介面</center>

<br>
<br>

![歷史紀錄](https://i.imgur.com/AQADZHo.png)
<center>▲ 失智老人歷史位置紀錄介面</center>



## Demo 影片
### 網頁 Demo 影片
[![](http://img.youtube.com/vi/SRcZ4PaRkbo/0.jpg)](http://www.youtube.com/watch?v=SRcZ4PaRkbo "")
> 影片點選觀看


### 實際 Demo 情境影片
[![](http://img.youtube.com/vi/7yTOFd2Cqb4/0.jpg)](http://www.youtube.com/watch?v=7yTOFd2Cqb4 "")
> 影片點選觀看<br />
> 茲感謝**國立金門大學社工系、護理系**協助拍攝影片

## 專題紀錄
1. [2019 年全國計算機會議（NCS）論文投稿](http://ncs2019.nqu.edu.tw/cn/thesis/NCS2019_thesis/06-8102.pdf)
    * 時間：2019 年 11 月 15 日
    * 地點：國立金門大學（金門，台灣）
    * 會議名稱：NCS 2019 全國計算機會議 National Computer Symposium
2. [2019 年國立金門大學資工系 專題競賽](https://photos.google.com/share/AF1QipOf_f4fohw1-yN3LycTgtUDklMYZbLJ2Y-ymXV6mWKXWGjjQUxjlTqMYv78mgfAaQ?key=djBTQmMxc3phWmZNWUFaaWVFTVhVS2lHd1Q2djl3)&nbsp;&nbsp;**第一名**
    * 時間：2019 年 12 月 20 日
    * 地點：國立金門大學資工系中庭（金門，台灣）
3. [2020 年第十五屆戰國策全國創新創意競賽 企業指定組（金門產業組）](https://drive.google.com/file/d/1qbtq8qYhT8_gBZ59ZmCipdl4YDCIqazJ/view?usp=sharing)**入圍決賽**
    * 時間：2020 年 5 月 18 日
    * 地點：台北市電腦公會（台北，台灣）
    * 團隊名稱：安心上路 ‧ 有跡可循
    * 作品名稱：以 LoRa 為基礎之失智老人定位系統
4. [2020 年第十五屆戰國策全國創新創意競賽 企業指定組（金門產業組）](https://drive.google.com/file/d/1WaQ63BNMEJ7IsK5W_pLM4ODUG7TQuXq7/view?usp=sharing)台北場&nbsp;&nbsp;**優選銀獎(亞軍)**
    * 時間：2020 年 7 月 17 日
    * 地點：國立臺北科技大學億光大樓（台北，台灣）
    * 團隊名稱：安心上路 ‧ 有跡可循
    * 作品名稱：以 LoRa 為基礎之失智老人定位系統
    * 相關報導：[金門縣政府](https://www.kinmen.gov.tw/News_Content2.aspx?n=98E3CA7358C89100&sms=BF7D6D478B935644&s=4A7DCDF04DD995D1)、[金門三創服務平台 fb](https://www.facebook.com/kinmenstartuphub/posts/765131000925207)、[金門日報](https://www.kmdn.gov.tw/1117/1271/1272/321385)、[台灣好報](https://tw.news.yahoo.com/三創創新創業競賽-培植金門產業未來能量-000000676.html)
5. [2020 年第十五屆戰國策全國創新創意競賽 企業指定組（金門產業組）]()金門場
    * 時間：2020 年 7 月 24 日
    * 地點：昇恆昌金湖大飯店（金門，台灣）
    * 團隊名稱：安心上路 ‧ 有跡可循
    * 作品名稱：以 LoRa 為基礎之失智老人定位系統
    * 備註：學弟妹（[林家齊](https://github.com/linjiachi)、[傅于軒](https://github.com/FUYUHSUAN)、[林妍汝](https://github.com/AIONLin)）代為參賽
