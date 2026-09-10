在網頁上加入書籤或分頁標籤上的那個小圖示（專業術語叫 Favicon），其實非常簡單！只需要兩個步驟：準備圖片，然後在 HTML 檔案的 <head> 區塊內加一行程式碼。

步驟 1：準備圖示檔案
圖片格式：現在多數現代瀏覽器都支援 .png、.ico 或 .svg 格式。

尺寸建議：建議製作 1:1 正方形 的圖片（例如 32x32px 或 512x512px 的 PNG 檔）。

步驟 2：在 HTML 的 <head> 裡面加入這一行
只要把你的圖示檔案（例如取名叫 favicon.png）和網頁放在同一個資料夾，然後在 HTML 的 <head> 和 </head> 之間貼上這段程式碼：



<link rel="icon" type="image/png" href="favicon.png">



完整範例：


<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的網頁</title>

    <!-- 這就是加入分頁 icon 的語法 -->
    <link rel="icon" type="image/png" href="favicon.png">

</head>
<body>
    <h1>Hello World</h1>
</body>
</html>



💡 實用小撇步（免圖片檔的偷懶方法）：
如果你手邊沒有現成的圖片檔，但又想快速用一個可愛的小圖示或 Emoji 代替，你可以直接用 SVG 格式 把程式碼寫進 href 裡面，完全不需要上傳圖片檔案！

例如，想用一個書本 📖 的 Emoji 當作分頁圖示，可以這樣寫：


<link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>📖</text></svg>">


只要把這行貼進 <head>，你的網頁分頁馬上就會變成一本小書的圖示，非常方便！




if failed, old version or etc, can use:

方法一：用 PNG 圖片代替（最穩陣）
如果你有一張細嘅書本 PNG 圖（例如 180x180 或 32x32 像素，命名為 favicon.png），將檔案同網頁放喺同一資料夾，然後喺 <head> 裡面加入下面兩行：


<link rel="icon" type="image/png" href="favicon.png">
<link rel="apple-touch-icon" href="favicon.png">


點解有效：舊版 iOS Safari 對 .png 格式嘅支援非常完整，特別是配合 apple-touch-icon，無論係加入書籤定係擺落主畫面，都會直接讀取呢張 PNG。



方法二：暫時用「Emoji 網址」當作圖片引入
如果你手頭真係冇 PNG 圖，又唔想煩整檔案，可以借用網上現成嘅 Emoji 轉圖服務（例如 sapi.is 或其他 favicon 產生器），把 📚 轉成 PNG 連結：


<link rel="apple-touch-icon" href="https://api.iconify.design/fluent-emoji:books.svg?format=png">


(你也可以把上面這行直接貼進 <head> 試試看舊版 Safari 會不會抓取這個遠端 PNG 連結)

💡 實測時必須注意：
因為 iOS Safari 的快取（Cache）極度頑固，你每次修改完程式碼之後，必須要把 Safari 整個從背景強制關閉（上滑清除），然後重新開機或重新打開 Safari，先至有機會重新整理出個 icon。如果試咗 PNG 都唔得，通常就真係受限於 iOS 15.6 嘅系統瀏覽器版本上限。



Icon web information:

1. Iconify (icon-sets.iconify.design)

數量：超過 200,000 個以上的開源圖示。

特點：它整合了幾乎所有知名的開源圖標集（例如 Material Design、FontAwesome、Bootstrap Icons、Lucide 等）。

用法：入面有大量電子書、書本、閱讀器相關嘅圖標。你可以直接在網站搜尋「book」或「reading」，點選喜歡的圖標後，它會提供可以直接用的圖片網址或 PNG 下載選項。



2. Flaticon (www.flaticon.com)

數量：數以百萬計的向量圖與 Icon。

特點：全世界最大的免費 icon 搜尋引擎之一。只要在搜尋欄打「book」、「epub」或者「reader」，就會彈出幾萬個唔同設計風格（手繪、扁平化、霓虹、極簡）嘅書本 icon。

用法：揀中邊個就可以直接免費下載成 PNG 格式（有 16x16、32x32、64x64 等尺寸），非常適合拿來解決 iOS 舊版本支援的問題。


3. IconScout (iconscout.com)

數量：數十萬個免費 Icon、3D 插圖與動態圖標。

特點：介面非常現代化，支援一鍵下載 PNG、SVG 格式，甚至可以線上直接修改 icon 的顏色。


💡 點樣用呢啲網站嘅 PNG 救星方法？
去 Flaticon 或 Iconify 搵一個你最鍾意嘅書本 icon。

下載它的 PNG 檔案（例如命名為 my-book.png）。

放到你網頁嘅資料夾入面。

喺 HTML 嘅 <head> 裡面加入以下呢行（支援所有包括 iOS 15.6 在內的舊版 Safari）：


<link rel="apple-touch-icon" href="my-book.png">
<link rel="icon" type="image/png" href="my-book.png">




































