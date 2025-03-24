# 第3部：データの読み取りとpandasの基本

## 3.1 pandasの導入

### 3.1.1 pandasとは何か

pandasは、Pythonでデータ分析を行うための強力なライブラリです。Excel のスプレッドシートのようなデータ構造（「データフレーム」と呼ばれる）を扱うことができ、実験データの読み込み、整理、分析、可視化を簡単に行うことができます。

### 3.1.2 データフレームの概念

pandasの中心的なデータ構造は「DataFrame（データフレーム）」です。これは表形式のデータを扱うためのもので、以下の特徴があります：

- 行と列で構成された2次元のデータ構造
- 各列には名前（ラベル）がつく
- 異なる型のデータ（数値、文字列など）を混在させることができる
- エクセルのスプレッドシートや SQLのテーブルのようなイメージ

### 3.1.3 実験データ処理におけるpandasの利点

1. **多様なデータ形式のサポート**：テキストファイル（CSV, TSV）、Excel、SQLデータベースなど様々な形式のデータを読み込める
2. **直感的なデータ操作**：データのフィルタリング、ソート、グループ化などが簡単
3. **欠損値の処理**：実験データによくある欠損値の処理に強い
4. **統計計算の容易さ**：平均、標準偏差などの統計量を簡単に計算できる
5. **Matplotlibとの連携**：データフレームから直接グラフを作成できる

## 3.2 データ読み込み

### 3.2.1 pandasのインポート

```python
import pandas as pd
```

### 3.2.2 テキストファイル（CSV/TSV）の読み込み

CSVファイル（Comma-Separated Values）やTSVファイル（Tab-Separated Values）を読み込む方法：

```python
# CSVファイルの読み込み
df_csv = pd.read_csv('data.csv')

# TSVファイルの読み込み
df_tsv = pd.read_table('data.txt')

# 区切り文字を指定して読み込み
df_custom = pd.read_csv('data.txt', sep=';')  # セミコロン区切りの場合
```

### 3.2.3 列名の指定方法

データファイルに列名がない場合、`names`引数で列名を指定できます：

```python
# 列名を指定して読み込み
df = pd.read_csv('data.txt', names=['Time', 'Temperature', 'Pressure'])
```

列名がある場合は、`header`引数で何行目が列名かを指定できます（デフォルトは0行目）：

```python
# 1行目を列名として使用
df = pd.read_csv('data.csv', header=0)

# 列名を使用しない（自動的に0, 1, 2...が列名になる）
df = pd.read_csv('data.csv', header=None)
```

### 3.2.4 実習例：SineCurve.txtを読み込む

先ほどの研修資料で使用していた`SineCurve.txt`を読み込んでみましょう：

```python
# SineCurve.txtの読み込み
df = pd.read_table('SineCurve.txt', names=['X', 'Y'])
print(df.head())  # 最初の5行を表示
```

実行結果（例）：
```
     X         Y
0  0.0  0.000000
1  1.0  0.017452
2  2.0  0.034899
3  3.0  0.052336
4  4.0  0.069756
```

### 3.2.5 読み込んだデータの確認方法

データを読み込んだ後、中身を確認する方法はいくつかあります：

```python
# 最初の5行を表示
print(df.head())

# 最後の5行を表示
print(df.tail())

# データフレームの構造情報を表示
print(df.info())

# 基本的な統計情報を表示
print(df.describe())

# 行数と列数を確認
print(f"行数: {len(df)}, 列数: {df.shape[1]}")
```

### 3.2.6 異なるディレクトリにあるファイルの読み込み方法

作業ディレクトリ以外の場所にあるファイルを読み込む場合、パスを指定する必要があります：

```python
# 絶対パス（Windowsの場合）
df = pd.read_csv('C:/Users/username/Documents/data.csv')

# 絶対パス（Macの場合）
df = pd.read_csv('/Users/username/Documents/data.csv')

# 相対パス（サブディレクトリ）
df = pd.read_csv('./data/data.csv')

# 相対パス（親ディレクトリ）
df = pd.read_csv('../data/data.csv')
```

**注意点**：
- Windowsのパス区切りは「\」ですが、Pythonでは「/」または「\\」（バックスラッシュを2つ）を使います
- パスに日本語が含まれていると問題が起きることがあります
- パスを指定する際は、「r'パス'」（raw文字列）を使うと便利です：
  ```python
  df = pd.read_csv(r'C:\Users\username\Documents\data.csv')
  ```

## 3.3 簡単なデータ操作

### 3.3.1 列の選択

データフレームから特定の列を選択する方法：

```python
# 単一の列を選択（Seriesオブジェクトとして取得）
x_values = df['X']
print(type(x_values))  # <class 'pandas.core.series.Series'>
print(x_values.head())

# 複数の列を選択（DataFrameオブジェクトとして取得）
subset = df[['X', 'Y']]
print(type(subset))  # <class 'pandas.core.frame.DataFrame'>
print(subset.head())
```

### 3.3.2 基本的なフィルタリング

条件に合う行だけを抽出する方法：

```python
# X列が180以上の行を抽出
df_filtered = df[df['X'] >= 180]
print(df_filtered.head())

# 複数条件の組み合わせ（AND条件）
df_range = df[(df['X'] >= 90) & (df['X'] <= 180)]
print(df_range.head())

# 複数条件の組み合わせ（OR条件）
df_either = df[(df['X'] < 10) | (df['X'] > 350)]
print(df_either.head())
```

**注意点**：
- 条件式では、Pythonの通常の論理演算子（`and`, `or`）ではなく、`&`や`|`を使います
- 各条件は括弧でくくる必要があります

### 3.3.3 簡単な統計量の計算

データフレームやSeriesの統計量を計算する方法：

```python
# 基本的な統計量
print(f"Xの平均値: {df['X'].mean()}")
print(f"Yの平均値: {df['Y'].mean()}")
print(f"Xの最大値: {df['X'].max()}")
print(f"Yの最小値: {df['Y'].min()}")
print(f"Yの標準偏差: {df['Y'].std()}")

# 特定の範囲のデータに対する統計量
df_range = df[(df['X'] >= 90) & (df['X'] <= 180)]
print(f"90°～180°の範囲におけるYの平均値: {df_range['Y'].mean()}")
```

### 3.3.4 データの変換

新しい列を追加する方法：

```python
# 既存の列から新しい列を計算
df['Y_squared'] = df['Y'] ** 2
print(df.head())

# ラジアンから度に変換（X列がラジアンの場合）
df['X_degrees'] = df['X'] * 180 / 3.14159
print(df.head())

# 関数を適用
import numpy as np
df['sin_2x'] = np.sin(2 * df['X'])
print(df.head())
```

### 3.3.5 実践例：複数のデータセットを読み込んで処理

研修資料で使用されていた複数のファイルを読み込んで処理する例：

```python
import pandas as pd
import matplotlib.pyplot as plt

# 複数のファイルを読み込む
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])
df_points = pd.read_table("plot.txt", names=["X", "Y"])

# データの確認
print("SineCurve.txt の先頭5行:")
print(df_sine.head())
print("\nCosineCurve.txt の先頭5行:")
print(df_cosine.head())
print("\nplot.txt の先頭5行:")
print(df_points.head())

# 各データセットの基本統計量
print("\nSineCurve.txt の統計量:")
print(df_sine.describe())
print("\nCosineCurve.txt の統計量:")
print(df_cosine.describe())
print("\nplot.txt の統計量:")
print(df_points.describe())

# グラフで可視化
plt.figure(figsize=(10, 6))
plt.plot(df_sine["X"], df_sine["Y"], label="Sine")
plt.plot(df_cosine["X"], df_cosine["Y"], label="Cosine")
plt.scatter(df_points["X"], df_points["Y"], color="red", label="Points")
plt.xlabel("X")
plt.ylabel("Y")
plt.title("Multiple Datasets")
plt.legend()
plt.grid(True)
plt.show()
```

## 3.4 練習問題

### 練習問題1：データの読み込みと基本操作

1. `SineCurve.txt`ファイルを読み込み、以下の情報を表示してください：
   - 最初の10行
   - データの行数と列数
   - X列とY列の平均値、最大値、最小値

2. X列の値が以下の条件に合うデータのみを表示してください：
   - 0度から90度まで
   - 180度から270度まで
   - 0度から360度までを30度刻みで

### 練習問題2：データの変換と新しい列の追加

1. `SineCurve.txt`を読み込み、以下の新しい列を追加してください：
   - `Y_squared`: Y値の2乗
   - `Y_abs`: Y値の絶対値

2. X列とY列の相関係数を計算してください。

### 練習問題3：複数データセットの操作

1. `SineCurve.txt`と`CosineCurve.txt`を読み込み、以下を計算してください：
   - 各X値に対するsin(x)とcos(x)の2乗和（理論上は常に1になるはず）
   - X値が0から360までの範囲で、Y値の絶対値が0.5以上になるデータ点の割合

2. 結果をグラフで可視化してください。

## 解答例

### 練習問題1の解答

```python
import pandas as pd

# 1. SineCurve.txtの読み込みと基本情報
df = pd.read_table("SineCurve.txt", names=["X", "Y"])

# 最初の10行を表示
print("最初の10行:")
print(df.head(10))

# データの行数と列数
rows, cols = df.shape
print(f"\nデータの行数: {rows}, 列数: {cols}")

# 統計情報
print("\nX列の統計情報:")
print(f"平均値: {df['X'].mean()}")
print(f"最大値: {df['X'].max()}")
print(f"最小値: {df['X'].min()}")

print("\nY列の統計情報:")
print(f"平均値: {df['Y'].mean()}")
print(f"最大値: {df['Y'].max()}")
print(f"最小値: {df['Y'].min()}")

# 2. 条件に合うデータの表示
print("\n0度から90度までのデータ:")
print(df[(df['X'] >= 0) & (df['X'] <= 90)])

print("\n180度から270度までのデータ:")
print(df[(df['X'] >= 180) & (df['X'] <= 270)])

# 0度から360度までを30度刻み
step = 30
selected_rows = df[df['X'] % step == 0]
print("\n0度から360度までを30度刻みでサンプリング:")
print(selected_rows)
```

### 練習問題2の解答

```python
import pandas as pd

# SineCurve.txtの読み込み
df = pd.read_table("SineCurve.txt", names=["X", "Y"])

# 新しい列の追加
df['Y_squared'] = df['Y'] ** 2
df['Y_abs'] = df['Y'].abs()

# 結果の確認
print("新しい列を追加したデータフレーム:")
print(df.head())

# 相関係数の計算
correlation = df['X'].corr(df['Y'])
print(f"\nX列とY列の相関係数: {correlation}")
```

### 練習問題3の解答

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

# データ読み込み
df_sine = pd.read_table("SineCurve.txt", names=["X", "Y"])
df_cosine = pd.read_table("CosineCurve.txt", names=["X", "Y"])

# 同じX値を持つことを確認
if df_sine['X'].equals(df_cosine['X']):
    # 新しいデータフレームを作成
    df_combined = pd.DataFrame()
    df_combined['X'] = df_sine['X']
    df_combined['sin_x'] = df_sine['Y']
    df_combined['cos_x'] = df_cosine['Y']
    
    # sin^2(x) + cos^2(x)を計算
    df_combined['sin2_plus_cos2'] = df_combined['sin_x']**2 + df_combined['cos_x']**2
    
    print("sin^2(x) + cos^2(x)の計算結果:")
    print(df_combined.head())
    
    # 統計量
    print("\nsin^2(x) + cos^2(x)の統計量:")
    print(df_combined['sin2_plus_cos2'].describe())
    
    # Y値の絶対値が0.5以上になるデータ点の割合を計算
    df_sine_filtered = df_sine[(df_sine['X'] >= 0) & (df_sine['X'] <= 360)]
    total_points = len(df_sine_filtered)
    points_above_threshold = len(df_sine_filtered[df_sine_filtered['Y'].abs() >= 0.5])
    
    percentage = (points_above_threshold / total_points) * 100
    print(f"\n|Y| >= 0.5 となるデータ点の割合: {percentage:.2f}%")
    
    # グラフで可視化
    plt.figure(figsize=(12, 8))
    
    # サブプロット1: sin(x)とcos(x)
    plt.subplot(2, 1, 1)
    plt.plot(df_combined['X'], df_combined['sin_x'], label='sin(x)')
    plt.plot(df_combined['X'], df_combined['cos_x'], label='cos(x)')
    plt.xlabel('X')
    plt.ylabel('Value')
    plt.title('sin(x) and cos(x)')
    plt.legend()
    plt.grid(True)
    
    # サブプロット2: sin^2(x) + cos^2(x)
    plt.subplot(2, 1, 2)
    plt.plot(df_combined['X'], df_combined['sin2_plus_cos2'], 'r-')
    plt.axhline(y=1, color='k', linestyle='--')
    plt.xlabel('X')
    plt.ylabel('sin^2(x) + cos^2(x)')
    plt.title('Verification of sin^2(x) + cos^2(x) = 1')
    plt.grid(True)
    
    plt.tight_layout()
    plt.show()
else:
    print("SineCurve.txtとCosineCurve.txtのX値が一致しません。")
```

## 次のステップ

これでデータの読み取りとpandasの基本操作について学びました。次の第4部では、matplotlibを使ったグラフの作成と、論文品質のグラフを作るための体裁整備について詳しく学びます。
