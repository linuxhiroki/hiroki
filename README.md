# 4年生研修用資料(python講習会)　２０２５版

# Python研修：データ分析とグラフ描画

本レポジトリは、研究室の新入生向けPython研修（4年生クイズ）の資料およびサンプルコードを提供します。この研修では、Python初学者が実験データの読み込みからグラフ描画までを効率的に学ぶことを目的としています。(その割にはちょっと難しいかも)

*本研修は、生成AIと共同して作られていますので、間違っている可能性が大いにあります。変なところがあったら悩まず、ここおかしいと指摘お願いします。

## 概要

この研修は以下の目的で設計されています：

- Python環境の基本的な操作方法の習得
- 実験データの読み込みと基本的な分析方法の習得
- 論文品質のグラフ作成スキルの習得
- 実践的なデータ可視化技術の学習


## ファイル構成

### 研修資料

1. **`part1.md`**: 第1部：グラフをPythonで作る意義と環境設定
   - Pythonでグラフ作成する利点（再現性・自動化・カスタマイズ性）
   - Anacondaとspyderのインストールと基本設定
   - 基本的なPythonの実行方法

2. **`part2.md`**: 第2部：Pythonの基本操作
   - 変数と基本的な計算
   - リストとNumPy配列の基礎
   - 関数の作成と活用方法
   - import文の使い方

3. **`part3.md`**: 第3部：データの読み取りとpandasの基本
   - pandasを使ったデータ読み込み
   - データフレームの基本操作
   - tkinterを使ったファイル選択ダイアログ
   - 複数データの操作

4. **`part4.md`**: 第4部：matplotlibを用いたグラフ描画
   - 基本的なグラフの作成
   - グラフの体裁整備（フォント・色・線の設定）
   - 論文品質のグラフを作るためのテクニック
   - 関数を活用した効率的なグラフ作成

### サンプルデータ

研修で使用するデータファイルは `data` フォルダに配置されています：

1. **`SineCurve.txt`**
   - 角度（0〜360度）と対応する正弦値
   - タブ区切りの2列データ
   - 基本的な折れ線グラフ作成練習用

2. **`CosineCurve.txt`**
   - 角度（0〜360度）と対応する余弦値
   - タブ区切りの2列データ
   - 複数データの描画練習用

3. **`plot.txt`**
   - 散布図用のX-Y座標データ
   - タブ区切りの2列データ
   - 散布図作成練習用

4. **`experiment.csv`**
   - 時間、温度、圧力などの実験データを模したサンプル
   - カンマ区切りCSV（列名あり）
   - 実際の研究データに近い形式での操作練習用

### 出力フォルダ

研修中に生成したグラフやデータを保存するフォルダです：

- **`output/figures/`**: グラフ保存用フォルダ
- **`output/processed/`**: 処理済みデータ保存用フォルダ

## 使用方法

### 研修の進め方

1. 第1部から順に進めてください。第1部と第2部は事前学習として解いてもらおうと思っています。第3部と第4部は研修当日に実施することをお勧めします。

2. 各部にはコードサンプルと練習問題があります。サンプルコードは自分のエディタにコピペして実行しながら学習を進めてください。

3. わからないことがあったら、周りの先輩に気軽に聞いてください。もちろん、googleやchat gptを使っても大丈夫ですが、解くことが目的じゃないので内容の理解を頑張ってください(自力では解けなそうな問題もいくつか...)。

### 前提条件

- Windows環境（研修はWindows向けに最適化されています）
- Anacondaがインストールされていること(part1でやります)

---

本研修資料は、研究室の実際のニーズに基づいて作成されました。Python初学者が実験データを効率的に処理し、高品質なグラフを作成できるようになることを目指しています。
