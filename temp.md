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


