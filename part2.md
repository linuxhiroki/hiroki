# 第2部：Pythonの基本操作

この章では、グラフ描画に必要なPython基本操作について学びます。プログラミング経験がなくても大丈夫です。

## 2.1 変数と代入

変数は値を保存するための「箱」のようなものです。

### 2.1.1 基本的な変数の使い方

```python
# 変数への代入
x = 10      # 整数
y = 3.14    # 小数（浮動小数点数）
name = "データ分析"  # 文字列
is_valid = True  # 真偽値（Boolean）

# 変数の中身を確認
print(x)
print(y)
print(name)
print(is_valid)
```

変数名のルール：
- 英数字とアンダースコア（_）が使用可能
- 数字から始めることはできない
- 大文字と小文字は区別される（`data` と `Data` は別の変数）
- すでにPythonで使われている予約語（`if`, `for`, `while`など）は使用できない

### 2.1.2 変数の型

Pythonでは変数の型が自動的に決まります（動的型付け）。

```python
# 変数の型を確認
x = 10
print(type(x))  # <class 'int'>

y = 3.14
print(type(y))  # <class 'float'>

name = "データ分析"
print(type(name))  # <class 'str'>
```

よく使う型：
- `int`: 整数（例：1, 100, -5）
- `float`: 浮動小数点数（例：3.14, -0.001）
- `str`: 文字列（例："hello", 'Python'）
- `bool`: 真偽値（例：True, False）
- `list`: リスト（後述）

## 2.2 数値と簡単な計算

### 2.2.1 基本的な演算

```python
a = 10
b = 3

# 基本的な演算
print(f"a + b = {a + b}")    # 足し算: 13
print(f"a - b = {a - b}")    # 引き算: 7
print(f"a * b = {a * b}")    # 掛け算: 30
print(f"a / b = {a / b}")    # 割り算: 3.3333...
print(f"a // b = {a // b}")  # 整数除算（小数点以下切り捨て）: 3
print(f"a % b = {a % b}")    # 余り: 1
print(f"a ** b = {a ** b}")  # べき乗（aのb乗）: 1000
```

### 2.2.2 数値計算の優先順位

数学と同じく、掛け算・割り算は足し算・引き算より先に計算されます。

```python
result = 2 + 3 * 4
print(result)  # 14 (3*4が先に計算され、その後で2を足す)

# 括弧を使って優先順位を変更
result = (2 + 3) * 4
print(result)  # 20 (括弧内が先に計算される)
```

### 2.2.3 便利な数学関数

より複雑な数学計算には、`math`モジュールや`numpy`モジュールを使います。

```python
import math
import numpy as np

# mathモジュールの関数
print(f"円周率: {math.pi}")
print(f"平方根: {math.sqrt(16)}")  # 4.0
print(f"三角関数: {math.sin(math.pi/2)}")  # 1.0

# numpyモジュールの関数
angles = np.linspace(0, 2*np.pi, 5)  # 0から2πまでを4等分した点
print(f"等間隔の点: {angles}")
print(f"指数関数: {np.exp(1)}")  # 自然対数の底e
print(f"対数関数: {np.log10(100)}")  # 2.0
```

## 2.3 リスト（グラフデータを扱うための基本）

リストは複数の値をまとめて扱うためのデータ構造です。グラフを描画する際には、x軸とy軸のデータをリストで管理することが多いです。

### 2.3.1 リストの作成と基本操作

```python
# リストの作成
numbers = [1, 2, 3, 4, 5]
colors = ["red", "green", "blue"]
mixed = [1, "hello", 3.14, True]  # 異なる型の要素も含められる

# リストの長さ
print(f"リストの長さ: {len(numbers)}")  # 5

# リストの要素にアクセス（インデックスは0から始まる）
print(f"最初の要素: {numbers[0]}")  # 1
print(f"2番目の要素: {numbers[1]}")  # 2
print(f"最後の要素: {numbers[4]}")  # 5
print(f"最後の要素（別の書き方）: {numbers[-1]}")  # 5（負のインデックスは後ろから）

# リストの一部を取り出す（スライス）
print(f"最初の3つの要素: {numbers[0:3]}")  # [1, 2, 3]
print(f"2番目から最後まで: {numbers[1:]}")  # [2, 3, 4, 5]
print(f"最初から3番目まで: {numbers[:3]}")  # [1, 2, 3]
```

### 2.3.3 NumPyの配列

科学計算やグラフ描画では、NumPyの配列（array）を頻繁に使います。NumPy配列はリストに似ていますが、数値計算に最適化されています。

```python
import numpy as np

# NumPy配列の作成
arr1 = np.array([1, 2, 3, 4, 5])
print(f"NumPy配列: {arr1}")

# 等間隔の数列を作成（グラフのx軸によく使う）
x = np.linspace(0, 10, 6)  # 0から10までの範囲を5等分（6点）
print(f"等間隔の点: {x}")  # [ 0.  2.  4.  6.  8. 10.]

# 配列の演算（要素ごとに計算される）
y = x ** 2  # xの各要素を2乗
print(f"x^2: {y}")  # [  0.   4.  16.  36.  64. 100.]

# 数学関数の適用
z = np.sin(x)  # xの各要素の正弦を計算
print(f"sin(x): {z}")
```

NumPy配列の利点：
- 要素ごとの演算が簡単（リストでは `[x**2 for x in list1]` のような内包表記が必要）
- 数学関数を直接適用できる
- 計算速度が速い

## 2.4 import文の基本

Pythonでは、外部のライブラリやモジュールを使うために`import`文を使います。

### 2.4.1 基本的なimport

```python
# モジュール全体をインポート
import math
print(math.pi)  # 3.141592653589793

# 特定の関数や変数だけをインポート
from math import sqrt, pi
print(sqrt(16))  # 4.0
print(pi)  # 3.141592653589793

# 別名（エイリアス）をつける
import numpy as np
import matplotlib.pyplot as plt

x = np.array([1, 2, 3])
plt.plot(x, x**2)
```

### 2.4.2 グラフ描画に必要な主なライブラリ

```python
# 基本的なグラフ描画に必要なインポート
import matplotlib.pyplot as plt  # グラフ描画
import numpy as np              # 数値計算
import pandas as pd             # データ操作

# 使用例
x = np.linspace(0, 10, 100)
y = np.sin(x)
plt.plot(x, y)
plt.title("正弦波")
plt.xlabel("x")
plt.ylabel("sin(x)")
plt.grid(True)
plt.show()
```

## 2.5 関数の基本

関数とは、特定の処理をまとめて名前をつけたものです。繰り返し使う処理を一度定義しておくと便利です。

### 2.5.1 関数の定義と使い方

```python
# 関数の定義
def greet(name):
    """あいさつする関数"""
    message = f"こんにちは、{name}さん！"
    return message

# 関数の使用
result = greet("太郎")
print(result)  # こんにちは、太郎さん！
```

関数の基本構造：
```python
def 関数名(引数1, 引数2, ...):
    """関数の説明文（省略可）"""
    # 処理内容
    return 戻り値  # 戻り値を返す（省略可）
```

### 2.5.2 関数を使うメリット

1. **コードの再利用**：同じ処理を何度も書く必要がなくなる
2. **コードの整理**：処理をまとめることでプログラムが読みやすくなる
3. **修正が簡単**：処理を変更する場合、関数定義を一箇所だけ修正すればよい

### 2.5.3 グラフ描画での関数の活用例

```python
def plot_sine_wave(amplitude=1, frequency=1, phase=0):
    """
    正弦波をプロットする関数
    
    引数:
    amplitude: 振幅
    frequency: 周波数
    phase: 位相（ラジアン）
    """
    import numpy as np
    import matplotlib.pyplot as plt
    
    x = np.linspace(0, 2*np.pi, 100)
    y = amplitude * np.sin(frequency * x + phase)
    
    plt.figure(figsize=(8, 4))
    plt.plot(x, y)
    plt.title(f"正弦波 (振幅={amplitude}, 周波数={frequency})")
    plt.xlabel("x")
    plt.ylabel("y")
    plt.grid(True)
    plt.show()

# 関数の使用例
plot_sine_wave(amplitude=2, frequency=2)  # 振幅2、周波数2の正弦波をプロット
```

## 2.6 練習問題

### 練習問題1: 変数と計算
以下の計算結果を表示するコードを書いてください：
1. 半径5の円の面積と円周の長さ
2. 摂氏25度を華氏に変換（華氏 = 摂氏 × 9/5 + 32）

### 練習問題2: リスト操作
1. 1から10までの整数を含むリストを作成して表示
2. リストの3番目の要素と最後の要素を表示
3. リストの前半部分（最初の5つの要素）を取り出して表示

### 練習問題3: NumPy配列
1. 0から2πまでの範囲を100分割したNumPy配列を作成
2. その配列を使って、sin(x)とcos(x)を計算
3. matplotlibを使って、sin(x)とcos(x)をグラフにプロット

### 練習問題4: 関数の作成
1. 摂氏から華氏に変換する関数 `celsius_to_fahrenheit` を作成
2. 半径から円の面積を計算する関数 `calculate_circle_area` を作成
3. 以下の関数を完成させて、指定した範囲でのグラフをプロットする関数を作成
(*追記 グラフのプロットはpart4でやるので3は飛ばして大丈夫です。)

```python
def plot_function(func, start, end, points=100, title="関数のグラフ"):
    """
    指定した関数のグラフをプロットする
    
    引数:
    func: プロットする関数（例: np.sin, np.cos）
    start: x軸の開始値
    end: x軸の終了値
    points: プロットする点の数
    title: グラフのタイトル
    """
    # ここにコードを書く
    
# 使用例
plot_function(np.sin, 0, 2*np.pi, title="正弦関数")
```

## 解答例

### 練習問題1の解答

```python
import math

# 半径5の円の面積と円周
radius = 5
area = math.pi * radius ** 2
circumference = 2 * math.pi * radius

print(f"半径{radius}の円の面積: {area:.2f}")
print(f"半径{radius}の円の周長: {circumference:.2f}")

# 摂氏から華氏への変換
celsius = 25
fahrenheit = celsius * 9/5 + 32
print(f"{celsius}℃は{fahrenheit}°Fです")
```

### 練習問題2の解答

```python
# 1から10までのリスト
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
print(f"リスト: {numbers}")

# 3番目の要素
third_element = numbers[2]  # インデックスは0から始まるので、3番目は2
print(f"3番目の要素: {third_element}")

# 最後の要素
last_element = numbers[-1]
print(f"最後の要素: {last_element}")

# 前半部分（最初の5つの要素）
first_half = numbers[:5]
print(f"前半部分: {first_half}")
```

### 練習問題3の解答

```python
import numpy as np
import matplotlib.pyplot as plt

# 0から2πまでの等間隔な点を100個生成
x = np.linspace(0, 2*np.pi, 100)

# sin(x)とcos(x)を計算
y_sin = np.sin(x)
y_cos = np.cos(x)

# グラフの描画
plt.figure(figsize=(10, 6))
plt.plot(x, y_sin, label='sin(x)')
plt.plot(x, y_cos, label='cos(x)')
plt.xlabel('x')
plt.ylabel('y')
plt.title('正弦波と余弦波')
plt.legend()
plt.grid(True)
plt.show()
```

### 練習問題4の解答

```python
import math
import numpy as np
import matplotlib.pyplot as plt

# 1. 摂氏から華氏への変換関数
def celsius_to_fahrenheit(celsius):
    """摂氏温度を華氏温度に変換する"""
    return celsius * 9/5 + 32

# 関数のテスト
print(f"25℃ = {celsius_to_fahrenheit(25)}°F")
print(f"0℃ = {celsius_to_fahrenheit(0)}°F")
print(f"100℃ = {celsius_to_fahrenheit(100)}°F")

# 2. 円の面積を計算する関数
def calculate_circle_area(radius):
    """半径から円の面積を計算する"""
    return math.pi * radius ** 2

# 関数のテスト
print(f"半径5の円の面積: {calculate_circle_area(5):.2f}")
print(f"半径10の円の面積: {calculate_circle_area(10):.2f}")

# 3. グラフプロット関数
def plot_function(func, start, end, points=100, title="関数のグラフ"):
    """指定した関数のグラフをプロットする"""
    # x軸のデータ生成
    x = np.linspace(start, end, points)
    # y軸のデータ計算
    y = func(x)
    
    # グラフのプロット
    plt.figure(figsize=(8, 5))
    plt.plot(x, y)
    plt.title(title)
    plt.xlabel('x')
    plt.ylabel('y')
    plt.grid(True)
    plt.show()

# 関数の使用例
plot_function(np.sin, 0, 2*np.pi, title="正弦関数")
plot_function(np.cos, 0, 2*np.pi, title="余弦関数")
# 2次関数のプロット
plot_function(lambda x: x**2, -5, 5, title="2次関数")
```

## 次のステップ

これでPythonの基本操作を学習しました。次の第3部では、実験データの読み込みとパンダス（pandas）ライブラリを使ったデータ操作について学びます。
