# SIGNATE Cup 2024

[SIGNATE Cup 2024](https://signate.jp/competitions/1376) の184th place solution です。

## 概要

- 方針
    - 以下の結果から、オッカムの剃刀に従って極力シンプルなモデルを作ることにした。
        - CVとLBがまったく相関しなかった。
        - LightGBMやCatBoostを試したところ、過学習をかなり強く防ぐようなハイパラ設定にするとCV・LB共に向上した。
- 説明変数
    - 元データの各カラムをデータクレンジングしたもの
    - タイポフラグ
    - 欠損フラグ
- 説明変数の前処理
    - `Age` `DurationOfPitch` `MonthlyIncome` を数値変数、それ以外をカテゴリー変数をみなした。
    - 数値変数は正規化と欠損値補完 (`IterativeImputer`) を、カテゴリー変数はダミー変数化をそれぞれ施した。
    - L1正則化で絞り込んだ後、CVを見ながら手作業で変数を選択した。
- モデル
    - ロジスティック回帰モデル
- モデル選択
    - `StratifiedShuffleSplit(n_splits=100, test_size=0.5)`
- アンサンブル
    - なし
- スコア
    - CV: 0.8472193
    - Public LB: 0.8391560
    - Private LB: 0.8388465 (184位)

## コード

- [20240901_04.ipynb](/20240901_04.ipynb)
