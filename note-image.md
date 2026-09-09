在 Flet 中加入與修改圖片非常簡單。你可以使用本地圖片（電腦上的圖檔）或是網路上的圖片連結。

以下是新增與動態修改圖片的詳細做法與範例：

1. 基礎概念：ft.Image 元件
Flet 使用 ft.Image 來渲染圖片。常用的屬性包括：

src：圖片路徑（可以填網址 https://... 或本地相對路徑）。

width / height：圖片的寬度與高度（像素）。

fit：圖片裁切/縮放模式（例如 ft.ImageFit.COVER 或 ft.ImageFit.CONTAIN）。

border_radius：設定圓角（配搭 Container 可以做出圓形頭像）。

2. 實作範例：動態切換頭像圖片
下面這段程式碼展示了如何放一張預設頭像，並透過點擊按鈕來動態更換頭像圖片：


PIC1
import ssl
import flet as ft

# 解決 macOS 11.3 SSL 證書問題
ssl._create_default_https_context = ssl._create_unverified_context

def main(page: ft.Page):
    page.title = "Flet 圖片顯示與切換範例"
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER
    page.vertical_alignment = ft.MainAxisAlignment.CENTER

    # 定義兩張網路圖片網址（做為範例）
    avatar_1 = "https://picsum.photos/id/1025/200/200"  # 狗狗圖片
    avatar_2 = "https://picsum.photos/id/237/200/200"   # 黑狗圖片

    # 1. 建立圖片元件
    user_avatar = ft.Image(
        src=avatar_1,
        width=150,
        height=150,
        fit=ft.ImageFit.COVER,
    )

    # 2. 用 Container 包裹圖片，做成圓形頭像框
    avatar_container = ft.Container(
        content=user_avatar,
        width=150,
        height=150,
        border_radius=75,  # 寬度的一半即可變成正圓形
        clip_behavior=ft.ClipBehavior.ANTI_ALIAS,  # 裁切超出圓形的圖片邊緣
        border=ft.border.all(3, ft.colors.BLUE)     # 外框線
    )

    # 3. 更換圖片的邏輯
    def change_avatar(e):
        # 切換圖片來源 (src)
        if user_avatar.src == avatar_1:
            user_avatar.src = avatar_2
        else:
            user_avatar.src = avatar_1
        
        page.update()  # 告知 Flet 刷新畫面

    change_btn = ft.ElevatedButton(
        "換一張頭像", 
        icon=ft.icons.REFRESH, 
        on_click=change_avatar
    )

    # 4. 將元件加入頁面
    page.add(
        ft.Text("👤 個人頭像範例", size=22, weight=ft.FontWeight.BOLD),
        avatar_container,
        ft.Divider(height=20, color=ft.colors.TRANSPARENT),
        change_btn
    )

ft.app(target=main)



核心重點解析
圓形頭像做法：
將 ft.Image 放入 ft.Container 中，將 Container 的 border_radius 設定為寬度的一半（150 / 2 = 75），並加上 clip_behavior=ft.ClipBehavior.ANTI_ALIAS，圖片就會被裁切成完美的圓形頭像。

如何修改圖片：
在事件函式中（如 change_avatar），直接修改 user_avatar.src = "新路徑"，最後呼叫 page.update()，畫面上的圖片就會立刻更新。

使用電腦裡面的本地圖片：
如果你想用電腦裡的圖檔（例如 my_photo.png），請把圖片跟 app.py 放在同一個資料夾，並將 src 寫成：


PIC2
user_avatar = ft.Image(src="my_photo.png", width=150, height=150)




