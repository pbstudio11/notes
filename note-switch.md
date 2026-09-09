切換深色（Dark）與淺色（Light）主題是現代 App 最常見的功能之一。

在 Flet 中，這項功能實現起來非常簡潔，因為 ft.Page 本身就內建了 page.theme_mode 屬性，我們只需要透過 ft.Switch 開關來改變這個屬性即可。

1. 基礎屬性說明
ft.Switch：開關元件。

label：開關旁邊顯示的文字。

value：開關狀態，True 代表開啟，False 代表關閉。

on_change：當使用者點擊切換開關時，要執行的函式。

page.theme_mode：控制頁面主題模式。

ft.ThemeMode.DARK（深色模式）

ft.ThemeMode.LIGHT（淺色模式）

ft.ThemeMode.SYSTEM（跟隨系統預設設定）

2. 完整實作範例
請將以下程式碼貼入你的 app.py 中並執行：



PIC1
import ssl
import flet as ft

# 解決 macOS 11.3 SSL 證書問題
ssl._create_default_https_context = ssl._create_unverified_context

def main(page: ft.Page):
    page.title = "主題切換 App"
    page.padding = 30
    
    # 預設頁面主題為淺色模式
    page.theme_mode = ft.ThemeMode.LIGHT
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER

    # 1. 定義主題切換的邏輯函式
    def theme_changed(e):
        # e.control.value 會取得 Switch 的當前狀態 (True 或 False)
        if theme_switch.value:
            page.theme_mode = ft.ThemeMode.DARK
            status_text.value = "當前模式：深色主題 🌙"
            status_text.color = ft.colors.AMBER_300  # 更換文字顏色
        else:
            page.theme_mode = ft.ThemeMode.LIGHT
            status_text.value = "當前模式：淺色主題 ☀️"
            status_text.color = ft.colors.BLUE_700

        page.update()  # 重新渲染頁面

    # 2. 建立 Switch 切換開關
    theme_switch = ft.Switch(
        label="切換深色模式",
        value=False,             # 預設為關閉 (False)
        on_change=theme_changed  # 當開關狀態改變時觸發函式
    )

    # 3. 建立狀態文字與卡片，觀察主題變化
    status_text = ft.Text("當前模式：淺色主題 ☀️", size=20, weight=ft.FontWeight.BOLD)
    
    sample_card = ft.Card(
        content=ft.Container(
            content=ft.Column(
                controls=[
                    ft.ListTile(
                        leading=ft.Icon(ft.icons.PALETTE),
                        title=ft.Text("卡片元件示範"),
                        subtitle=ft.Text("切換主題時，Card 與 Container 的背景色會自動適應主題風格！")
                    )
                ]
            ),
            padding=15
        ),
        width=400
    )

    # 4. 將元件加入頁面
    page.add(
        ft.Text("🌓 Flet 主題切換教學", size=26, weight=ft.FontWeight.BOLD),
        theme_switch,
        ft.Divider(height=20),
        status_text,
        sample_card
    )

ft.app(target=main)



核心重點解析
自動適應顏色：
Flet 的原生元件（如 ft.Card、ft.TextField、ft.ElevatedButton）都內建了主題適應功能。當你改變 page.theme_mode 並呼叫 page.update() 時，所有文字顏色與背景顏色都會自動跟著調整，不需要手動幫每一個元件改顏色。

e.control.value：
在事件處理函式中，theme_switch.value（或 e.control.value）會回傳一個布林值（True 代表開關被拉到右邊開起，False 代表在左邊關閉）。
