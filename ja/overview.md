<!-- pre-align:aligned sig=51287bc99a9c -->

<a id="search-cloud-search-overview"></a>
## Search > Cloud Search > 概要 { #search-cloud-search-overview }

別途インフラおよび検索ソリューションをインストールしなくても、簡単に検索サービスを構築できます。

- インデックスREST APIを利用して検索するデータを入力します。
- 検索REST APIを利用して検索結果を取得します。

<a id="developing-search-service"></a>
### 検索サービス開発プロセス { #developing-search-service }

**サービス構成図**

![img](http://static.toastoven.net/prod_search/block_diagrm-ja-20200304.png)

**サービス開発プロセス**

1. サービス作成

    - 検索サービスを作成します。

2. フィールド設定

    - 検索データのスキーマを設定します。

3. インデックス

    - Cloud Searchの入力形式に合わせてJSONデータを作成します。
    - 作成されたJSONデータをREST APIを利用してCloud Searchに入力します。

4. 検索

    - 検索REST APIの結果を利用してフロント画面を構成します。
