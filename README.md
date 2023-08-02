# car_price_prediction
Signate主催の中古車価格予測コンペのリポジトリ

```
.
├── READEME.md
├── .gitignore
├── data
│   ├── submit_sample.csv
│   └── test.csv
│   └── train.csv
├── etc
├── lib
├── scripts
│   ├── EDA.ipynb
│   └── 2023xxxx_xxx_xxxx.ipynb
├──submit-file
│   ├── 2023xxxx_submission.csv
```

## Log
### 2023/07/29
■EDAの実施
ファイル:
scripts/EDA.ipynb

アプローチ方法の検討：
- 数値変数の外れ値を整形して精度がどれくらいがあるか
  - issue参照
- カテゴリ変数をクレンジングして、精度がどれくらい上がるか
  - issue参照
- 比較的、priceと相関がありそうな項目を全て特徴に入れて予測モデルを構築すると精度はどうか
  - odometer, region, state, manufacture, size, condition 
- 製造メーカの各値のデータ量に偏りがあるので、メーカごとに予測モデルを構築してはどうか
   -　データ量が少ないものは平均値で出すのはどうか
- pycaretを利用して適切なモデルを確認してみる
- 販売店（データとしては持ってないので考える必要はある）ごとに価格の算出式があるのではないか
  - 走行距離などからベースの価格を出して状態によって減算しているとか
  - 規則性の調査が必要

### 2023/07/30
■前処理の工夫
- cconditionカラムを確認すると新車（new）のデータがあるように見えたので対象データを削除
  - レコードを削除するとファイル投稿時にエラーになるので修正
  - そもそも中古車販売店でも新車が売られているのあり得るので他の値と同様にダミー変数化する
- 数値変数の外れ値を整形して精度がどれくらいがあるか
  - odometerとyearのみの特徴ではデータ整形後も予測精度は上がらない（yearがpriceと相関がない）

■予測結果
- ファイル：data_preprocessing_analysis
- 特徴に使用したカラム
  - odometer
  - condition
  - manufacturer
  - size
  - state
  - region
- シンプルな前処理を行ったのみ
- 精度：	71.3387451

### 2023/08/02
- 前処理の部分をモジュール化
- stateの欠損値をちゃんと埋めたい。。
- 前処理のアプローチをもう少しやってみる

### 2023/08/03
- sizeの値も揃ってなかったので、整形
- typeは人気度によってpriceに影響してきそう（特徴量として人気度を足すのはいいかも）  
