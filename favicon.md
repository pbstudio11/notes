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



