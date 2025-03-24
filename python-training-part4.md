# 第4部：matplotlibを用いたグラフ描画

この章では、matplotlibを使って論文品質のグラフを作成する方法を学びます。基本的なプロットから体裁の整え方まで、段階的に解説します。

## 4.1 基本プロット

### 4.1.1 matplotlibの導入

matplotlibはPythonで最も広く使われているグラフ描画ライブラリです。多種多様なグラフを作成でき、細かなカスタマイズも可能です。

```python
import matplotlib.pyplot as plt
import numpy as np
```

matplotlibには2つの主要なインターフェースがあります：

1. **PyplotインターフェースとOOインターフェース**
   - `pyplot`（plt）：MATLABライクな使い方ができるシンプルなインターフェース
   - Object-Oriented（OO）：より柔軟なカスタマイズが可能な方法

この研修では、主にObject-Oriented（OO）インターフェースを使用します。これは先に紹介されていた`fig, ax = plt.subplots()`のような書き方です。

### 4.1.2 折れ線グラフ（plot）の基本

最も基本的なグラフ、折れ線グラフを描画してみましょう：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 10, 100)  # 0から10までの100点
y = np.sin(x)  # 正弦波

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))  # 図とサブプロットの作成
ax.plot(x, y)  # 折れ線グラフの描画
ax.set_xlabel('x')  # x軸ラベル
ax.set_ylabel('sin(x)')  # y軸ラベル
ax.set_title('Sine Wave')  # タイトル
ax.grid(True)  # グリッド線表示

plt.show()  # グラフの表示
```

折れ線グラフのカスタマイズ：

```python
# 線のスタイル、色、マーカーを指定
ax.plot(x, y, linestyle='-', color='blue', linewidth=2, 
        marker='o', markersize=5, markevery=10, 
        label='sin(x)')

# 別の方法（短縮形）
ax.plot(x, y, 'ro-', label='sin(x)')  # 赤い線、丸いマーカー
```

よく使う線のスタイル：
- 線のスタイル：`'-'`（実線）、`'--'`（破線）、`'-.'`（一点鎖線）、`':'`（点線）
- マーカー：`'o'`（丸）、`'s'`（四角）、`'^'`（三角）、`'*'`（星）
- 色：`'b'`（青）、`'g'`（緑）、`'r'`（赤）、`'c'`（シアン）、`'m'`（マゼンタ）、`'y'`（黄）、`'k'`（黒）

### 4.1.3 散布図（scatter）の基本

点データを表示するための散布図を描画してみましょう：

```python
import matplotlib.pyplot as plt
import numpy as np

# ランダムデータの生成
np.random.seed(42)  # 乱数の再現性のため
x = np.random.rand(50)  # 0~1の一様乱数を50個
y = np.random.rand(50)

# 散布図の作成
fig, ax = plt.subplots(figsize=(8, 5))
ax.scatter(x, y, color='blue', marker='o', s=50, alpha=0.7, 
           edgecolors='black', label='Random Data')
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_title('Scatter Plot')
ax.legend()
ax.grid(True)

plt.show()
```

散布図のカスタマイズ：
- `s`: マーカーのサイズ（デフォルトは36）
- `alpha`: 透明度（0〜1、1が不透明）
- `edgecolors`: マーカーの枠線の色
- `c`: マーカーの色（データに応じて変えることも可能）

### 4.1.4 pandasからの直接プロット

pandasのデータフレームからは、直接プロットすることも可能です：

```python
import pandas as pd
import matplotlib.pyplot as plt

# データの準備（SineCurve.txtを読み込む）
df = pd.read_table("SineCurve.txt", names=["X", "Y"])

# pandasから直接プロット
fig, ax = plt.subplots(figsize=(8, 5))
df.plot(x='X', y='Y', ax=ax, color='blue', label='Sine')
ax.set_xlabel('X [degree]')
ax.set_ylabel('Y [-]')
ax.set_title('Sine Curve')
ax.grid(True)

plt.show()
```

複数の列をプロットする場合：

```python
# 複数列のデータフレーム
df['Y_squared'] = df['Y'] ** 2

# 複数列を一度にプロット
fig, ax = plt.subplots(figsize=(8, 5))
df.plot(x='X', y=['Y', 'Y_squared'], ax=ax)
ax.set_xlabel('X [degree]')
ax.set_ylabel('Y [-]')
ax.set_title('Sine Curve and Its Square')
ax.grid(True)
ax.legend(['sin(x)', 'sin²(x)'])

plt.show()
```

## 4.2 グラフの体裁整備

### 4.2.1 軸ラベルと凡例の設定

論文品質のグラフを作るためには、適切な軸ラベルと凡例が重要です：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y1 = np.sin(np.radians(x))
y2 = np.cos(np.radians(x))

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(x, y1, label='sin(x)')
ax.plot(x, y2, label='cos(x)')

# 軸ラベルの設定
ax.set_xlabel('Angle [degree]')  # 単位を含めるのが一般的
ax.set_ylabel('Amplitude [-]')   # 無次元量は[-]で表現

# タイトル設定
ax.set_title('Sine and Cosine Waves')

# 凡例の設定
ax.legend(loc='upper right', frameon=False)  # 枠なし、右上に配置

# グリッド線
ax.grid(True, linestyle='--', alpha=0.7)

plt.show()
```

凡例のカスタマイズ：
- `loc`: 位置（'best', 'upper right', 'lower left'など）
- `frameon`: 枠の表示/非表示
- `fontsize`: フォントサイズ
- `ncol`: 列数（複数列にする場合）

### 4.2.2 フォント設定（種類・サイズ）

論文に適したフォント設定：

```python
import matplotlib.pyplot as plt
import numpy as np

# フォント設定（グラフ作成前に行う）
plt.rcParams['font.family'] = 'Arial'  # 論文でよく使われるフォント
plt.rcParams['font.size'] = 12  # 基本フォントサイズ

# データの準備
x = np.linspace(0, 360, 100)
y = np.sin(np.radians(x))

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(x, y, label='sin(x)')

# フォントサイズを個別に設定
ax.set_xlabel('Angle [degree]', fontsize=14)
ax.set_ylabel('Amplitude [-]', fontsize=14)
ax.set_title('Sine Wave', fontsize=16)
ax.legend(fontsize=12)

# 軸の目盛りのフォントサイズ
ax.tick_params(axis='both', labelsize=12)

plt.show()
```

主要なフォントファミリー：
- 'Arial'（サンセリフ、論文に最適）
- 'Times New Roman'（セリフ、論文でよく使われる）
- 'Helvetica'（サンセリフ、クリーンな印象）
- 'DejaVu Sans'（サンセリフ、多言語対応）

### 4.2.3 範囲と目盛設定

軸の範囲と目盛りを適切に設定することで、データを効果的に表示できます：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y = np.sin(np.radians(x))

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(x, y)

# 軸の範囲設定
ax.set_xlim(0, 360)  # x軸の範囲
ax.set_ylim(-1.2, 1.2)  # y軸の範囲（少し余裕を持たせる）

# 主目盛の設定
ax.set_xticks(np.arange(0, 361, 90))  # 0, 90, 180, 270, 360
ax.set_yticks(np.arange(-1, 1.1, 0.5))  # -1, -0.5, 0, 0.5, 1

# 補助目盛の表示
ax.minorticks_on()

# 目盛線を内向きに（論文スタイル）
ax.tick_params(which='both', direction='in')

# グリッド線は主目盛のみ
ax.grid(which='major', linestyle='-', alpha=0.5)

plt.show()
```

目盛り設定のカスタマイズ：
- `ax.set_xticks()`: x軸の主目盛位置
- `ax.set_yticks()`: y軸の主目盛位置
- `ax.set_xticklabels()`: x軸の目盛ラベル
- `ax.minorticks_on()`: 補助目盛の表示
- `ax.tick_params()`: 目盛線のスタイル設定

### 4.2.4 複数データの表示方法

複数のデータセットを1つのグラフ上に表示する方法：

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

# データの準備（複数のデータセット）
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])
df_points = pd.read_table("plot.txt", names=["X", "Y"])

# グラフの作成
fig, ax = plt.subplots(figsize=(10, 6))

# 複数のデータをプロット
ax.plot(df_sine["X"], df_sine["Y"], 
        color='blue', linestyle='-', linewidth=1.5, 
        label='Sine')
        
ax.plot(df_cosine["X"], df_cosine["Y"], 
        color='red', linestyle='--', linewidth=1.5, 
        label='Cosine')
        
ax.scatter(df_points["X"], df_points["Y"], 
           color='green', marker='o', s=50, 
           label='Experimental')

# 軸ラベルと凡例
ax.set_xlabel('X [degree]')
ax.set_ylabel('Y [-]')
ax.set_title('Multiple Datasets')
ax.legend(loc='lower left', frameon=False)

# 軸範囲と目盛
ax.set_xlim(0, 360)
ax.set_ylim(-1.2, 1.2)
ax.minorticks_on()
ax.tick_params(which='both', direction='in')
ax.grid(True, alpha=0.5)

plt.show()
```

複数データの表示テクニック：
- 異なる線のスタイル、色、マーカーを使って区別する
- 適切な凡例で各データセットを説明する
- 理論曲線と実験データを区別するために、線と点を組み合わせる

### 4.2.5 グラフサイズの調整（縦横比）

グラフのサイズと縦横比は、見やすさと美しさに大きく影響します：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y = np.sin(np.radians(x))

# 異なる縦横比でグラフを作成
# 1. 標準サイズ（デフォルト）
fig1, ax1 = plt.subplots()
ax1.plot(x, y)
ax1.set_title('Default Size')

# 2. 黄金比（1:1.618）
fig2, ax2 = plt.subplots(figsize=(8, 5))  # 近似的な黄金比
ax2.plot(x, y)
ax2.set_title('Golden Ratio (1:1.618)')

# 3. 白銀比（1:1.414）
fig3, ax3 = plt.subplots(figsize=(7, 5))  # 近似的な白銀比
ax3.plot(x, y)
ax3.set_title('Silver Ratio (1:1.414)')

# 4. 正方形（1:1）
fig4, ax4 = plt.subplots(figsize=(5, 5))
ax4.plot(x, y)
ax4.set_title('Square (1:1)')

plt.show()
```

論文によく使われる縦横比：
- 黄金比（1:1.618）：欧米の出版物で好まれる
- 白銀比（1:1.414）：日本の出版物で好まれる
- 正方形（1:1）：データの分布が等方的な場合に適している

### 4.2.6 線の太さ・スタイル・色の調整

グラフの見やすさと美しさは、線の太さ、スタイル、色の選択にも左右されます：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y1 = np.sin(np.radians(x))
y2 = np.cos(np.radians(x))

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))

# 線のスタイル調整
ax.plot(x, y1, 
        color='#1f77b4',  # ヘックスカラーコード
        linewidth=1.5,    # 線の太さ
        linestyle='-',    # 実線
        label='sin(x)')

ax.plot(x, y2, 
        color='#ff7f0e',  # オレンジ
        linewidth=1.5,    # 同じ太さで統一感
        linestyle='--',   # 破線
        label='cos(x)')

# 軸と背景の調整
ax.set_facecolor('none')  # 背景を透明に
ax.spines['top'].set_linewidth(1.5)    # 上の軸線
ax.spines['right'].set_linewidth(1.5)  # 右の軸線
ax.spines['bottom'].set_linewidth(1.5) # 下の軸線
ax.spines['left'].set_linewidth(1.5)   # 左の軸線

# 軸ラベルと凡例
ax.set_xlabel('Angle [degree]')
ax.set_ylabel('Amplitude [-]')
ax.legend(frameon=False)

# 目盛線の調整
ax.tick_params(which='major', width=1.5, length=5)
ax.tick_params(which='minor', width=1.0, length=3)
ax.minorticks_on()

plt.show()
```

色の選択ガイドライン：
- 色覚多様性に配慮する（赤と緑の組み合わせは避ける）
- 印刷したときにも区別できる色を選ぶ
- カラーパレットツールを使用する（例：ColorBrewer）
- matplotlibのデフォルトカラーサイクルは比較的良い選択肢

### 4.2.7 解像度（dpi）設定

特に論文投稿用のグラフは、高解像度が要求されることが多いです：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y = np.sin(np.radians(x))

# 高解像度のグラフを作成
fig, ax = plt.subplots(figsize=(8, 5), dpi=300)  # 300 dpi（論文品質）
ax.plot(x, y)
ax.set_xlabel('Angle [degree]')
ax.set_ylabel('Amplitude [-]')
ax.set_title('High Resolution Plot')

plt.show()

# 画像として保存（高解像度）
fig.savefig('high_res_plot.png', dpi=300, bbox_inches='tight')
fig.savefig('high_res_plot.pdf', bbox_inches='tight')  # PDFは解像度に依存しない
```

解像度の目安：
- 画面表示用：72-96 dpi
- 一般的な印刷用：150-200 dpi
- 論文投稿用：300 dpi以上
- ポスター用：600 dpi以上

### 4.2.8 目盛線の方向と太さの調整

論文品質のグラフでは、目盛線の方向や太さも重要です：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y = np.sin(np.radians(x))

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))
ax.plot(x, y)

# 目盛線の調整
ax.tick_params(which='major',  # 主目盛
               direction='in',  # 内向き（論文スタイル）
               length=6,        # 長さ
               width=1.5,       # 太さ
               colors='black')  # 色

ax.tick_params(which='minor',  # 補助目盛
               direction='in', 
               length=3, 
               width=1.0, 
               colors='black')

# 補助目盛の表示
ax.minorticks_on()

# 上下左右すべての軸に目盛線を表示（論文スタイル）
ax.tick_params(top=True, right=True)

plt.show()
```

目盛線の方向：
- `direction='in'`：内向き（論文に推奨）
- `direction='out'`：外向き（デフォルト）
- `direction='inout'`：内外両方向

### 4.2.9 グラフの保存方法

作成したグラフを様々な形式で保存する方法：

```python
import matplotlib.pyplot as plt
import numpy as np

# データの準備
x = np.linspace(0, 360, 100)
y = np.sin(np.radians(x))

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5), dpi=300)
ax.plot(x, y)
ax.set_xlabel('Angle [degree]')
ax.set_ylabel('Amplitude [-]')
ax.set_title('Sine Wave')
ax.grid(True)

# 様々な形式で保存
formats = ['png', 'pdf', 'svg', 'eps', 'jpg', 'tif']
for fmt in formats:
    fig.savefig(f'sine_wave.{fmt}', 
                dpi=300,              # 解像度（PDFやSVGは影響なし）
                bbox_inches='tight',  # 余白を最小化
                transparent=True)     # 背景を透明に
```

ファイル形式の選択ガイド：
- **PNG**：ウェブや画面表示用、背景透過可能
- **PDF**：論文投稿用、ベクター形式で高品質
- **SVG**：ウェブ用ベクター形式、編集可能
- **EPS**：出版用、一部の雑誌で要求される
- **TIFF**：印刷出版用、高品質な画像形式

## 4.3 演習問題

### 演習問題1：サンプルデータを使った基本グラフ

1. 以下のコードを実行して、SineCurve.txtとCosineCurve.txtのデータを読み込み、一つのグラフにプロットしてください：

```python
import pandas as pd
import matplotlib.pyplot as plt

# データ読み込み
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])

# ここにプロットコードを追加
```

2. 上記のグラフに以下の体裁を整えてください：
   - X軸の範囲：0から360度
   - Y軸の範囲：-1.2から1.2
   - X軸ラベル：「Angle [degree]」
   - Y軸ラベル：「Amplitude [-]」
   - タイトル：「Sine and Cosine Waves」
   - SineCurveは青い実線、CosineCurveは赤い破線
   - 凡例を左下に配置
   - フォントをArialに設定
   - 内向きの目盛線

### 演習問題2：論文品質のグラフ作成

1. 以下のデータをプロットし、論文品質のグラフを作成してください：
   - SineCurve.txt、CosineCurve.txt、plot.txt（散布図として）
   - 縦横比：白銀比（1:1.414）
   - 解像度：300 dpi
   - 軸の太さ：1.5 pt
   - 線の太さ：1.5 pt
   - フォント：Arial、サイズ14 pt
   - 補助目盛あり
   - グリッド線あり（薄い灰色）

2. 作成したグラフをPDFとPNG形式で保存してください。

### 演習問題3：複数のサブプロットを含むグラフ

1. 3つのサブプロットを含む図を作成してください：
   - 上段：SineCurveのプロット
   - 中段：CosineCurveのプロット
   - 下段：SineCurveとCosineCurveの2乗和（理論上は常に1）

2. 各サブプロットに適切な軸ラベルとタイトルを付けてください。

3. 全体のスタイルを論文品質に整えてください。

## 解答例

### 演習問題1の解答

```python
import pandas as pd
import matplotlib.pyplot as plt

# データ読み込み
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])

# フォント設定
plt.rcParams["font.family"] = "Arial"
plt.rcParams["font.size"] = 12

# グラフの作成
fig, ax = plt.subplots(figsize=(8, 5))

# データのプロット
ax.plot(df_sine["X"], df_sine["Y"], 
        color='blue', linestyle='-', linewidth=1.5, 
        label='Sine')
ax.plot(df_cosine["X"], df_cosine["Y"], 
        color='red', linestyle='--', linewidth=1.5, 
        label='Cosine')

# 軸の範囲設定
ax.set_xlim(0, 360)
ax.set_ylim(-1.2, 1.2)

# 軸ラベルとタイトル
ax.set_xlabel('Angle [degree]')
ax.set_ylabel('Amplitude [-]')
ax.set_title('Sine and Cosine Waves')

# 凡例
ax.legend(loc='lower left', frameon=False)

# 目盛線の設定
ax.minorticks_on()
ax.tick_params(which='both', direction='in')
ax.tick_params(top=True, right=True)

# グリッド線
ax.grid(True, alpha=0.5)

plt.show()
```

### 演習問題2の解答

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# データ読み込み
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])
df_points = pd.read_table("plot.txt", names=["X", "Y"])

# フォント設定
plt.rcParams["font.family"] = "Arial"
plt.rcParams["font.size"] = 14

# グラフの作成（白銀比、高解像度）
fig, ax = plt.subplots(figsize=(7, 5), dpi=300)

# データのプロット
ax.plot(df_sine["X"], df_sine["Y"], 
        color='#1f77b4', linestyle='-', linewidth=1.5, 
        label='Sine')
ax.plot(df_cosine["X"], df_cosine["Y"], 
        color='#ff7f0e', linestyle='--', linewidth=1.5, 
        label='Cosine')
ax.scatter(df_points["X"], df_points["Y"], 
           color='#2ca02c', marker='o', s=50, 
           label='Experimental')

# 軸の範囲設定
ax.set_xlim(0, 360)
ax.set_ylim(-1.2, 1.2)

# 軸ラベルとタイトル
ax.set_xlabel('Angle [degree]')
ax.set_ylabel('Amplitude [-]')
ax.set_title('Comparison of Theoretical and Experimental Data')

# 凡例
ax.legend(loc='lower left', frameon=False)

# 目盛線の設定
ax.minorticks_on()
ax.tick_params(which='major', direction='in', length=6, width=1.5)
ax.tick_params(which='minor', direction='in', length=3, width=1.0)
ax.tick_params(top=True, right=True)

# 軸の太さ設定
for spine in ax.spines.values():
    spine.set_linewidth(1.5)

# グリッド線
ax.grid(True, color='gray', alpha=0.3)

# グラフを保存
plt.savefig('theoretical_and_experimental.pdf', bbox_inches='tight')
plt.savefig('theoretical_and_experimental.png', bbox_inches='tight')

plt.show()
```

### 演習問題3の解答

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# データ読み込み
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])

# 2乗和の計算
sum_of_squares = pd.DataFrame({
    'X': df_sine['X'],
    'Y': df_sine['Y']**2 + df_cosine['Y']**2
})

# フォント設定
plt.rcParams["font.family"] = "Arial"
plt.rcParams["font.size"] = 12

# 複数のサブプロットを作成
fig, (ax1, ax2, ax3) = plt.subplots(3, 1, figsize=(8, 10), dpi=300, sharex=True)

# 1つ目のサブプロット（正弦波）
ax1.plot(df_sine["X"], df_sine["Y"], 
         color='blue', linewidth=1.5)
ax1.set_ylabel('sin(x) [-]')
ax1.set_title('Sine Wave')
ax1.set_ylim(-1.2, 1.2)
ax1.grid(True, alpha=0.5)
ax1.minorticks_on()
ax1.tick_params(which='both', direction='in')
ax1.tick_params(top=True, right=True)

# 2つ目のサブプロット（余弦波）
ax2.plot(df_cosine["X"], df_cosine["Y"], 
         color='red', linewidth=1.5)
ax2.set_ylabel('cos(x) [-]')
ax2.set_title('Cosine Wave')
ax2.set_ylim(-1.2, 1.2)
ax2.grid(True, alpha=0.5)
ax2.minorticks_on()
ax2.tick_params(which='both', direction='in')
ax2.tick_params(top=True, right=True)

# 3つ目のサブプロット（2乗和）
ax3.plot(sum_of_squares["X"], sum_of_squares["Y"], 
         color='green', linewidth=1.5)
ax3.axhline(y=1, color='black', linestyle='--', alpha=0.7)
ax3.set_xlabel('Angle [degree]')
ax3.set_ylabel('sin²(x) + cos²(x) [-]')
ax3.set_title('Sum of Squares')
ax3.set_xlim(0, 360)
ax3.set_ylim(0.9, 1.1)
ax3.grid(True, alpha=0.5)
ax3.minorticks_on()
ax3.tick_params(which='both', direction='in')
ax3.tick_params(top=True, right=True)

# レイアウトの調整
plt.tight_layout()

# グラフを保存
plt.savefig('multiple_subplots.pdf', bbox_inches='tight')
plt.savefig('multiple_subplots.png', bbox_inches='tight')

plt.show()
```

## 総括

この第4部では、matplotlibを使った基本的なグラフ描画から、論文品質のグラフを作成するための細かな設定方法まで学びました。実践的な演習を通じて、以下のスキルを身につけることができました：

1. 基本的な折れ線グラフと散布図の作成
2. pandasデータフレームからのグラフ描画
3. 軸ラベル、タイトル、凡例の設定
4. フォント、色、線のスタイルなどの調整
5. 適切な解像度と縦横比の設定
6. 論文品質のグラフを保存する方法

これらのスキルを組み合わせることで、研究データを効果的に可視化し、論文やプレゼンテーションで使える高品質なグラフを作成することができます。

## 発展的な内容

さらに高度なグラフ作成に興味がある方は、以下のトピックも探索してみてください：

1. 複数の軸を持つグラフ（twinx, twiny）
2. 3Dプロット
3. ヒートマップやコンター図
4. カラーマップの適切な選択
5. アニメーションの作成
6. seabornやplotlyなどの高水準ライブラリ

matplotlibの公式ギャラリーには、様々なタイプのグラフの例とコードが掲載されているので参考にしてください：
https://matplotlib.org/stable/gallery/index.html
