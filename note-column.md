Column or Container

在 Flet 中，製作動態清單（新增與刪除項目）的核心概念是：

1. 使用 ft.Column 作為容器，專門用來存放一整排的列（Row）或控制項。

2. 新增項目時：向 column.controls 清單中 append() 一個全新的列。

3. 刪除項目時：從 column.controls 中 remove() 指定的列。

4. 關鍵步驟：每次修改陣列後，都要呼叫 page.update() 來刷新介面。


1. 核心邏輯與語法說明
ft.Column：垂直排列容器。它的 .controls 是一個 Python 清單（List），裡面放著所有要顯示的元件。

controls.append(item)：把新元件加到清單最下方。

controls.remove(item)：把指定的元件從清單中移除。

ft.Card / ft.Container：包裝每一個項目，讓每個清單列看起來像獨立的卡片。

2. 完整實作範例：可新增/刪除的卡片清單 App
請將以下程式碼貼入你的 app.py 中並執行：



PIC1
import ssl
import flet as ft

# 解決 macOS 11.3 SSL 證書問題
ssl._create_default_https_context = ssl._create_unverified_context

def main(page: ft.Page):
    page.title = "動態清單管理 App"
    page.padding = 30
    page.scroll = ft.ScrollMode.AUTO  # 允許頁面超出時自動滾動
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER

    # 1. 輸入框與清單容器
    item_input = ft.TextField(
        label="輸入項目名稱", 
        placeholder="例如：購買牛奶、寫 Python 作業", 
        width=300
    )
    
    # 用來存放所有動態項目的 Column 容器
    list_column = ft.Column(spacing=10)

    # 2. 刪除項目的邏輯函式
    def delete_item(item_card):
        # 從 Column 的 controls 陣列中移除指定的卡片元件
        list_column.controls.remove(item_card)
        page.update()  # 重新渲染畫面

    # 3. 新增項目的邏輯函式
    def add_item(e):
        text_val = item_input.value.strip()
        if not text_val:
            return  # 如果輸入框是空的就不處理

        # 先宣告一個變數預留給 Card，這樣內部的刪除按鈕才能引用到它自身
        item_card = None

        # 建立刪除按鈕與事件
        delete_btn = ft.IconButton(
            icon=ft.icons.DELETE_OUTLINED,
            icon_color=ft.colors.RED_400,
            tooltip="刪除此項",
            on_click=lambda _: delete_item(item_card)  # 利用 lambda 傳入對應的 item_card
        )

        # 建立單一項目的卡片 (Card)
        item_card = ft.Card(
            content=ft.Container(
                content=ft.Row(
                    controls=[
                        ft.Row(
                            controls=[
                                ft.Icon(ft.icons.CHECK_CIRCLE_OUTLINE, color=ft.colors.BLUE),
                                ft.Text(text_val, size=16, weight=ft.FontWeight.W_500),
                            ],
                            alignment=ft.MainAxisAlignment.START
                        ),
                        delete_btn
                    ],
                    alignment=ft.MainAxisAlignment.SPACE_BETWEEN
                ),
                padding=12,
                bgcolor=ft.colors.SURFACE_VARIANT,
                border_radius=8
            ),
            width=450
        )

        # 將新建的卡片加入至 Column 中
        list_column.controls.append(item_card)
        
        # 清空輸入框並刷新頁面
        item_input.value = ""
        page.update()

    add_btn = ft.ElevatedButton(
        "新增", 
        icon=ft.icons.ADD, 
        on_click=add_item
    )

    # 4. 版面配置
    input_row = ft.Row(
        controls=[item_input, add_btn],
        alignment=ft.MainAxisAlignment.CENTER
    )

    page.add(
        ft.Text("📝 動態清單管理 (Column/Container)", size=24, weight=ft.FontWeight.BOLD),
        ft.Divider(height=20),
        input_row,
        ft.Divider(height=20, color=ft.colors.TRANSPARENT),
        list_column
    )

ft.app(target=main)


💡 核心技巧拆解
1. lambda 閉包傳參（刪除關鍵）：



PIC2
on_click=lambda _: delete_item(item_card)

因為每個項目的刪除按鈕需要知道自己該刪除哪一個 item_card，所以使用匿名函式 lambda 把該項目的 item_card 物件精準傳入 delete_item() 函式中。

2. 內置滾動（page.scroll）：
當新增了幾十個項目導致長度超出螢幕時，設定 page.scroll = ft.ScrollMode.AUTO 可以讓頁面自動出現滾動條，不會產生畫面溢出裁切的問題。

3. 視覺包裝（Row + Card + Container）：
在 Row 裡面設定 alignment=ft.MainAxisAlignment.SPACE_BETWEEN，可以讓左邊的「文字標題」與右邊的「刪除圖示」自動向兩端靠齊，呈現漂亮的清單版面。






