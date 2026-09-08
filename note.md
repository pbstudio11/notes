我們可以把 app.py 擴充成一個「互動式個人名片與任務清單 App」，加入更多常見的介面元素：

圖片 (Image)：顯示頭像或圖片

切換開關 (Switch)：切換深色/淺色主題模式

下拉選單 (Dropdown)：選擇類別

動態動態清單 (Column/Container)：可以新增與刪除項目

請直接複製以下程式碼，覆蓋你的 app.py 試試看：

SEE PIC 1.md

這段程式碼帶你學會的新技巧：
ft.Row 與 ft.Column（水平與垂直排版）

Row 讓元件橫向並排（例如：圖示 + 標題 + 開關）。

Column 讓元件直向排列（例如：清單項目一個接一個往下排）。

ft.Container（區塊容器）

類似網頁的 <div> 或 App 的卡片，可以設定圓角（border_radius）、背景顏色（bgcolor）與內邊距（padding）。

動態更新 UI（tasks_column.controls.append()）

可以在程式執行過程中，隨時把新的元件放入畫面上，並呼叫 page.update() 讓使用者看到更新結果。

儲存後重新執行 python3 app.py，試試看新增幾條待辦事項和切換主題！
