Calibre 3.48 的 Edit Book（編輯書籍） 裡直接修改，以下「可以直接複製貼上」的 code。


最常用的 CSS：

/* =========================
   EPUB 基本設定
   ========================= */

body {
    margin: 0;
    padding: 0;
    font-family: serif;
    font-size: 1em;
    line-height: 1.8;
    text-align: justify;
}


/* =========================
   章節標題
   ========================= */

h1 {
    text-align: center;
    font-size: 2em;
    margin-top: 20%;
    margin-bottom: 1.5em;
}

h2 {
    text-align: center;
    font-size: 1.4em;
    margin-top: 2em;
    margin-bottom: 1em;
}


/* =========================
   正文
   ========================= */

p {
    margin-top: 0;
    margin-bottom: 0;
    text-indent: 2em;
}


/* 第一段不縮排 */

p.first {
    text-indent: 0;
}


/* =========================
   置中
   ========================= */

.center {
    text-align: center;
    text-indent: 0;
}


/* =========================
   左對齊
   ========================= */

.left {
    text-align: left;
}


/* =========================
   右對齊
   ========================= */

.right {
    text-align: right;
}


/* =========================
   強制換頁
   ========================= */

.page-break {
    page-break-before: always;
}


/* =========================
   圖片
   ========================= */

img {
    max-width: 100%;
    height: auto;
}

.image-center {
    text-align: center;
    text-indent: 0;
}

.image-center img {
    max-width: 100%;
    height: auto;
}


/* =========================
   橫向頁面
   ========================= */

.landscape {
    page-break-before: always;
    page-break-after: always;
}


/* =========================
   引文
   ========================= */

blockquote {
    margin-left: 2em;
    margin-right: 2em;
    font-style: italic;
}


/* =========================
   不縮排
   ========================= */

.no-indent {
    text-indent: 0;
}






HTML 模式：
例如普通章節：


<h1>第一章</h1>

<p class="first">這是第一段文字，第一行不縮排。</p>

<p>這是第二段文字，會自動首行縮排兩個字。</p>

<p>這是第三段文字。</p>




強制從新頁開始：


<div class="page-break"></div>

<h1>第二章</h1>



文字置中：


<p class="center">這一行文字會置中。</p>



圖片置中：


<div class="image-center">
    <img src="../Images/cover.jpg" alt="圖片" />
</div>




「直向／橫向」

若EPUB 是一般小說、文字書，不建議單純依賴：

@page {
    size: landscape;
}


因為 Calibre 3.48 以及不同 EPUB 閱讀器對這個設定的處理可能不同。

如果需求是：

📖 一般章節全部直向，但是某一頁地圖／大型表格需要橫向

最好用 EPUB 3 Fixed Layout（固定版面） 的方式處理；如果只是普通 reflowable EPUB，則需要考慮閱讀器支援。


可以直接給完整範本：

📖 小說型 EPUB — 直向、首行縮排、章節、目錄、分頁
📚 教材型 EPUB — 直向＋橫向表格／圖片
🖼️ 圖文書 — 每頁固定圖片大小、直向／橫向
📐 固定版面 EPUB — 像 PDF 一樣，每一頁都有固定位置
🇨🇳 中文書排版 — 直排（文字由上至下、由右至左）

如果說的是「中文書的直向」，也就是想要 文字真正由上往下、右邊開始，像傳統中文書那樣的直排，也可以直接給 Calibre 3.48 可用的寫法。





適合 Calibre 3.48「Edit Book」直接使用的完整 EPUB 範本。我會以「中文小說／一般文字書」為主，包含：

封面
書名頁
版權頁
目錄
章節
中文首行縮排
章節換頁
置中／左右對齊
圖片
引文
頁面分隔
橫向內容頁
CSS 基本設定
EPUB 3 package.opf

1. 建議的 EPUB 結構
在 Calibre 3.48 的 Edit Book 裡，建議整理成：


EPUB/
│
├── Text/
│   ├── cover.xhtml
│   ├── title.xhtml
│   ├── copyright.xhtml
│   ├── toc.xhtml
│   ├── chapter01.xhtml
│   ├── chapter02.xhtml
│   └── chapter03.xhtml
│
├── Styles/
│   └── style.css
│
├── Images/
│   └── cover.jpg
│
└── content.opf



2. CSS 完整範本
在 Styles/style.css 放下面這份。

/* =========================================================
   EPUB CSS
   適用：Calibre 3.48
   用途：中文小說／一般文字書
   ========================================================= */


/* =========================================================
   1. 基本設定
   ========================================================= */

html {
    margin: 0;
    padding: 0;
}

body {
    margin: 0;
    padding: 0;

    font-family: serif;
    font-size: 1em;
    line-height: 1.8;

    text-align: justify;

    /* 中文不要自動斷字 */
    word-break: normal;
    overflow-wrap: normal;
}


/* =========================================================
   2. 段落
   ========================================================= */

p {
    margin-top: 0;
    margin-bottom: 0;

    text-indent: 2em;
}


/* 第一段不縮排 */

p.first {
    text-indent: 0;
}


/* 不縮排 */

.no-indent {
    text-indent: 0;
}


/* =========================================================
   3. 章節標題
   ========================================================= */

h1 {
    margin-top: 20%;
    margin-bottom: 2em;

    text-align: center;

    font-size: 2em;
    font-weight: bold;

    text-indent: 0;
}


h2 {
    margin-top: 2em;
    margin-bottom: 1em;

    text-align: center;

    font-size: 1.4em;
    font-weight: bold;

    text-indent: 0;
}


h3 {
    margin-top: 1.5em;
    margin-bottom: 1em;

    text-align: center;

    font-size: 1.2em;
    font-weight: bold;

    text-indent: 0;
}


/* =========================================================
   4. 章節開始／強制換頁
   ========================================================= */

.chapter {
    page-break-before: always;
}


.page-break {
    page-break-before: always;
}


/* 避免標題獨立在頁尾 */

h1,
h2,
h3 {
    page-break-after: avoid;
}


/* =========================================================
   5. 文字對齊
   ========================================================= */

.center {
    text-align: center;
    text-indent: 0;
}


.left {
    text-align: left;
    text-indent: 0;
}


.right {
    text-align: right;
    text-indent: 0;
}


.justify {
    text-align: justify;
}


/* =========================================================
   6. 書名頁
   ========================================================= */

.title-page {
    text-align: center;
    text-indent: 0;

    margin-top: 25%;
}


.book-title {
    font-size: 2.5em;
    font-weight: bold;

    text-align: center;
    text-indent: 0;

    margin-bottom: 1em;
}


.book-subtitle {
    font-size: 1.3em;

    text-align: center;
    text-indent: 0;

    margin-bottom: 3em;
}


.author {
    font-size: 1.2em;

    text-align: center;
    text-indent: 0;
}


/* =========================================================
   7. 版權頁
   ========================================================= */

.copyright {
    margin-top: 20%;

    text-align: center;
    text-indent: 0;
}


.copyright p {
    text-indent: 0;
    text-align: center;

    margin-bottom: 0.8em;
}


/* =========================================================
   8. 目錄
   ========================================================= */

.toc {
    text-align: left;
    text-indent: 0;
}


.toc h1 {
    text-align: center;
}


.toc a {
    text-decoration: none;
}


/* =========================================================
   9. 圖片
   ========================================================= */

.image {
    text-align: center;
    text-indent: 0;

    margin: 1em 0;
}


.image img {
    max-width: 100%;
    height: auto;
}


.full-image {
    text-align: center;
    text-indent: 0;

    margin: 0;
    padding: 0;
}


.full-image img {
    max-width: 100%;
    height: auto;
}


/* =========================================================
   10. 圖片說明
   ========================================================= */

.caption {
    text-align: center;
    text-indent: 0;

    font-size: 0.9em;
    font-style: italic;

    margin-top: 0.5em;
}


/* =========================================================
   11. 引文
   ========================================================= */

blockquote {
    margin-left: 2em;
    margin-right: 2em;

    text-align: justify;

    font-style: italic;
}


blockquote p {
    text-indent: 0;
}


/* =========================================================
   12. 分隔線
   ========================================================= */

.separator {
    text-align: center;
    text-indent: 0;

    margin-top: 1.5em;
    margin-bottom: 1.5em;
}


/* =========================================================
   13. 詩／歌詞／特殊文字
   ========================================================= */

.poem {
    text-align: left;
    text-indent: 0;

    margin-left: 2em;
    margin-right: 2em;

    line-height: 1.8;
}


.poem p {
    text-indent: 0;
}


/* =========================================================
   14. 注釋
   ========================================================= */

.footnote {
    font-size: 0.85em;

    text-indent: 0;

    margin-top: 1em;
}


/* =========================================================
   15. 橫向內容
   ========================================================= */

.landscape {
    page-break-before: always;
    page-break-after: always;

    text-align: center;
    text-indent: 0;
}


/* EPUB 閱讀器支援時使用 */

@page landscape-page {
    size: landscape;
}


/* =========================================================
   16. 表格
   ========================================================= */

table {
    width: 100%;

    border-collapse: collapse;

    margin-top: 1em;
    margin-bottom: 1em;

    font-size: 0.9em;
}


th,
td {
    border: 1px solid #666;

    padding: 0.4em;

    text-align: left;

    vertical-align: top;
}


/* =========================================================
   17. 粗體／斜體
   ========================================================= */

.bold {
    font-weight: bold;
}


.italic {
    font-style: italic;
}


/* =========================================================
   18. 大字／小字
   ========================================================= */

.large {
    font-size: 1.3em;
}


.small {
    font-size: 0.8em;
}


/* =========================================================
   19. 空白間距
   ========================================================= */

.space {
    height: 1em;
}


.large-space {
    height: 3em;
}


/* =========================================================
   20. 防止某些元素產生縮排
   ========================================================= */

img,
table,
blockquote,
div {
    text-indent: 0;
}





3. 書名頁 title.xhtml

<?xml version="1.0" encoding="utf-8"?>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:epub="http://www.idpf.org/2007/ops">

<head>
    <title>我的電子書</title>

    <link rel="stylesheet"
          type="text/css"
          href="../Styles/style.css" />
</head>

<body>

<div class="title-page">

    <p class="book-title">
        我的電子書
    </p>

    <p class="book-subtitle">
        一個故事的開始
    </p>

    <p class="author">
        作者：作者姓名
    </p>

</div>

</body>
</html>






4. 版權頁 copyright.xhtml

<?xml version="1.0" encoding="utf-8"?>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:epub="http://www.idpf.org/2007/ops">

<head>
    <title>版權資訊</title>

    <link rel="stylesheet"
          type="text/css"
          href="../Styles/style.css" />
</head>

<body>

<div class="copyright">

    <h1>版權資訊</h1>

    <p>書名：我的電子書</p>

    <p>作者：作者姓名</p>

    <p>出版年份：2026</p>

    <p>All Rights Reserved.</p>

    <p>本電子書僅供個人閱讀使用。</p>

</div>

</body>
</html>





5. 目錄 toc.xhtml

<?xml version="1.0" encoding="utf-8"?>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:epub="http://www.idpf.org/2007/ops">

<head>
    <title>目錄</title>

    <link rel="stylesheet"
          type="text/css"
          href="../Styles/style.css" />
</head>

<body>

<nav epub:type="toc" id="toc" class="toc">

    <h1>目錄</h1>

    <p class="no-indent">
        <a href="chapter01.xhtml">第一章　新的開始</a>
    </p>

    <p class="no-indent">
        <a href="chapter02.xhtml">第二章　旅程</a>
    </p>

    <p class="no-indent">
        <a href="chapter03.xhtml">第三章　相遇</a>
    </p>

</nav>

</body>
</html>





6. 第一章 chapter01.xhtml

<?xml version="1.0" encoding="utf-8"?>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:epub="http://www.idpf.org/2007/ops">

<head>
    <title>第一章　新的開始</title>

    <link rel="stylesheet"
          type="text/css"
          href="../Styles/style.css" />
</head>

<body>

<section class="chapter"
         epub:type="chapter">

    <h1>第一章</h1>

    <h2>新的開始</h2>

    <p class="first">
        清晨的陽光從窗簾的縫隙中照進房間。
    </p>

    <p>
        他慢慢睜開眼睛，看著熟悉的天花板，卻突然感覺今天似乎有些不同。
    </p>

    <p>
        過了幾秒，他才想起來，今天是他離開這座城市的日子。
    </p>

    <p>
        行李早已整理完畢，放在房間的一角。
    </p>

    <p>
        他站起身，走到窗前，看著街道上逐漸忙碌起來的人群。
    </p>

    <p class="center">
        「是時候出發了。」
    </p>

</section>

</body>
</html>







7. 第二章 chapter02.xhtml：

<?xml version="1.0" encoding="utf-8"?>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml"
      xmlns:epub="http://www.idpf.org/2007/ops">

<head>
    <title>第二章　旅程</title>

    <link rel="stylesheet"
          type="text/css"
          href="../Styles/style.css" />
</head>

<body>

<section class="chapter"
         epub:type="chapter">

    <h1>第二章</h1>

    <h2>旅程</h2>

    <p class="first">
        火車緩緩離開月台。
    </p>

    <p>
        窗外的景色開始向後移動，熟悉的街道逐漸消失在視線之外。
    </p>

    <p>
        他靠在座椅上，第一次真正感覺到自己已經踏上了新的旅程。
    </p>

</section>

</body>
</html>





8. 如果需要圖片
例如章節中加入一張圖片：

<div class="image">

    <img src="../Images/example.jpg"
         alt="圖片說明" />

    <p class="caption">
        圖一　城市風景
    </p>

</div>


圖片會自動限制在閱讀器的寬度之內：


.image img {
    max-width: 100%;
    height: auto;
}


這對手機、平板和電腦閱讀器比較安全。





9. 如果需要橫向的大圖／表格
有一張很寬的地圖：


<div class="landscape">

    <img src="../Images/map.jpg"
         alt="地圖"
         style="max-width:100%; height:auto;" />

</div>


或者大型表格：


<div class="landscape">

    <table>

        <tr>
            <th>年份</th>
            <th>事件</th>
            <th>地點</th>
            <th>人物</th>
        </tr>

        <tr>
            <td>2026</td>
            <td>事件一</td>
            <td>倫敦</td>
            <td>人物 A</td>
        </tr>

        <tr>
            <td>2027</td>
            <td>事件二</td>
            <td>巴黎</td>
            <td>人物 B</td>
        </tr>

    </table>

</div>


**但要注意：**這種 CSS 的 landscape 並不能保證所有 EPUB 閱讀器真的把裝置畫面旋轉成橫向。
若你要求「這一頁一定橫屏」，就應該製作 Fixed Layout EPUB，那是另一種做法。



10. content.opf
如果直接在 Calibre 裡做 EPUB，通常可以讓 Calibre 幫忙管理 OPF。基本概念大概是：


<?xml version="1.0" encoding="utf-8"?>

<package xmlns="http://www.idpf.org/2007/opf"
         version="3.0"
         unique-identifier="BookID">

    <metadata xmlns:dc="http://purl.org/dc/elements/1.1/">

        <dc:identifier id="BookID">
            urn:uuid:12345678-1234-1234-1234-123456789abc
        </dc:identifier>

        <dc:title>我的電子書</dc:title>

        <dc:language>zh-TW</dc:language>

        <dc:creator>作者姓名</dc:creator>

        <meta property="dcterms:modified">
            2026-09-12T12:00:00Z
        </meta>

    </metadata>

    <manifest>

        <item id="css"
              href="Styles/style.css"
              media-type="text/css" />

        <item id="title"
              href="Text/title.xhtml"
              media-type="application/xhtml+xml" />

        <item id="copyright"
              href="Text/copyright.xhtml"
              media-type="application/xhtml+xml" />

        <item id="toc"
              href="Text/toc.xhtml"
              media-type="application/xhtml+xml"
              properties="nav" />

        <item id="chapter01"
              href="Text/chapter01.xhtml"
              media-type="application/xhtml+xml" />

        <item id="chapter02"
              href="Text/chapter02.xhtml"
              media-type="application/xhtml+xml" />

        <item id="chapter03"
              href="Text/chapter03.xhtml"
              media-type="application/xhtml+xml" />

    </manifest>

    <spine>

        <itemref idref="title" />

        <itemref idref="copyright" />

        <itemref idref="toc" />

        <itemref idref="chapter01" />

        <itemref idref="chapter02" />

        <itemref idref="chapter03" />

    </spine>

</package>


不過在 Calibre 3.48 裡，建議不要一開始就手改 OPF。
先讓 Calibre 建立 EPUB，再用 Edit Book → Tools → Table of Contents 等功能處理目錄，會比較不容易出錯。



11. 如果是「傳統中文直排」
但所說的「直向」其實是：

文字由上往下，而且由右邊開始，一欄一欄往左

例如：

我  天
們  地
在  玄
這  黃
裡  宇
相  宙
遇  之
。  間


那就不是普通的 Portrait，而是 CSS Writing Mode（直排）。

可以另外做：

.vertical {
    writing-mode: vertical-rl;
    -webkit-writing-mode: vertical-rl;

    height: 90vh;

    text-align: left;
    line-height: 1.8;

    margin: 0 auto;
}





HTML：


<div class="vertical">

    <p class="no-indent">
        這是一段中文直排文字。
        文字會從上往下排列，
        並由右向左延伸。
    </p>

</div>



不過這一部分要特別測試使用的目標閱讀器。 
Calibre 3.48 本身可以編輯 EPUB，但最後顯示效果是由實際 EPUB 閱讀器決定的；
Kindle、Apple Books、Calibre Viewer、Kobo 等對 CSS 的支援也可能不同。





如果目標是**「繁體中文小說，而且整本書像紙本中文書一樣右起直排」，可以使用一份完整的「中文直排 EPUB 模板」，
包括封面 → 書名頁 → 版權頁 → 目錄 → 右起直排正文 → 章節 → 標點 → 英文／數字 → 圖片 → 橫向頁面**，
是專門按照 Calibre 3.48 的編輯方式整理。

































