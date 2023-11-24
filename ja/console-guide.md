## Search > Cloud Search > コンソール使用ガイド

## 注意

- 文書内のアプリケーションキー「CwSx6kv99g0QuNtM」は、ユーザーごとに異なります。

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

4. 複数の値を使用するかどうかをチェックします。

    - フィールド値のセパレータは、(カンマ)のみ使用でき、最大30個まで使用できます。

5. インデックスを使用するかどうかをチェックします。

6. フィルタを使用するかどうかをチェックします。

7. ソートを使用するかどうかをチェックします。

8. 要約を使用するかどうかをチェックします。

9. **保存**ボタンをクリックします。

![img](http://static.toastoven.net/prod_search/field_create_procedure-ja-20230831.jpg)

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

- ファイル説明
    - action
        - add:該当文書が追加されます。
            - 既に同じIDが存在する場合はアップデートされます。
        - delete:該当文書が削除されます。
    - ID
        - 文書の固有IDです。
        - IDのタイプは文字列です。
    - 最大ファイルサイズは8MBです。
        - 8MB以上のデータは複数に分けてインデックスする必要があります。

**インデックス方法**

1. **インデックス**タブをクリックします。

2. **ファイル選択**ボタンをクリックします。

3. インデックスするファイルを選択します。

4. **開く**ボタンをクリックします。

5. インデックスコマンドがREST APIで出力されます。

    - REST APIを利用して検索サービスを開発できます。

6. **インデックス**ボタンをクリックします。

7. インデックス結果を確認します。

![img](http://static.toastoven.net/prod_search/indexing_procedure_01-ja-20230831.jpg)
![img](http://static.toastoven.net/prod_search/indexing_procedure_02-ja-20230831.jpg)<br>

**REST API**

下記のようにREST APIを使用可能です。

- インデックスAPI
    - Request
        - ファイルアップロード方式
	      ```
	      curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing' -H 'Accept-Language:ja' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents.json'
	      ```
        - ペイロード(payload)方式
	      ```
	      curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing' -H 'Accept-Language:ja' -H 'Content-Type:application/json; charset=UTF-8' -d '
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
	    curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing_log?id=1' -H 'Accept-Language:ja'
	    ```
	    - id 1は上のインデックスAPI Responseのidです。
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
	    - 2 :無視された(フィールド設定変更前のインデックスリクエストは無視される)
	    - 3 :進行中
	    - 4 :成功
	    - 5 :失敗
	    - 6 :キャンセル

### 4. 検索

検索方法は次のとおりです。

1. **検索**タブをクリックします。

2. 検索するフィールド名をチェックします。

3. 検索するフィールドごとに重みを設定します。

    - 0.0～1.0の値を設定します。

4. ソートするフィールドを選択します。

    - 多重ソートする場合は多重ソートフィールドを選択します。
    - ソート方式を指定します。

5. 検索結果に出力するフィールドをチェックします。

6. 検索結果の長さを設定します。

7. 強調(highlight) preタグを設定します。

8. 強調(highlight) postタグを設定します。

9. 検索結果で出力する開始順位を指定します。

    - 「1」に設定すると1位から出力され、「10」に設定すると10位から出力されます。

10. 検索結果の数を指定します。

    - 「5」に設定すると5個出力され、「10」に設定すると10個出力されます。

11. 検索演算子を選択します。

12. 検索する単語を入力します。

13. 検索アイコンをクリックします。

14. 2～11番まで設定した内容がREST APIで出力されます。

    - REST APIを利用して検索サービスを開発できます。

15. 検索結果が出力されます。

![img](http://static.toastoven.net/prod_search/basic-search-ja-20230831.jpg)<br>

**REST API**

下記のようにREST APIを使用できます。

- Request
  ```
  curl -G -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,body*1.0,title*1.0&return=&passage.body=180&passage.title=180' -H 'Accept-Language:ja' --data-urlencode q='ナイキ 運動靴' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ja'
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
            "_RELEVANCE" : 100,
            "_RANK" : 1,
            "_ID" : "id-2",
            "body" : "7日間だけの限定価格！超特価]アディダスシューズ109種！迷っていたら売り切れ必至",
            "title" : "[超特価]<b>ナイキ</b> <b>運動靴</b> 109種"
          }
        ]
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
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/stats/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/stats?kind=total_query_count&date=2020-03-09' -H 'Accept-Language:ja'
	```
    - kind
	    - total_query_count ：全クエリー数
	    - no_result_query_count ：検索結果がないクエリー数
    - date ：照会する日
- Response
    ```
    [ [ "ナイキ", 8 ], [ "アディダス", 4 ] ]
    ```
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

    - 多重ソートフィールドで使用されるフィールドは、削除できません。多重ソートフィールドを削除してから進めてください。

2. **保存**ボタンをクリックします。

3. **今再インデックス**ボタンをクリックします。

    - 再インデックス中は文書の追加、修正、削除ができません。

![img](http://static.toastoven.net/prod_search/field_delete-1-ja-20230831.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-2-ja-20230831.jpg)
![img](http://static.toastoven.net/prod_search/field_delete-3-ja-20230831.jpg)

### フィールドの修正

フィールドの修正はサポートしていません。削除後に再度追加する必要があります。

### フィルタリング

**フィールド設定**

1. 対象フィールドのフィルタを使用するかどうかをチェックします。
2. 'text'タイプの場合はフィルタ機能をサポートしません。

![img](http://static.toastoven.net/prod_search/filtering-field-ja-20230831.jpg)

- フィルタがチェックされたフィールドのみ機能を使用できます。

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

![img](http://static.toastoven.net/prod_search/filtering-search-ja-20230831.jpg)

フィルタリング値の入力方法です。

1. filter_and : 単一値フィルタリング、フィルタフィールド間のand演算が必要な時に使用します。
2. filter_or :フィルタフィールド間or演算が必要な場合、v2使用します。
    - 範囲指定、経緯度フィルタリングに使用できません。

- 単一の値のフィルタリング
    - 例) filter_and='category=1'
    	- category == 1
- orフィルタリング
    - 例) filter_and='category=1|2'
    	- category == 1 or category == 2
- andフィルタリング
    - 例) filter_and='category=1&2'
    	- category == 1 and category == 2
- 範囲指定フィルタリング
    - 例) filter_and='category=[1,2]'
    	- 1 <= category <= 2
    - 例) filter_and='category={1,2]'
  	    - 1 < category <= 2
    - 例) filter_and='category={,2]'
  	    - category <= 2
    - keyword, boolean, geo_pointタイプは、範囲指定フィルタリングに使用できません。
- notフィルタリング
    - 例) filter_and='category=!1'
  	    - category != 1
- dateタイプフィルタリング
    - filter_or='update=[2017-03-22T08:28:44,}'
    	- 2017-03-22T08:28:44 <= update
    - filter_or='update=[,2018-10-02T15:26:28}'
 	    - update < 2018-10-02T15:26:28
    - filter_or='update=[2017-03-22T08:28:44,2018-10-02T15:26:28}'
	    - 2017-03-22T08:28:44 <= update < 2018-10-02T15:26:28
- keywordタイプフィルタリング
    - filter_and='dealer="DNCショップ"|"Widショッピング"'
 	    - keywordタイプはダブルクォーテーションの使用を推薦します。
- 複数のフィールドのフィルタリング
    - filter_and='category=1&brand=2'
 	    - category == 1 and brand == 2
    - filter_or='category=1|brand=2'
 	    - category == 1 or brand == 2
    - filter_or='(category=1&brand=2)|(category=3&brand=4)'
 	    - (category == 1 and brand == 2) or (category == 3 and brand == 4)

### 経緯度(geolocation)フィルタリング

**フィールド設定**

1. 経緯度を入力するフィールドのタイプに「geo_point」を選択します。

![img](http://static.toastoven.net/prod_search/geolocation-field-ja-20230831.jpg)

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

![img](http://static.toastoven.net/prod_search/geolocation-search-circle-ja-20230831.jpg)

- 領域(polygon)フィルタリング
1. フィルタリング値を入力します。
    - 形式：[{経度1},{緯度1}],[{経度2},{緯度2}],[{経度N},{緯度N}]
    - 例：[10.2,10.2],[10.3,10.5],[10.5,10.2]
    - 各点は、時計方向に接続されます。
    - 接続された多角形内の文書のみ検索されます。

![img](http://static.toastoven.net/prod_search/geolocation-search-polygon-ja-20230831.jpg)

### ソート

**フィールド設定**

1. 対象フィールドのソートを使用するかどうかをチェックします。
2. 'text'タイプの場合はソート機能をサポートしません。
3. 多重値を使用する場合はソート機能をサポートしません。

![img](http://static.toastoven.net/prod_search/sorting-field-01-ja-20230831.jpg)

- ソートがチェックされたフィールドのみ機能を使用できます。

**多重ソート設定**

1. フィールド名を入力します。
2. 対象フィールドを追加後、選択して順序を調整します。
    - ソートが2つ以上あると出力されます。
    - 選択順序通りにソートします。
3. 各フィールドのソート方式を選択します。

![img](http://static.toastoven.net/prod_search/sorting-field-02-ja-20230920.jpg)

- 2つ以上のフィールドのソートがチェックされた場合に機能を使用できます。

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

1. ソートフィールドを選択し、方式を指定します。

    - "asc"：昇順ソート
    - "desc"：降順ソート

2.  多重ソートフィールドを選択し、方式を指定します。

    - "asc"：昇順ソート
    - "desc"：降順ソート

![img](http://static.toastoven.net/prod_search/sorting-search-01-ja-20230831.jpg)
![img](http://static.toastoven.net/prod_search/sorting-search-02-ja-20230831.jpg)

- 1つのソートフィールドのみ選択可能です。

### 要約

**フィールド設定**

1. 対象フィールドの要約を使用するかどうかをチェックします。
2. 'text', 'geo_point'タイプの場合、要約機能をサポートしません。

![img](http://static.toastoven.net/prod_search/aggregation-field-ja-20230831.jpg)

- 要約がチェックされたフィールドのみ機能を使用できます。

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

1. categoryフィールドの「要約」をチェックします。

![img](http://static.toastoven.net/prod_search/aggregation-search-ja-20230831.jpg)

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
- categoryが「靴」の検索結果が2件、「衣類」の検索結果が1件という意味です。
- 要約可能なタイプ
    - 「text」および「geo_point」タイプは要約機能を使用できません。

### ブーリアンクエリー

**フィールド設定**

![img](https://static.toastoven.net/prod_search/boolean_query-field-ja-20230831.jpg)

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

![img](https://static.toastoven.net/prod_search/boolean_query-search-ja-20230831.jpg)

- 演算子優先順位
    - (), !, &, | の順です。
- 被演算子処理
    - 被演算子はExact matchingで処理されます。
    - q=ナイキ 靴&q_option=boolean
    - 検索される検索対象
        - 「人気 ナイキ 靴 割引」
        - 「人気 ナイキ靴 割引」
    - 検索されない検索対象
        - 「人気 ナイキ 割引 靴」
            - 「ナイキ」と「靴」の間に他の単語が含まれているため
        - 「人気 靴 ナイキ 割引」
            - 「ナイキ」と「靴」の順序が異なるため 

### フィールドの重み指定

**検索**

- 「ナイキ」で検索します。

![img](http://static.toastoven.net/prod_search/document_boosting-search-01-ja-20230831.jpg)
![img](http://static.toastoven.net/prod_search/document_boosting-search-02-ja-20230831.jpg)

**検索結果**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 200,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>ナイキ</b>"
      "body": "<b>ナイキ</b>"
    },
    {
      "_RELEVANCE": 200,
      "_RANK": 2,
      "_ID": "id-1",
      "title": "<b>ナイキ</b>"
      "body": "<b>ナイキ</b>"
    }
  ]
}
```

- 「title」フィールドに重みが高く付与され、「id-2」文書が検索結果上位に表示されます。

**重み反映比率を調整**

- doc_weight_ratioパラメータを利用して反映比率を調整します。
    ```
    curl -G -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,title*1.0&return=&passage.title=180&doc_weight_ratio=0.1' --data-urlencode q='ナイキ' --data-urlencode highlight='<b>,</b>' -H 'Accept-Language:ja'
    ```
    - 0.0～1.0の間の値を入力できます。
    - defaultは1.0です。

**Tip**

- 検索の重みと文書ランキングを調節して、検索結果出力順序をカスタマイズできます。

### 文書ランキング指定

**フィールド設定**

![img](http://static.toastoven.net/prod_search/document_ranking-field-ja-20230831.jpg)

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

![img](http://static.toastoven.net/prod_search/document_ranking-search-ja-20230831.jpg)

**検索結果**

```
"itemList": {
  "item": [
    {
      "_RELEVANCE": 100,
      "_RANK": 1,
      "_ID": "id-2",
      "title": "<b>ナイキ</b>"
    },
    {
      "_RELEVANCE": 100,
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

![img](https://static.toastoven.net/prod_search/field-download-ja-20230831.jpg)

**設定のアップロード**

1. **設定アップロード**ボタンをクリックして設定をアップロードします。

![img](https://static.toastoven.net/prod_search/filed-upload-ja-20230831.jpg)

- 設定されたフィールドが1つもない時は**設定アップロード**ボタンが表示されます。

### 全データの再インデックス

全データを再インデックスする時はFull indexing APIを使用します。

- Full indexingの開始
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/begin'
	```
    - 新しいindex(保存場所)が作成されます。
    - Full indexingが反映されるまでは既存indexでサービスされます。
- Full indexingのリクエスト
    ```
    curl -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full' -H 'Content-Type:multipart/form-data; charset=UTF-8' -F 'file=@documents-001.json'
    ```
    - documents-002.json, documents-003.jsonなど、複数回のインデックスをリクエストします。
- Full indexingの反映
    ```
    curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/end'
    ```
  - インデックスされたデータをサービスに反映します。
- Full indexingのキャンセル
    ```
    curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing/full/cancel'
    ```
    - インデックスが進行中の時は動作しません。

### 同義語辞典

**URL**

1. 登録
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/thesaurus?way=1
2. 削除
	- DELETE	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/thesaurus
3. リセット
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/thesaurus/reset

**パラメータ**

- パラメータ
	- way	
- 値
	- 1 :単方向(デフォルト値)
	- 2 :双方向
	
**形式**
- 単語間をカンマ(',')で区切ります。単語内に空白、セパレータを使用不可

**同意語**

1. 初期状態
- '靴'検索
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=靴&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
	  "item": [
	    {
	      "_ID": "100433865",
	      "_RANK": "0",
	      "_RELEVANCE": 100,
	      "productName": "ブティック リアルラビット スリッパ 毛皮スリッパ オフィス<b>靴</b>"
	    }
	  ]
	}
	```
	
2. 同義語辞書登録(単方向)
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/thesaurus?way=1'
	```
	```
	靴,スニーカー,スポーツシューズ
	```
- '靴'検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=靴&passage.productName=180'
	```

	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "100433865",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "ブティック リアルラビット スリッパ 毛皮スリッパ オフィス<b>靴</b>"
        },
        {
          "_ID": "101874425",
          "_RANK": "0",
          "_RELEVANCE": 1,
          "productName": "アイボリードットスニーカー"
        },
        {
	      "_ID": "101714054",
	      "_RANK": "0",
	      "_RELEVANCE": 1,
	      "productName": "ナイキ/Nike Free TR 8 - Womens/Nike/機能性 スポーツシューズ/ラファッショニスタ"
	    }
	  ]
	}
	```
- 'スニーカー'検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=スニーカー&passage.productName=180'
	```

	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "101874425",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": アイボリードット<b>スニーカー</b>"
        }
	  ]
	}
	```

	
4. 同意語削除(単方向)

	- Request
	```
	curl -i -XDELETE 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/thesaurus'
	```
	```
	靴
	```
- '靴'検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=靴&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "100433865",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "ブティック リアルラビット スリッパ 毛皮スリッパ オフィス<b>靴</b>"
        }
	  ]
	}
	```

- 'スニーカー'検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=スニーカー&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "101874425",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": アイボリードット<b>スニーカー</b>"
        }
	  ]
	}
	```

5. 同意語 初期化
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/thesaurus/reset'
	```

### 不用語辞書

**URL**

1. 登録
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/stopwords
2. 削除
	- DELETE	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/stopwords
3. リセット
	- POST	/dictionary/v2.0/appkeys/EMKPutYozUttWVY/serviceids/test/dictionary/stopwords/reset

**形式**

- 単語間をnew line('\n')単位で区切ります。単語内の空白は使用不可

**不用語**

1. 初期状態
- 'コーヒー'検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=コーヒー&passage.productName=180'
	```
	
	- Response
	```
	"itemList": {
      "item": [
        {
          "_ID": "100433702",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "(STANLEY)  スタンレーマウンテン<b>コーヒー</b>システム500ミリ"
        }
      ]
	}
	```

2. 不用語の事前登録
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/stopwords'
	```
	```
 コーヒー 
 コールドブリュー 
	```
	
- 'コーヒー'検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q=コーヒー&passage.productName=180'
	```

	- Response
	```
	{
      "message": {
        "result": {
          "total": 0,
          "query": "コーヒー",
          "start": 1,
          "status": {
             "code": 200,
             "message": "OK"
          },
          "itemCount": 0
        },
        "meta": {
          "timezone": "+09:00"
        }
      }
    }
	```
	
- ' コールドブリュー '検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q= コールドブリュー &passage.productName=180'
	```

	- Response
	```
	{
      "message": {
        "result": {
          "total": 0,
          "query": " コールドブリュー ",
          "start": 1,
          "status": {
             "code": 200,
             "message": "OK"
          },
          "itemCount": 0
        },
        "meta": {
          "timezone": "+09:00"
        }
      }
    }
	```
	
2. 不用語の事前削除
	- Request
	```
	curl -i -XDELETE 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/stopwords'
	```
	```
 コールドブリュー 
	```


- ' コールドブリュー '検索
	- Request
	```
	curl -i -XGET 'https://kr1-search.api.nhncloudservice.com/search/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/search?start=1&size=10&q_option=and,productName*1.0&return=productName&q= コールドブリュー &passage.productName=180'
	```
	
	- Response
	```
    "itemList": {
      "item": [
        {
          "_ID": "101704573",
          "_RANK": "0",
          "_RELEVANCE": 100,
          "productName": "[ブルービクセン] ティモレステ <b>コールドブリュー</b> オランダコーヒー 750ml (高級型)"
        }
      ]
    }
	```

3. 不用語辞書の初期化
	- Request
	```
	curl -i -XPOST 'https://kr1-search.api.nhncloudservice.com/dictionary/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/dictionary/stopwords/reset'
	```

## 詳細ガイド

### フィールドタイプ

フィールドタイプ選択画面は次のとおりです。

![img](http://static.toastoven.net/prod_search/field_type-ja-20230831.jpg)

- text
    - 「検索」するフィールドの場合に選択します。
    - 形態素解析を行います。
        - フィールドの値が「ナイキ運動靴」の場合、「ナイキ運動靴」、「ナイキ運動靴」、「ナイキ」または「運動靴」で検索した時、検索結果に表示されます。
    - 最大サイズは32,768バイトです。
- keyword
    - 「フィルタ」、「ソート」、「要約」するフィールドの場合に選択します。
    - 形態素解析を行いません。
        - フィールドの値が「ナイキ運動靴」の場合、「ナイキ運動靴」でのみ「フィルタ」、「ソート」、「要約」されます。
        - フィールドの値が「ナイキ運動靴」の場合、「ナイキ運動靴」でのみ「フィルタ」、「ソート」、「要約」されます。
    - 最大サイズは128バイトです。
- byte
    - 1byteの整数です。
    - -128～127まで記憶可能です。
- short
    - 2byteの整数です。
    - -32,768～32,767まで記憶可能です。
- integer
    - 4byteの整数です。
    - -999,999,999～999,999,999まで記憶可能です。
- long
    - 8byteの整数です。
    - -999,999,999,999,999,999～999,999,999,999,999,999まで記憶可能です。
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
- textを除くすべてのフィールドタイプは、配列形式で入力できます。
    - ["ナイキ", "アディダス"]
    - [1.0, 2.0]
    - ["2017-09-22T15:39:28", "2017-09-22T15:39:29"]

### 形態素解析

形態素解析の選択画面は次のとおりです。

![img](http://static.toastoven.net/prod_search/analyzer-ja-20230831.jpg)

- default
    - 形態素解析ツールを利用して単語を分離します。
        - 例) 「ナイキメンズシューズ」 → 「ナイキ」 「メンズ」 「シューズ」
- whitespace
    - whitespaceをセパレータにしてトークンを分離します。
        - 例) 「ナイキ メンズシューズ」 → 「ナイキ」 「メンズシューズ」
- bigram
    - 2文字ずつ単語を分離します。
        - 例) 「ナイキ メンズシューズ」 →「ナイ」 「イキ」 「メン」 「ンズ」 「ズシ」 「シュ」 「ュー」 「ーズ」
- quadgram
    - 4文字ずつ単語を分離します。
        - 例) 「スタンスミス」 → 「スタンス」 「タンスミ」 「ンスミス」
- trigram
    - 3文字ずつ単語を分離します。
        - 例) 「スタンスミス」 → 「スタン」 「タンス」 「ンスミ」 「スミス」
- unigram
    - 1文字ずつ単語を分離します。
        - 例) 「スタンスミス」 → 「ス」 「タ」 「ン」 「ス」 「ミ」 「ス」

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

```java
compile group: 'org.apache.httpcomponents', name: 'httpclient', version: '4.5.6'
compile group: 'org.apache.httpcomponents', name: 'httpmime', version: '4.5.6'
```

- インデックス(ファイルアップロード方式)

```java
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
  .post("https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing")
        .setEntity(data)
        .build();
       .post("https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing")
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

```php
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
    curl_setopt($ch, CURLOPT_URL,"https://kr1-search.api.nhncloudservice.com/indexing/v2.0/appkeys/CwSx6kv99g0QuNtM/serviceids/test/indexing");
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
