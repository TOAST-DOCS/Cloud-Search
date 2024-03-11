## Search > Cloud Search > API v2.0ガイド

NHN Cloud Searchで提供するCloud Search API v2.0を説明します。

## 共通

**[リクエスト]**

URI情報

| 環境 | URI                                        |
| ---- | ------------------------------------------ |
| REAL | https://kr1-search.api.nhncloudservice.com |

Pathパラメータ情報

| 名前     | 説明                   |
| --------- | ----------------------- |
| appKey    | コンソールで発行されたアプリケーションキー |
| serviceId | ユーザーの任意の名前   |

## 全体インデックス

全体インデックスを実行すると、以前にインデックスしたファイルは消えます。

必ず開始-インデックス-終了の順番で実行する必要があります。

### 1. 開始

**[リクエスト]**

URI情報

| メソッド | URI                                                                            |
| ------ | ------------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/begin |

**[レスポンス]**

レスポンス本文

```
{}
```

### 2. インデックス

**[リクエスト]**

URI情報

| メソッド | URI                                                                      |
| ------ | ------------------------------------------------------------------------ |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full |

BODY情報(例)

```
[
    {
        "action": "add",
        "id": "id-1",
        "fields": {
            "title": "大当たり！一等！"
        }
    }
]
```

**[レスポンス]**

レスポンス本文(例)

```
{
    "id": 1
}
```

### 3. 終了

**[リクエスト]**

URI情報

| メソッド | URI                                                                          |
| ------ | ---------------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/end |

**[レスポンス]**

レスポンス本文

```
{}
```

### 4. キャンセル

**[リクエスト]**

URI情報

| メソッド | URI                                                                             |
| ------ | ------------------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing/full/cancel |

**[レスポンス]**

レスポンス本文

```
{}
```

## 追加インデックス

インデックスは既存のIDがある場合はアップデートされ、IDがない場合は追加されます。

### 1. 追加インデックス

**[リクエスト]**

URI情報

| メソッド | URI                                                                 |
| ------ | ------------------------------------------------------------------- |
| POST   | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing |

BODY情報(例)

```
[
    {
        "action": "add",
        "id": "id-2",
        "fields": {
            "title": "大当たり！二等！"
        }
    }
]
```

**[レスポンス]**

レスポンス本文(例)

```
{
    "id": 2
}
```

## インデックスログ

インデックス結果を表示します。

### 1. インデックスログ照会

**[リクエスト]**

URI情報

| メソッド | URI                                                                          |
| ------ | ---------------------------------------------------------------------------- |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/indexing_log?id=1 |

パラメータ情報

| 名前 | 説明   |
| ---- | ------- |
| id   | インデックスID |

**[レスポンス]**

レスポンス本文(例)

```
{
    "total_doc_count" : 3,
    "request_time" : "2024-01-30T14:12:01",
    "file_name" : "payload-1.json",
    "total_index_file_size" : 355,
    "file_size" : 355,
    "status" : 4
}
```

## 検索

インデックスを利用してフィールドを検索できます。

### 1. 検索

**[リクエスト]**

URI情報(例)

| メソッド | URI                                                                                                                            |
| ------ | ------------------------------------------------------------------------------------------------------------------------------ |
| GET    | /indexing/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/search?q=&q_option=and,title\*1.0&start=1&size=10&passage.title=180 |

パラメータ情報

| 名前            | 説明                                   |
| ---------------- | --------------------------------------- |
| start            | 開始番号(必須)                        |
| size             | サイズ(必須)                             |
| q_option         | and, or, boolean、フィールド\* 重み(必須) |
| return           | 結果出力                              |
| q                | クエリ                                   |
| sort             | ソート                                   |
| passage.\*       | 結果の長さ                               |
| summary.\*       | 要約                                   |
| filter_and       | フィルタAnd                                |
| filter_or        | フィルタOr                                 |
| highlight        | ハイライト                             |
| doc_weight_ratio | 重み                                 |

**[レスポンス]**

レスポンス本文(例)

```
{
    "message": {
        "result": {
            "total": 2,
            "query": "",
            "start": 1,
            "itemList": {
                "item": [
                    {
                        "_ID": "id-1",
                        "_RANK": "0",
                        "_RELEVANCE": 100,
                        "title": "大当たり！一等！"
                    },
                    {
                        "_ID": "id-2",
                        "_RANK": "0",
                        "_RELEVANCE": 100,
                        "title": "大当たり！二等！"
                    }
                ]
            },
            "status": {
                "code": 200,
                "message": "OK"
            },
            "itemCount": 2
        },
        "meta": {
            "timezone": "+09:00"
        }
    }
}
```

## 統計

統計は全体クエリと結果がないクエリの数を日付(日)別に表示します。

### 1. stat照会

**[リクエスト]**

URI情報(例)

| メソッド | URI                                                                                                  |
| ------ | ---------------------------------------------------------------------------------------------------- |
| GET    | /stats/v2.0/appkeys/{{appKey}}/serviceids/{{serviceId}}/stats?kind=total_query_count&date=2024-01-29 |

パラメータ情報

<table>
    <tr>
        <th>名前</th>
        <th>説明</th>
    </tr>
    <tr>
        <td rowspan="2">kind</td>
        <td>total_query_count - 全体クエリ数</td>
    </tr>
    <tr>
        <td>no_result_query_count - 結果がないクエリ数</td>
    </tr>
    <tr>
        <td>date</td>
        <td>日付</td>
    </tr>
</table>

**[レスポンス]**

レスポンス本文(例)

```
[["", 13]]
```
