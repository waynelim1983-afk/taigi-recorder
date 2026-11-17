# 台語錄音清單 · Taigi Recorder

**👉 [開啟錄音網頁](https://waynelim1983-afk.github.io/taigi-recorder/)**

為台語語音輸入專案收集測試語料的手機網頁。參與者看 20 句國語，用平常講話的台語說出來，約 10–15 分鐘。

*A mobile web page for collecting Taiwanese Hokkien (Taigi) speech samples. Participants read 20 Mandarin prompts and say them in everyday Taigi. Recordings stay on the phone until they tap Send.*

## 為什麼做這個

我在做一個語音輸入工具：用台語說話，手機鍵盤上直接變成國語文字。對象是不太會打字的長輩，以及台灣國語很重、一般語音輸入常聽不準的人。

要知道辨識準不準，需要不同年齡、不同地區的人念同一批句子，所以做了這個錄音頁，讓親友用手機就能幫忙，不用安裝任何 App。

## 錄音會去哪裡

| 階段 | 錄音在哪裡 |
|---|---|
| 錄音中、按「送出」前 | 只存在這支手機的瀏覽器（IndexedDB），不會自動上傳 |
| 按「送出給作者」後 | 經 Google Apps Script 傳到作者個人的 Google 雲端硬碟，只有作者看得到 |
| 送不出去時 | 打包成 `.zip` 存在手機，自己決定用 LINE 或雲端硬碟傳給誰 |

- 網頁沒有統計工具，也不載入外部程式；頁面由 GitHub Pages 提供，錄音不會經過 GitHub。
- 每一句都能刪除或重錄；清除瀏覽器資料，錄音就消失。送出後想撤回，告訴作者即可刪除。
- 送出時會附上年齡層與成長縣市（都可以不填），以及自動產生的隨機編號、手機型號與瀏覽器版本，只用來分析不同口音與機型的辨識結果。

## 功能

- **按住錄音、放開就存**；按住不方便的人可以改成「按一下開始，再按一下結束」
- 每句可以播放、重錄，進度條顯示完成幾句
- 自動偵測 LINE、Facebook 等 App 內建瀏覽器，提示改用 Safari 或 Chrome（內建瀏覽器常常無法錄音）
- 沒錄完也可以先送出，之後補錄再送，重複的句子會被新的取代
- 網址加 `?c=代號` 可以指定參與者代號；沒有就由手機自動產生隨機碼
- 大字、高對比、支援深色模式，按鈕至少 48px，方便長輩操作

## 技術

- 單一 `index.html`，原生 JavaScript，沒有建置步驟、沒有框架
- `MediaRecorder` + `getUserMedia` 錄音，依瀏覽器自動選擇支援的音訊格式
- `IndexedDB` 暫存錄音，重新整理頁面也不會遺失
- [JSZip](https://stuk.github.io/jszip/) 打包成 zip
- 收件端是 Google Apps Script 網頁應用程式（程式不在這個倉庫）：檢查代號與檔名格式、單檔上限 8 MB、每天最多 800 個檔案，依代號存進不同資料夾

## 相關專案

收集到的錄音用來測試手機離線台語辨識（whisper.cpp 交叉編譯到 Android），目前在私人倉庫開發中。
