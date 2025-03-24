# 第1部：グラフをPythonで作る意義と環境設定

## 1.1 Pythonでグラフを作る意義

研究活動では、実験データの可視化が非常に重要です。従来のExcelなどでもグラフ作成は可能ですが、Pythonを使うことで以下の3つの大きなメリットがあります：

### 1.1.1 再現性
- **一度コードを書けば何度でも同じグラフが作成できる**
  - 実験条件を変えても、同じコードで一貫したスタイルのグラフが作成可能
  - 数か月後に見返したときも、どのようにグラフを作成したかが明確

### 1.1.2 自動化
- **データ処理からグラフ作成までを自動化できる**
  - 新しいデータが得られたら、コードを実行するだけで最新のグラフが生成
  - 複数のデータセットに対して、同じ処理を一度に適用可能

### 1.1.3 カスタマイズ性
- **論文品質のグラフを細部まで調整できる**
  - フォント、サイズ、色、線の太さなど、あらゆる要素を細かく制御
  - 学術誌の要件に合わせた高解像度・高品質のグラフを作成可能

### 目標とするグラフの例

この研修を通じて、以下のような論文品質のグラフ作成を目指します：

![目標とするグラフ例](https://media.githubusercontent.com/media/matplotlib/matplotlib/master/doc/_static/gallery_thumbnails/subplots_gridspec_hspace.png)

*注：実際の研修では、研究室で実際に使用している論文品質のグラフ例を入れることを推奨します*

## 1.2 環境設定

### 1.2.1 Anacondaのインストール

Anacondaは、Python本体と科学計算に必要な多数のライブラリを一括でインストールできるディストリビューションです。

1. [Anacondaの公式サイト](https://www.anaconda.com/products/distribution)にアクセス
2. お使いのOSに合わせたインストーラをダウンロード
3. インストーラを実行し、画面の指示に従ってインストール
   - 特別な理由がない限り、デフォルト設定のままでOK
   - インストール終了後、「Register Anaconda as my default Python」にチェックを入れることを推奨

### 1.2.2 Spyderの起動

Spyderは、科学計算向けの統合開発環境（IDE）です。コード編集、実行、デバッグが一つの画面で行えます。

1. Windowsの場合：スタートメニュー → Anaconda3 → Spyder
2. macOSの場合：Launchpad → Anaconda-Navigator → Spyder
3. または、Anaconda Promptを開き、`spyder`と入力して実行

### 1.2.3 Spyderの基本UI

![Spyderの基本UI](https://docs.spyder-ide.org/current/_images/mainwindow_default_1610.png)

Spyderの画面は主に3つのエリアに分かれています：

1. **エディタペイン**（左側）：コードを書く場所
2. **IPythonコンソール**（右下）：コードの実行結果が表示される場所
3. **プロット表示エリア**（右上）：グラフが表示されるエリア（Plotsタブ）

### 1.2.4 作業ディレクトリの設定

作業ディレクトリとは、コードやデータファイルを置く場所です。適切に設定することで、ファイルのパス指定が簡単になります。

1. デスクトップまたはドキュメントフォルダに「Python_Training」などの新しいフォルダを作成
2. Spyderのメニューから「Tools」→「Preferences」を選択
3. 左側の「Current working directory」を選択
4. 「The following directory:」を選択し、先ほど作成したフォルダを指定
5. 「Apply」→「OK」をクリック

あるいは、簡単な方法として：

1. Spyderの上部にある「Current working directory」欄の横の「Browse」ボタンをクリック
2. 作業フォルダを選択して「Select Folder」をクリック

## 1.3 Spyderの基本操作

### 1.3.1 重要なショートカットキー

| ショートカット | 機能 |
|-------------|------|
| F5 | ファイル全体を実行 |
| Ctrl+Enter | 選択した部分のみ実行 |
| Ctrl+1 | 選択行のコメントアウト/解除 |
| Ctrl+S | ファイルの保存 |
| Ctrl+N | 新規ファイルの作成 |
| F9 | ファイル内の行を実行 |
| Ctrl+Space | コード補完の表示 |

### 1.3.2 ファイルの保存と読み込み

- **保存**: 「File」→「Save」または Ctrl+S
- **読み込み**: 「File」→「Open」または Ctrl+O
- **新規作成**: 「File」→「New File」または Ctrl+N

ファイル名は半角英数字とアンダースコア（_）のみを使い、スペースや日本語は避けましょう。
例：`plot_example.py`

### 1.3.3 エラーメッセージの読み方

エラーが発生すると、コンソールに赤字でエラーメッセージが表示されます。

```
---------------------------------------------------------------------------
FileNotFoundError                         Traceback (most recent call last)
<ipython-input-1-6e5aee5c805e> in <module>
      3 import pandas as pd
      4 
----> 5 df = pd.read_csv("data.csv")

FileNotFoundError: [Errno 2] No such file or directory: 'data.csv'
```

主なエラーメッセージの読み方：

1. 最後の行に簡潔なエラーの種類と理由が書かれています（例：`FileNotFoundError: [Errno 2] No such file or directory: 'data.csv'`）
2. `--->`マークの行がエラーが発生した行です
3. 上から下に向かって実行された順番でトレースバックが表示されます

よくあるエラー：
- `SyntaxError`: 文法エラー（括弧の閉じ忘れなど）
- `NameError`: 未定義の変数を使おうとした
- `FileNotFoundError`: ファイルが見つからない
- `ImportError`: モジュールのインポートに失敗

## 1.4 最初の一歩

### 1.4.1 Hello, World!

新しいファイルを作成し、以下のコードを入力してみましょう：

```python
# 最初のプログラム
print("Hello, World!")
```

F5キーを押して実行すると、コンソールに「Hello, World!」と表示されます。

### 1.4.2 基本的な数値計算

次に、簡単な計算を行ってみましょう：

```python
# 基本的な数値計算
a = 5
b = 3
print(f"a + b = {a + b}")  # 足し算
print(f"a - b = {a - b}")  # 引き算
print(f"a * b = {a * b}")  # 掛け算
print(f"a / b = {a / b}")  # 割り算
print(f"a ** b = {a ** b}")  # べき乗（a^b）
```

### 1.4.3 最初のグラフ描画

最後に、非常に簡単なグラフを描画してみましょう：

```python
# 最初のグラフ描画
import matplotlib.pyplot as plt

# データの準備
x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

# グラフの描画
plt.figure(figsize=(8, 5))  # グラフサイズの指定
plt.plot(x, y, 'ro-')  # 赤い丸と線でプロット
plt.xlabel('x値')  # x軸ラベル
plt.ylabel('y値')  # y軸ラベル
plt.title('y = x^2のグラフ')  # タイトル
plt.grid(True)  # グリッド線表示
plt.show()  # グラフの表示
```

このコードを実行すると、右側のプロットエリアに簡単なグラフが表示されます。

## 1.5 練習問題

1. 以下の数式を計算するコードを書いて実行してください：
   - (5 + 3) × 4 ÷ 2
   - 2の8乗

2. 以下のようなグラフを描画してみましょう：
   - x軸の範囲を0から10まで
   - y = x × sin(x)のグラフ
   - 青い線を使用

**ヒント**: `import numpy as np`を使うと、sin関数などの数学関数や等間隔の数値列が使えます。

## 次のステップ

次の第2部では、Pythonの基本的な文法とデータ構造について学びます。特にグラフ描画に必要な変数、リスト、配列などについて重点的に学習します。
