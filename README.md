# car_price_prediction
Signate主催の中古車価格予測コンペのリポジトリ

```
.
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
