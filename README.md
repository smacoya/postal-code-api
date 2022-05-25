# 郵便番号 API

この郵便番号APIはmadefor様により作成されたレポジトリを引き継いだものになります。

GitHubページを使用して静的なファイルで配信しているため信頼性が高く、さらにオープンソースなのでクライアントワークでも安心して使用できます。

また、郵便番号から英語の住所を取得することも可能です。（大口事業所個別番号は英語には対応していません。）

なお、このAPIはGitHub Actionsを使用して毎日更新しています。

## デモ
https://arrow-payment.github.io/postal-code-api/

## エンドポイント

```
https://arrow-payment.github.io/postal-code-api/api/v2/
```

## 使い方

郵便番号が`100-0014`(東京都千代田区永田町)の住所を取得したい場合。

https://arrow-payment.github.io/postal-code-api/api/v2/100/0014.json

```json
{
  "code":"1000014",
  "data":[
    {
      "prefcode":"13",
      "ja":{
        "prefecture":"東京都",
        "address1":"千代田区",
        "address2":"永田町",
        "address3":"",
        "address4":""
      },
      "ja_kana":{
        "prefecture":"ﾄｳｷｮｳﾄ",
        "address1":"ﾁﾖﾀﾞｸ",
        "address2":"ﾅｶﾞﾀﾁｮｳ",
        "address3":"",
        "address4":""
      },
      "en":{
        "prefecture":"Tokyo",
        "address1":"Chiyoda-ku",
        "address2":"Nagatacho",
        "address3":"",
        "address4":""
      }
    }
  ]
}
```

1つの郵便番号に複数の住所がある場合は以下のような感じです。

https://arrow-payment.github.io/postal-code-api/api/v2/618/0000.json

```json
{
  "code":"6180000",
  "data":[
    {
      "prefcode":"26",
      "ja":{
        "prefecture":"京都府",
        "address1":"乙訓郡大山崎町",
        "address2":"",
        "address3":"",
        "address4":""
      },
      "ja_kana":{
        "prefecture":"ｷｮｳﾄﾌ",
        "address1":"ｵﾄｸﾆｸﾞﾝｵｵﾔﾏｻﾞｷﾁｮｳ",
        "address2":"",
        "address3":"",
        "address4":""
      },
      "en":{
        "prefecture":"Kyoto",
        "address1":"Oyamazaki-cho, Otokuni-gun",
        "address2":"",
        "address3":"",
        "address4":""
      }
    },
    {
      "prefcode":"27",
      "ja":{
        "prefecture":"大阪府",
        "address1":"三島郡島本町",
        "address2":"",
        "address3":"",
        "address4":""
      },
      "ja_kana":{
        "prefecture":"ｵｵｻｶﾌ",
        "address1":"ﾐｼﾏｸﾞﾝｼﾏﾓﾄﾁｮｳ",
        "address2":"",
        "address3":"",
        "address4":""
      },
      "en":{
        "prefecture":"Osaka",
        "address1":"Shimamoto-cho, Mishima-gun",
        "address2":"",
        "address3":"",
        "address4":""
      }
    }
  ]
}
```

大口事業所個別番号では英語の事業所名は空になっています。
また、番地の読み仮名は提供されないため空欄になっています。

https://arrow-payment.github.io/postal-code-api/api/v2/100/8791.json

```json
{
  "code":"1008791",
  "data":[
    {
      "prefcode":"13",
      "ja":{
        "prefecture":"東京都",
        "address1":"千代田区",
        "address2":"大手町",
        "address3":"２－３－１",
        "address4":"日本郵政　株式会社"
      },
      "ja_kana":{
        "prefecture":"ﾄｳｷｮｳﾄ",
        "address1":"ﾁﾖﾀﾞｸ",
        "address2":"ｵｵﾃﾏﾁ",
        "address3":"",
        "address4":"ﾆﾂﾎﾟﾝﾕｳｾｲ ｶﾌﾞｼｷｶﾞｲｼﾔ"
      },
      "en":{
        "prefecture":"Tokyo",
        "address1":"Chiyoda-ku",
        "address2":"Otemachi",
        "address3":"",
        "address4":""
      }
    }
  ]
}
```

## 仕様

* 大口事業所個別番号データは英語には対応していません。
* Gulpタスクで以下の処理を行っています。
  1. [日本郵便のウェブサイト](http://www.post.japanpost.jp/zipcode/)から[郵便番号データ](https://www.post.japanpost.jp/zipcode/dl/kogaki-zip.html)をダウンロード。
  2. ダウンロードしたファイルを解凍して、取り出したCSVをパース。
  3. 郵便番号の上3桁の名前を持つディレクトリを作り、その中に下4桁の名前を持つJSONを作成。
* GitHub Actionsを使用して毎日更新しています
* 互換性維持のため、v1も引き続きメンテナンスされますが以下の理由のためv2への移行を推奨します
  * v1のデータソースであるローマ字表記CSVデータは年に1回程度しか更新されません
  * v1には読み仮名が含まれません

## ローカルでJSONデータを作成する

このリポジトリをcloneしてください。

```
$ git@github.com:arrow-payment/postal-code-api.git
```

必要なモジュールをインストールしてください。

```
$ cd postal-code-api
$ npm install
```

以下のコマンドでAPIを生成してください。

```
$ npm run build
```

ローカルでAPIを動かしたい場合には以下のコマンドを実行してください。

```
$ npm start
```

## 貢献

* バグレポートは[Issue](https://github.com/arrow-payment/postal-code-api/issues)にお願いします。
* プルリクエストは大歓迎です。
* Starをつけてもらうと開発者たちのモチベーションが上がります。
* ぜひオリジナルのレポジトリ(madefor/postal-code-api)のほうにもStarをお願いします

## ライセンス

MIT
(弊社変更部分についてはPublic Domainとします。madefor様のライセンス表記は引き続き必要です)
