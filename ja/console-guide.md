## Search > Cloud Search > コンソール使用ガイド

## 注意
- 文書内のホスト名「api-7ab1617e2df0f1d1-search.cloud.toast.com」は、ユーザーごとに異なる場合があります。
- 文書内のアプリケーションキー「EMKPutYozUttWVY2」は、ユーザーごとに異なります。

## 始める
まずCloud Searchサービスを有効化します。

1. **NHN Cloud Console**で**サービス選択**をクリックします。

2. **Cloud Search**をクリックします。

![img](http://static.toastoven.net/prod_search/product-use-02-ja-20210506.jpg)<br>

サービスが有効化されているかを確認する方法は次のとおりです。

1. **NHN Cloud Console**左側メニューで**Search**をクリックします。

2. **Cloud Search**が表示されたらサービスが有効になっているということです。

![img](http://static.toastoven.net/prod_search/product-use-03-ja-20210506.jpg)

## 基本使用方法

### 1. サービスの作成

サービスを作成する方法は次のとおりです。

1. **サービス作成**ボタンをクリックします。

2. **サービス作成**ウィンドウでサービスIDを入力します。

    - 英字小文字、数字およびアンダースコア(_)とハイフン(-)のみ使用できます。
    - 最初の文字に数字、アンダースコア(_)、ハイフン(-)は使用できません。
    - 2文字以上入力する必要があります。

3. **保存**ボタンをクリックします。

![img](http://static.toastoven.net/prod_search/domain_create_prodedure-ja-20210506.jpg)<br>

作成されたサービス結果を確認します。

1. 作成されたサービスID(test)をクリックします。

![img](http://static.toastoven.net/prod_search/domain_create_result-ja-20210506.jpg)


### 2. フィールド設定

フィールドを追加する方法は次のとおりです。

1. **フィールド設定**タブをクリックします。

2. **フィールド追加**ボタンをクリックします。

3. フィールド名を入力します。

    - 英字大文字/小文字、数字およびアンダースコア(_)とハイフン(-)のみ使用できます。
    - 最初の文字に数字、アンダースコア(_)とハイフン(-)は使用できません。
    - 2文字以上入力する必要があります。

4. **保存**ボタンをクリックします。

![img](http://static.toastoven.net/prod_search/field_create_procedure-ja-20200304.jpg)

### 3. インデックス

インデックスするファイルを作成してインデックスする方法は次のとおりです。

**インデックスファイルの作成**

  - 下記例のような形式でインデックスリクエストファイルを作成します。
  - インデックスするファイルはUTF-8で作成する必要があります。
      - Windowsのメモ帳でファイルを保存する時は、エンコードをUTF-8に指定して保存します。
  - 例ではdata/documents.jsonという名前で作成しました。

```
[
  {
    "action": "add",
    "id": "id-1",
    "fields": {
      "title": "[送料無料]ナイキのシューズ195種！",
      "body": "ナイキの人気シューズには売れているワケがあります！ナイキの人気シューズ195種★一足は必要じゃないですか？"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "fields": {
      "title": "[超特価]ナイキの運動靴109種",
      "body": "7日間だけの限定価格！超特価]アディダスシューズ109種！迷っていたら売り切れ必至"
    }
  },
  {
    "action": "add",
    "id": "id-3",
    "fields": {
      "title": "[アディダス]メンズ運動靴/スリッパ114種",
      "body": "[アディダスのシューズ♥]送/料/無/料[アディダス]メンズスリッパ /スーパースター、スタンスミス /チューブラー他114種が手に入るチャンス！"
    }
  }
]
```

* ファイル説明
    * action
        * add :該当文書が追加されます。
            * 既に同じidが存在する場合はアップデートされます。
        * delete :該当文書が削除されます。
    * id
        * 文書の固有IDです。
        * idのタイプは文字列です。
    * 最大ファイルサイズは8Mbです。
        * 8Mb以上のデータは複数に分けてインデックスする必要があります。

**インデックス方法**

1. **インデックス**タブをクリックします。

2. **ファイル選択**ボタンをクリックします。

3. インデックスするファイルを選択します。

4. **開く**ボタンをクリックします。

5. インデックスコマンドがREST APIで出力されます。

    - REST APIを利用して検索サービスを開発してください。

6. **インデックス**ボタンをクリックします。

7. インデックス結果を確認します。

![img](http://static.toastoven.net/prod_search/indexing_procedure_01-ja-20200304.jpg)
![img](http://static.toastoven.net/prod_search/indexing_procedure_02-ja-20200304.jpg)<br>

**REST API**

下記のようにREST APIを使用可能です。

- インデックスAPI
    - Request
        - ファイルアップロード方式
            ```
            curl -XPOST 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing' -H 'Accept-Language:ja' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json'
                ```
        - ペイロード(payload)方式
            ```
            curl -XPOST 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing' -H 'Accept-Language:ja' -H 'Content-Type:application/json; charset=UTF-8' -d '
            [
              {
                "action": "add",
                "id": "id-1",
                "fields": {
                  "title": "[送料無料]ナイキシューズ195種！",
                  "body": "ナイキの人気シューズには売れているワケがあります！ナイキの人気シューズ195種★一足は必要じゃないですか？"
                }
              },
              {
                "action": "add",
                "id": "id-2",
                "fields": {
                  "title": "[超特価]ナイキの運動靴109種",
                  "body": "7日間だけの限定価格！超特価]アディダスシューズ109種！迷っていたら売り切れ必至"
                }
              }
            ]'
            ```
    - Response
        ```
        {
          "id" : 1
        }
        ```
- インデックス結果確認API
    - Request
        ```
        curl -i -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing_log?id=1' -H 'Accept-Language:ja'
        ```
        - id 1は上記のインデックスAPI Responseのidです。
    - Response
        ```
        {
          "request_time" : "2017-10-23T12:36:43",
          "file_name" : "documents.json",
          "file_size" : 1185,
          "status" : 4
        }
        ```
        - status
            - 1 :待機中
            - 2 : 無視された(フィールド設定変更前のインデックスリクエストは無視される)
            - 3 :進行中
            - 4 :成功
            - 5 :失敗

### 4. 検索

検索方法は次のとおりです。

1. **検索**タブをクリックします。

2. 検索するフィールド名をチェックします。

3. 検索するフィールドごとに重みを設定します。

    - 0.0～1.0の値を設定します。

4. 検索結果に出力するフィールドをチェックします。

5. 検索結果の長さを設定します。

6. 強調(highlight) preタグを設定します。

7. 強調(highlight) postタグを設定します。

8. 検索結果で出力する開始順位を指定します。

    - 「1」に設定すると1位から出力され、「10」に設定すると10位から出力されます。

9. 検索結果の数を指定します。

    - 「5」に設定すると5個出力され、「10」に設定すると10個出力されます。

10. 検索演算子を選択します。

11. 検索する単語を入力します。

12. 検索アイコンをクリックします。

13. 2～11番まで設定した内容がREST APIで出力されます。

    - REST APIを利用して検索サービスを開発してください。

14. 検索結果が出力されます。

![img](http://static.toastoven.net/prod_search/basic-search-ja-20200304.jpg)<br>

**REST API**

下記のようにREST APIを使用できます。

- Request
    ```
    curl -G -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/search/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=&passage.body=180&passage.title=180' --data-urlencode q='ナイキ 運動靴' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ja'
    ```
- Response
    ```
    {
      "message" : {
          "meta" : {
            "timezone" : "+09:00"
          },
          "result" : {
            "status" : {
            "code" : 200,
            "message" : "OK"
          },
          "query" : "ナイキ 運動靴",
          "start" : 1,
          "itemCount" : 1,
          "total" : 1,
          "itemList" : {
            "item" : [
            {
              "_RELEVANCE" : 0.07575758,
              "_RANK" : 1,
              "_ID" : "id-2",
              "body" : "7日間だけの限定価格！超特価]アディダスシューズ109種！迷っていたら売り切れ必至",
              "title" : "[超特価]<b>ナイキ</b> <b>運動靴</b> 109種"
            }
            ]
          }
        }
      }
    }
    ```

### 5. 統計

統計を確認する方法は次のとおりです。

1. **統計**タブをクリックします。

2. **全体クエリー数**または**結果がないクエリー数**を選択します。

3. 開始日を入力します。

4. 終了日を入力します。

5. **照会**ボタンをクリックすると、統計グラフが出力されます。

6. **データダウンロード**をクリックすると、クエリーごとに統計データがダウンロードされます。

7. **全体文書数**または**全体インデックスサイズ**を選択します。

8. 開始日を入力します。

9. 終了日を入力します。

10. **照会**ボタンをクリックすると、統計グラフが出力されます。

![img](http://static.toastoven.net/prod_search/stats-ja-20200304.jpg)<br>

**REST API**

- Request
    ```
    curl -i -XGET 'http://api-7ab1617e2df0f1d1-search.cloud.toast.com/stats/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/stats?kind=total_query_count&date=2020-03-09' -H 'Accept-Language:ja'
    ```
    - kind
        - total_query_count ：全体クエリー数
        - no_result_query_count ：検索結果がないクエリー数
    - date ：照会する日
- Response
    ````
    [ [ "ナイキ", 8 ], [ "アディダス", 4 ] ]
    ````
    - クエリー数3以上のみ照会されます。

### 6. ACL

インデックスおよび検索REST APIを呼び出すことができる端末のIPを制限できます。

- 他の人がデータを削除することができるため、インデックスACLは必ず設定してください。
- コンソールからテストする場合、ACL設定は関係ありません。

**ACLの設定方法**

下記は、IPアドレスが202.179.177.21の場合にのみインデックスが可能で、検索リクエストはすべてのIPからできるように設定した例です。クエリー統計データダウンロードリクエストは、すべてのIPからできるように設定した例です。

1. **ACL**タブをクリックします。

2. **インデックス**下の**許可**にIPアドレスを入力します。

3. **統計** **許可**に「all」を入力します。

4. **検索** **許可**に「all」を入力します。

5. **保存**ボタンをクリックします。

![img](http://static.toastoven.net/prod_search/acl_procedure-ja-20200304.jpg)

## 機能詳細説明

### フィールドの削除

フィールドを削除する方法は次のとおりです。

1. 削除するフィールドの**削除**ボタンをクリックします。

2. **保存**ボタンをクリックします。

3. **今実行**ボタンをクリックします。

    - 再インデックス中は文書の追加、修正、削除ができません。

![img](http://static.toastoven.net/prod_search/field_delete-1-ja-20200304.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-2-ja-20200304.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-3-ja-20200304.jpg)

### フィールドの修正

フィールドの修正はサポートしていません。削除後に再度追加する必要があります。

### フィルタリング

**フィールド設定**

![img](http://static.toastoven.net/prod_search/filtering-field-ja-20200304.jpg)

**インデックス**

テストを行うために、下記のデータをインデックスします。

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "ナイキエアマックス",
    "category" : 1
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "ナイキシャイアンソリッド",
    "category" : 2
  }
}
]
```

**検索**

1. フィルタリング値を入力します。

![img](http://static.toastoven.net/prod_search/filtering-search-ja-20200304.jpg)

フィルタリング値の入力方法です。

- 単一の値のフィルタリング
    - 例) category=1
        - category == 1
- orフィルタリング
    - 例) category=1|2
        - category == 1 or category == 2
- andフィルタリング
    - 例) category=1&2
        - category == 1 and category == 2      
- 範囲指定フィルタリング		
    - 例) category=[1,2]
        - 1 <= category <= 2
    - 例) category={1,2]      
        - 1 < category <= 2
    - 例) category={,2]      
        - category <= 2
    - keyword、boolean、geo_pointタイプは、範囲指定フィルタリングに使用できません。
- notフィルタリング
    - 例) category=!1
        - category != 1
    - 例) category=!1|2
        - category !=1 or category == 2
- dateタイプフィルタリング
    - filter='update=[2017-03-22T08:28:44,}'
        - 2017-03-22T08:28:44 <= update
    - filter='update=[,2018-10-02T15:26:28}'
        - update < 2018-10-02T15:26:28
    - filter='update=[2017-03-22T08:28:44,2018-10-02T15:26:28}'
        - 2017-03-22T08:28:44 <= update < 2018-10-02T15:26:28
- keywordタイプフィルタリング
    - filter='dealer="DNCショップ"|"Widショッピング"'
        - keywordタイプはダブルクォーテーションの使用を推薦します。
- 複数のフィールドのフィルタリング
    - filter='category=1&brand=2'
        - category == 1 and brand == 2
    - filter='category=1|brand=2'
        - category == 1 or brand == 2
    - filter='(category=1&brand=2)|(category=3&brand=4)'
        - (category == 1 and brand == 2) or (category == 3 and brand == 4)

### 経緯度(geolocation)フィルタリング

**フィールド設定**

1. 経緯度を入力するフィールドのタイプに「geo_point」を選択します。

![img](http://static.toastoven.net/prod_search/geolocation-field-ja-20200304.jpg)

**インデックス**

テストを行うために下記のデータをインデックスします。

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "FX数学塾",
    "location" : [10.1, 10.1]
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "良木思考力数学塾",
    "location" : [10.3, 10.4]
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "name" : "数学の朝塾",
    "location" : [10.4, 10.3]
  }
}
]
```

- geo_pointタイプには[{経度},{緯度}]形式で値を入力します。

**検索**

- 半径(circle)フィルタリング
    1. フィルタリング値を入力します。
        - 形式：[{経度},{緯度}],{半径}
        - 例：[10.3,10.3],15km
            - 経度10.3、緯度10.3を中心に半径15km以内の文書のみ検索されます。
            - 半径の単位は「km」「m」「cm」を使用できます。

![img](http://static.toastoven.net/prod_search/geolocation-search-circle-ja-20200304.jpg)

- 領域(polygon)フィルタリング
    1. フィルタリング値を入力します。
        - 形式：[{経度1},{緯度1}],[{経度2},{緯度2}],[{経度N},{緯度N}]
        - 例：[10.2,10.2],[10.3,10.5],[10.5,10.2]
        - 各点は、時計方向に接続されます。
        - 接続された多角形内の文書のみ検索されます。

![img](http://static.toastoven.net/prod_search/geolocation-search-polygon-ja-20200304.jpg)

### ソート

**フィールド設定**

![img](http://static.toastoven.net/prod_search/sorting-field-ja-20200304.jpg)

**インデックス**

テストを行うために下記のデータをインデックスします。

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "ナイキエアマックス",
    "popular" : 10,
    "price" : 84180
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "ナイキエアズーム",
    "popular" : 5,
    "price" : 97200
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "name" : "ナイキエアフォース",
    "popular" : 5,
    "price" : 74680
  }
}
]
```

**検索**

1. ソート方式を指定します。

    - "asc"：昇順ソート
    - "desc"：降順ソート

2. ソート順序を指定します。

    - 上の例では「popular」で先にソートします。
    - 「popular」が同じ場合、「price」でソートします。   

![img](http://static.toastoven.net/prod_search/sorting-search-ja-20200304.jpg)

### 要約

**フィールド設定**

![img](http://static.toastoven.net/prod_search/aggregation-field-ja-20200304.jpg)

- インデックスがチェックされたフィールドのみ要約機能を使用できます。

**インデックス**

テストを行うために下記のデータをインデックスします。

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "name" : "ナイキエアマックス",
    "category" : "靴"
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "name" : "ナイキエアズーム",
    "category" : "靴"
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "name" : "ナイキスウォッシュ半袖シャツ",
    "category" : "衣類"
  }
}
]
```

**検索**

1. 「category」フィールドの「要約」をチェックします。

![img](http://static.toastoven.net/prod_search/aggregation-search-ja-20200304.jpg)

**要約結果**

```
"summary": {
	"category": {
		"靴": 2,
		"衣類": 1
	}
}
```

- 検索結果と要約情報が出力されます。
- 「category」が「靴」の検索結果が2件、「衣類」の検索結果が1件という意味です。
- 要約可能なタイプ
    - textおよびgeo_pointタイプは要約機能を使用できません。

### ブーリアンクエリー

**フィールド設定**

![img](https://static.toastoven.net/prod_search/boolean_query-field-ja-20200304.jpg)

**インデックス**

テストを行うために下記のデータをインデックスします。

```
[
{
  "action": "add",
  "id": "id-1",
  "fields": {
    "title" : "ナイキ靴"
  }
},
{
  "action": "add",
  "id": "id-2",
  "fields": {
    "title" : "ナイキシューズ"
  }
},
{
  "action": "add",
  "id": "id-3",
  "fields": {
    "title" : "ナイキバッグ"
  }
}
]
```

**検索**

1. 「boolean」を選択します。

2. &, |, (, ), ! を利用したブーリアンクエリーを入力します。

![img](https://static.toastoven.net/prod_search/boolean_query-search-ja-20200304.jpg)

- 演算子優先順位
    - (), !, &, | の順です。
- 被演算子処理
    - 被演算子はExact matchingで処理されます。
    - q=ナイキ 靴&q_option=boolean
    - 検索される検索対象
        - 「人気 ナイキ 靴 割引」
        - 「人気 ナイキ靴 割引」
    - 検索される検索対象
        - 「人気 ナイキ 割引 靴」
            - 「ナイキ」と「靴」の間に他の単語が入っているため
        - 「人気 靴 ナイキ 割引」
            - 「ナイキ」と「靴」の順序が異なるため

### 文書重み指定

**フィールド設定**

![img](http://static.toastoven.net/prod_search/document_boosting-field-ja-20200304.jpg)

**インデックス**

テストを行うために下記のデータをインデックスします。

```
[
  {
    "action": "add",
    "id": "id-1",
    "weight": 0.1,
    "fields": {
      "title" : "ナイキ"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "weight": 0.9,
    "fields": {
      "title" : "ナイキ"
    }
  }
]
```

- 「id-1」には「weight」を0.1、「id-2」には「weight」を0.9に指定します。
- 「weight」は0.0～1.0の値を入力できます。

**検索**

- 「ナイキ」で検索します。

![img](http://static.toastoven.net/prod_search/document_boosting-search-ja-20200304.jpg)

**検索結果**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 0.45151517,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>ナイキ</b>"
    },
    {
      "_RELEVANCE": 0.18484849,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>ナイキ</b>"
    }
  ]
}
```

- 「weight」を高く付与した「id-2」文書が検索結果の上位に表示されます。

**weight反映比率を調整**

- doc_weight_ratioパラメータを利用して反映比率を調整します。
    ```
    curl -G -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/search/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&doc_weight_ratio=0.1' --data-urlencode q='ナイキ' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ja'
    ```
    - 0.0～1.0の値を入力できます。
    - defaultは1.0です。

**ユーザーが入力した検索ワードと、文書の類似度(similarity)を反映して比率調整**

- similarity_ratioパラメータを利用して反映比率を調整します。
    ```
    curl -G -XGET 'https://api-7ab1617e2df0f1d1-search.cloud.toast.com/search/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&similarity_ratio=0.1' --data-urlencode q='ナイキ' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ja'
    ```
    - 0.0～1.0の値を入力できます。
    - defaultは1.0です。

**Tip**

- similarity_ratioとdoc_weight_ratioを調節して検索結果出力順序をカスタマイズできます。

### 文書ランキング指定

**フィールド設定**

![img](http://static.toastoven.net/prod_search/document_ranking-field-ja-20200304.jpg)

**インデックス**

テストを行うために下記のデータをインデックスします。

```
[
  {
    "action": "add",
    "id": "id-1",
    "ranking": 2,
    "fields": {
      "title" : "ナイキ"
    }
  },
  {
    "action": "add",
    "id": "id-2",
    "ranking": 1,
    "fields": {
      "title" : "ナイキ"
    }
  }
]
```

- 「id-1」には「ranking」を2、「id-2」には「ranking」を1に指定します。
- 「ranking」は1～10000の値を入力できます。

**検索**

- 「ナイキ」で検索します。

![img](http://static.toastoven.net/prod_search/document_ranking-search-ja-20200304.jpg)

**検索結果**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 10000.151,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>ナイキ</b>"
    },
    {
      "_RELEVANCE": 9999.151,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>ナイキ</b>"
    }
  ]
}
```

- 「ranking」を1に指定した「id-2」文書が検索結果1位に表示されます。
- 「ranking」を同じように指定した場合、ユーザーが入力した検索ワードと類似度が高い文書が先に表示されます。

### フィールド設定のダウンロード/アップロード

**設定のダウンロード**

1. 「設定ダウンロード」ボタンをクリックして現在の設定をダウンロードします。

![img](https://static.toastoven.net/prod_search/field-download-ja-20200304.jpg)

**設定のアップロード**

1. **設定アップロード**ボタンをクリックして設定をアップロードします。   

![img](https://static.toastoven.net/prod_search/filed-upload-ja-20200304.jpg)

- 設定されたフィールドが1つもない時は**設定アップロード**ボタンが表示されます。

### 全データの再インデックス
全データを再インデックスする時はFull indexing APIを使用します。

- Full indexingの開始
    ```
    curl -i -XPOST 'http://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing/full/begin'
    ```
    - 新しいindex(保存場所)が作成されます。
    - Full indexingが反映されるまでは既存indexでサービスされます。
- Full indexingのリクエスト
    ```
    curl -XPOST 'http://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing/full' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents-001.json'
    ```
    - documents-002.json, documents-003.jsonなど、複数回のインデックスをリクエストします。		
- Full indexingの反映
    ```
    curl -i -XPOST 'http://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing/full/end'
    ```
    - インデックスされたデータをサービスに反映します。
- Full indexingのキャンセル
    ```
    curl -i -XPOST 'http://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing/full/cancel'
    ```
    - インデックスが進行中の時は動作しません。

## 詳細ガイド

### フィールドタイプ
フィールドタイプ選択画面は次のとおりです。

![img](http://static.toastoven.net/prod_search/field_type-ja-20200304.jpg)

- text
    - 「検索」するフィールドの場合に選択します。
    - 形態素解析を行います。
        - フィールドの値が「ナイキ 運動靴」の場合、「ナイキ運動靴」、「ナイキ 運動靴」、「ナイキ」または「運動靴」で検索した時、検索結果に表示されます。
    - 最大サイズは32,768バイトです。
- keyword
    - 「フィルタ」、「ソート」、「要約」するフィールドの場合に選択します。
    - 形態素解析を行いません。
        - フィールドの値が「ナイキ運動靴」の場合、「ナイキ運動靴」でのみ「フィルタ」、「ソート」、「要約」されます。
        - フィールドの値が「ナイキ 運動靴」の場合、「ナイキ 運動靴」でのみ「フィルタ」、「ソート」、「要約」されます。
    - 最大サイズは128バイトです。
- byte
    - 1byteの整数です。
    - -128～127まで記憶可能です。
- short
    - 2byteの整数です。
    - -32,768～32,767まで記憶可能です。
- integer
    - 4byteの整数です。
    - -2^31～2^31 - 1まで記憶可能です。
- long
    - 8byteの整数です。
    - -2^63～2^63 - 1まで記憶可能です。
- float
    - 4byteの単精度浮動小数点実数です。   
    - -3.4E38～3.4E38まで記憶可能です。
- double
    - 8byteの単精度浮動小数点実数です。
    - -1.7E308～1.7E308まで記憶可能です。
- boolean
    - 1byte
    - true or false
- date
    - フィールドの値が日付の場合に選択します。
    - サポートする日形式
        - yyyy-MM-dd
            - 例) 2017-09-22
        - yyyy-MM-dd’T’HH:mm:ss
            - 例) 2017-09-22T15:39:28
        - yyyy-MM-dd’T’HH:mm:ss'Z'
            - 例) 2017-09-22T15:39:28Z
        - yyyy-MM-dd'T'HH:mm:ss.SSS
            - 例) 2017-09-22T15:39:28.248
        - yyyy-MM-dd'T'HH:mm:ss.SSS'Z'
            - 例) 2017-09-22T15:39:28.248Z
- textを除くすべてのフィールドタイプは、配列形式で入力できます。
    - ["ナイキ", "アディダス"]
    - [1.0, 2.0]
    - ["2017-09-22T15:39:28", "2017-09-22T15:39:29"]

### 形態素解析

形態素解析の選択画面は次のとおりです。

![img](http://static.toastoven.net/prod_search/analyzer-ja-20200304.jpg)

- default
    - 形態素解析ツールを利用して単語を分離します。
      - 例) 「ナイキ メンズシューズ」 → 「ナイキ」 「メンズ」 「シューズ」
- whitespace
    - whitespaceをセパレータにしてトークンを分離します。
      - 例) 「ナイキ メンズシューズ」 → 「ナイキ」 「メンズシューズ」
- bigram
    - 2文字ずつ単語を分離します。
      - 例) 「ナイキ メンズシューズ」 → 「ナイ」  「イキ」 「メン」 「ンズ」 「ズシ」 「シュ」 「ュー」 「ーズ」

### ACL

ACL設定画面は次のとおりです。

![img](http://static.toastoven.net/prod_search/acl-detail-ja-20200304.jpg)

- 入力形式
    - IP形式で入力できます。
        - 例) 202.179.177.21
    - CIDR形式で入力できます。
        - 例) 202.179.177.0/24
    - IPまたはCIDRを複数入力できます。
        - 例) 202.179.177.21, 202.179.177.0/24
    - allの場合、すべてマッチングされます。
    - 値が空の場合、すべてマッチングされません。
- 許可、拒否のどちらにも該当する場合、拒否されます。
- 許可、拒否のどちらにも該当しない場合、拒否されます。

## クライアントサンプルコード

次はファイルアップロード方式のインデックスのサンプルコードです。

### java

- dependency

``` java
compile group: 'org.apache.httpcomponents', name: 'httpclient', version: '4.5.6'
compile group: 'org.apache.httpcomponents', name: 'httpmime', version: '4.5.6'
```

- インデックス(ファイルアップロード方式)
``` java
package com.toast.cloud.cloudsearch.client;

import org.apache.http.HttpEntity;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.ResponseHandler;
import org.apache.http.client.methods.HttpUriRequest;
import org.apache.http.client.methods.RequestBuilder;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.mime.HttpMultipartMode;
import org.apache.http.entity.mime.MultipartEntityBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.util.EntityUtils;

import java.io.File;
import java.io.IOException;
import java.io.PrintWriter;

public class IndexingClient {

  public static void main(String[] args) throws IOException {

    String documents = ""
      + "[\n"
      + "  {\n"
      + "    \"action\": \"add\",\n"
      + "    \"id\": \"id-1\",\n"
      + "    \"fields\": {\n"
      + "      \"title\": \"[送料無料]ナイキシューズ195種！\",\n"
      + "      \"body\": \"ナイキの人気シューズには売れているワケがあります！ナイキの人気シューズ195種★一足は必要じゃないですか？\"\n"
      + "    }\n"
      + "  }\n"
      + "]";

    File tempFile = File.createTempFile("documents-",".json", new File("/tmp/"));
    tempFile.deleteOnExit();

    PrintWriter printWriter = new PrintWriter(tempFile);
    printWriter.println(documents);
    printWriter.close();

    try (CloseableHttpClient httpclient = HttpClients.createDefault()) {

      // build multipart upload request.
      HttpEntity data = MultipartEntityBuilder.create()
        .setMode(HttpMultipartMode.BROWSER_COMPATIBLE)
        .addBinaryBody("file", tempFile, ContentType.DEFAULT_BINARY, tempFile.getName())
        .build();

      // build http request and assign multipart upload data.
      HttpUriRequest request = RequestBuilder
    	  .post("https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing")
        .setEntity(data)
        .build();

      System.out.println("Executing request " + request.getRequestLine());

      // Create a custom response handler.
      ResponseHandler<String> responseHandler = response -> {
        int status = response.getStatusLine().getStatusCode();
        if (status >= 200 && status < 300) {
          HttpEntity entity = response.getEntity();
          return entity != null ? EntityUtils.toString(entity) : null;
        } else {
          throw new ClientProtocolException("Unexpected response status: " + status);
        }
      };
      String responseBody = httpclient.execute(request, responseHandler);
      System.out.println(responseBody);
    }
  }
}
```

### php

- インデックス(ファイルアップロード方式)

``` php
<?php
    $documents = ""
      . "[\n"
      . "  {\n"
      . "    \"action\": \"add\",\n"
      . "    \"id\": \"id-1\",\n"
      . "    \"fields\": {\n"
      . "      \"title\": \"[送料無料]ナイキシューズ195種！\",\n"
      . "      \"body\": \"ナイキの人気シューズには売れているワケがあります！ナイキの人気シューズ195種★一足は必要じゃないですか？\"\n"
      . "    }\n"
      . "  }\n"
      . "]";

    $file = DIRECTORY_SEPARATOR.trim(sys_get_temp_dir(), DIRECTORY_SEPARATOR).DIRECTORY_SEPARATOR.ltrim("documents.json", DIRECTORY_SEPARATOR);
    file_put_contents($file, $documents);

    register_shutdown_function(function() use($file) {
        unlink($file);
    });

    $data = array(
        'file' => curl_file_create($file, "application/json", basename($file))
    );

    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL,"https://api-7ab1617e2df0f1d1-search.cloud.toast.com/indexing/v1.0/appkeys/EMKPutYozUttWVY2/serviceids/test/indexing");
    curl_setopt($ch, CURLOPT_POST, 1);
    curl_setopt($ch, CURLOPT_HTTPHEADER, array("Content-Type:multipart/form-data; charset=UTF-8"));
    curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_HEADER, true);

    $response = curl_exec($ch) or die(curl_error($ch));
    print_r($response);

    curl_close($ch);
?>
```
