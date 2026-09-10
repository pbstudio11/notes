print(type("Hello"))  # 會顯示 <class 'str'>  (字串 String)
print(type(True))     # 會顯示 <class 'bool'> (布林值 Boolean)
print(type(100))      # 會顯示 <class 'int'>  (整數 Integer/數字)

「不一定要加空格，但強烈建議要加。」
在 Python 語法中，s = "Hello" 與 s="Hello" 對電腦來說完全一樣，都可以正常執行。


例外情況（先知道即可）
只有在函式帶入參數（Function Arguments）時，等號兩邊才會故意不加空格，例如：
Python

print("Hello", end="")  # 這裡的 end="" 習慣不加空格
結論：平時建立變數時，養成長期習慣寫成 s = "Hello"（前後各空一格）是最好的做法！

n = 0
for x in [0, 1, 2, 3]:
	if x % 2 == 0:
		continue
	n +=1
print(n)


x=3+6
print(x)
= print 9

x=7%3
print (x)
= print 1

x=2+3
print(x)
= print 5
x=x+1 or x+=1
print(x)
= print 6







1. 在 Flet App 裡面想顯示文字，卻用了 print()
在 Flet 介面開發中，print(msg) 只會把文字印在底部看不見的 Terminal 終端機，而不會顯示在 App 畫面上！

如果在 Flet 中要顯示文字：你應該建立 ft.Text 元件並加入 page，而不是用 print()：


import flet as ft

def main(page: ft.Page):
    # Flet 顯示文字的方式：
    def say(msg):
        page.add(ft.Text(msg))  # 👈 顯示在 App 畫面上

    say("Hello Flet!")

ft.app(target=main)


2. 呼叫時忘記傳入參數
say(msg) 需要傳入一個參數，如果你呼叫時沒給參數（例如只寫 say()），Python 會報錯 TypeError: say() missing 1 required positional argument: 'msg'。




經典直覺 Emoji 書本 (📚)

<link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><rect width=%22100%22 height=%22100%22 rx=%2222%22 fill=%22%23f1f5f9%22/><text x=%2250%22 y=%2270%22 font-size=%2262%22 text-anchor=%22middle%22>📚</text></svg>">





