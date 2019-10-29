---
lab:
    title: 'Cosmos DB でのグローバル分散データベースの構築'
    module: 'モジュール 4: Azure Cosmos DB によるグローバルに分布されたデータベースの構築'
---

# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 4 - Cosmos DB でのグローバル分散データベースの構築

**所要時間**: 90 分

**前提条件**: このラボのケース スタディは既に確認していることを前提としています。内容とラボを前提としています。モジュール 1：Azure for the Data Engineer のコースとラボも完了済みであることを前提としています。

**ラボ ファイル**: このラボのファイルは、_Allfiles\Labfiles\Starter\DP-200.4_のフォルダーにあります。

## ラボの概要

受講者は、Azure Cosmos DB が組織にもたらす機能について説明し、デモンストレーションすることができるようになります。Cosmos DB インスタンスを作成し、ポータルと .Net アプリケーションを通じてデータをアップロードしてクエリを実行する方法を習得します。その後、Cosmos DB データベースのグローバル スケールを有効にする方法をデモンストレーションできるようになります。

## ラボの目的
  
このモジュールを修了すると、次のことができるようになります:

1. 拡張可能な Azure Cosmos DB データベースを作成する
1. Azure Cosmos DB データベースにデータを挿入してクエリを実行する
1. Visual Studio Code で Azure Cosmos DB 用の .NET コア アプリを構築できる
1. Azure Cosmos DB でデータをグローバルに配布する

## シナリオ
  
AdventureWorks の開発者および情報サービス部門は、Azure で最近リリースされた Cosmos DB と呼ばれる新サービスが、ほぼリアルタイムでデータへのプラネタリー規模のアクセスを提供できることを認識しています。彼らは、サービスの提供する機能と、それが AdventureWorks にもたらす価値、およびその際の状況を理解したいと考えています。

インフォメーション サービス部門は、サービスのセットアップ方法とデータのアップロード方法について理解したいと考えています。開発者は、Cosmos にデータをアップロードするために使用できるアプリケーションの例を知りたいと考えています。どちらも、プラネタリー規模の要求がどのように満たされるのかを理解したいと考えています。

このラボを完了すると:

1. 拡張可能な Azure Cosmos DB データベースを作成する
1. Azure Cosmos DB データベースにデータを挿入してクエリを実行する
1. Visual Studio Code で Azure Cosmos DB 用の .NET コア アプリを構築できる
1. Azure Cosmos DB でデータをグローバルに配布する

> **重要**: このラボを進めるにつれ、プロビジョニングまたは構成タスクで発生した問題を書き留め、_\Labfiles\DP-200-Issues-Docx_ にあるドキュメントの表に記録してください。ラボ番号を文書化し、テクノロジーを書き留め、問題とその解決を説明してください。このドキュメントは、後のモジュールで参照できるように保存します。

## エクササイズ 1: 拡張可能な Azure Cosmos DB データベースを作成する

所要時間: 10 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. Azure Cosmos DB インスタンスを作成する

### タスク 1: Azure Cosmos DB インスタンスを作成する

1. Azure portal で、[**+ リソースを作成する**] ブレードに移動します。

1. 新規のブレードで、[**マーケットプレースの検索**] テキスト ボックスに移動し、「**Cosmos**」という単語を入力します。表示される一覧の [**Azure Cosmos DB**] をクリックします。

1. **[Azure Cosmos DB]** ブレードで **[作成]** をクリックします。

1. **[Azure Cosmos DB アカウントの作成]** 画面から、次の設定を使用して Azure Cosmos DB アカウントを作成します。

    - サブスクリプション: このラボで使用するサブスクリプションの名前

    - リソース グループ名: **awrgstudxx** (**xx** は自分のイニシャル)

    - アカウント名: **awcdbstudxx** (**xx** は自分のイニシャル)

    - API: **Core(SQL)**

    - 場所: ラボの場所に最も近い Azure リージョンの名前と、Azure VM をプロビジョニングできる場所。

1. **[Azure Cosmos DB アカウントの作成]** ブレードで **[レビュー + 作成]** をクリックします。

1. **[Azure Cosmos DB アカウントの作成]*** ブレードの検証後、[**作成**] をクリックします。

   > **注記**: プロビジョニングの所要時間は約 5 分です。これらのエクササイズでは、Azure でサービスをプロビジョニングする際の追加のタブの説明は省略されています。プロビジョニング画面には、[ネットワーク]、[タグ]、[詳細] などの追加のタブが表示されることがあります。これにより、サービスに対してカスタマイズした設定を定義できます。たとえば、多くのサービスの [ネットワーク] タブを使用すると、仮想ネットワークの構成を定義できるため、特定のデータ サービスに対してネットワーク トラフィックを制御および保護することができます。[タグ] オプションは名前と値のペアになっており、複数のリソースおよびリソース グループに同じタグを適用して、リソースを分類し、一括請求を表示することができます。[詳細] タブは、タブのあるサービスによって異なります。ただし、これらの領域を制御し、ネットワーク管理者や財務部門と協力して、これらのオプションの構成方法を確認する必要がある点に注意してください。

1. プロビジョニングが完了すると、[デプロイが完了しました] という画面が表示されます。[**リソースに移動**] をクリックして次のエクササイズに進みます。  

>**結果** このエクササイズでは、Azure Cosmos DB アカウントのプロビジョニングを実行しました。

## エクササイズ 2: Azure Cosmos DB データベースにデータを挿入してクエリを実行する
  
所要時間: 20 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. Azure Cosmos DB データベースとコレクションをセットアップする

1. ポータルを使用してデータを追加する

1. Azure portal でクエリを実行する

1. データに対して複雑な操作を実行する

### タスク 1: Azure Cosmos DB データベースとコレクションをセットアップする

1. Azure portal の [**awcdbstudxx - クイック スタート**] 画面で、ブレードから [**概要**] オプションをクリックします。

1. [**awcdbstudxx**] 画面で、[**+ コレクションの追加**] をクリックします。これにより、**データ エクスプローラー** で [**コレクションの追加**] 画面が開きます。   

1. [**コレクションの追加**] 画面で、次の設定で「衣料品」という名前のコレクションを含む製品データベースを作成します。 

    - データベース ID: **製品**

    - サブスクリプション:  **衣料品**

    - パーティション キー: **/productId**

    - 残りのオプションは既定値のままにしておきます

1. [**コレクションの追加**] 画面で、[**OK**] をクリックします。 

### タスク 2: ポータルを使用してデータを追加する

1. [**awcdbstudcto - データ エクスプローラー**]  画面で、データ エクスプローラー ツールバーの [新規コレクション] ボタンの反対側で、[**全画面表示**] ボタンをクリックします。  [全画面表示] ダイアログ ボックスで、[**開く**] をクリックします。Microsoft Edge で新しいタブが開きます。

1. **SQL API** ウィンドウで、[**衣料品**] を展開し、[**ドキュメント**] をクリックします。新しいドキュメントが表示され、置き換えるサンプル JSON が表示されます。

1. [ドキュメント] ウィンドウで、[**New Document**] (新規ドキュメント) のアイコンをクリックします。

1. 次のコードをコピーし、[**ドキュメント**] タブに貼り付けます。

    ```JSON
    {
       "id": "1",
       "productId": "33218896",
       "category": "Women's Clothing",
       "manufacturer": "Contoso Sport",
       "description": "Quick dry crew neck t-shirt",
       "price": "14.99",
       "shipping": {
           "weight": 1,
           "dimensions": {
           "width": 6,
           "height": 8,
           "depth": 1
          }
       }
    }
    ```

1. [ドキュメント] タブに JSON を追加したら、[**保存**] をクリックします。

1. [ドキュメント] ウィンドウで、[**New Document**] (新規ドキュメント) のアイコンをクリックします。

1. 次のコードをコピーし、[**ドキュメント**] タブに貼り付けます。

    ```JSON
    {
        "id": "2",
        "productId": "33218897",
        "category": 「レディースアウターウェア」
        "manufacturer": "Contoso",
        "description": "Black wool pea-coat",
        "price": "49.99",
        "shipping": {
            "weight": 2,
            "dimensions": {
            "width": 8,
            "height": 11,
            "depth": 3
            }
        }
    }
    ```

1. [ドキュメント] タブに JSON を追加したら、[**保存**] をクリックします。

1. 左側のメニューで各ドキュメントをクリックすると、保存された各ドキュメントを表示することができます。

### タスク 3: Azure portal でクエリを実行する。

1. Azure portal の [**ドキュメント**] 画面で、[**新規 SQL クエリ**] ボタンをクリックします。

    > **注記**: [クエリ 1] 画面が表示され、クエリ **SELECT * FROM c** が表示されます。

1. productId 1 の詳細を示す JSON ファイルを返すクエリを記述します。

    ```SQL
    SELECT *
    FROM Products p
    WHERE p.id ="1"
    ```

1. [**Execute Query**] (クエリの実行) アイコンをクリックします。次の結果が返されます

    ```JSON
    [
        {
            "id": "1",
            "productId": "33218896",
            "category": "Women's Clothing",
            "manufacturer": "Contoso Sport",
            "description": "Quick dry crew neck t-shirt",
            "price": "14.99",
            "shipping": {
                "weight": 1,
                "dimensions": {
                    "width": 6,
                    "height": 8,
                    "depth": 1
                }
            },
            "_rid": "I2YsALxG+-EBAAAAAAAAAA==",
            "_self": "dbs/I2YsAA==/colls/I2YsALxG+-E=/docs/I2YsALxG+-EBAAAAAAAAAA==/",
            "_etag": "\"0000844e-0000-1a00-0000-5ca79f840000\"",
            "_attachments": "attachments/",
            "_ts": 1554489220
        }
    ]
    ```

1. 既存のクエリ ウィンドウ。productId の JSON ファイルに ID、製造元、および説明を返すクエリを記述する 

    ```SQL
    SELECT
        p.id,
        p.manufacturer,
        p.description
    FROM Products p
    WHERE p.id ="1"
    ```

1. [**Execute Query**] (クエリの実行) アイコンをクリックします。次の結果が返されます

    ```JSON
    [
    {
        "id": "1",
        "manufacturer": "Contoso Sport",
        "description": "Quick dry crew neck t-shirt"
    }
    ]
    ```

1. 既存のクエリ ウィンドウで、価格順に並べ替えられたすべての製品の価格、説明、および製品 ID を昇順に返すクエリを記述します。

    ```SQL
    SELECT p.price, p.description, p.productId
    FROM Products p
    ORDER BY p.price ASC
    ```

1. [**Execute Query**] (クエリの実行) アイコンをクリックします。次の結果が返されます

    ```JSON
    [
        {
            "price": "14.99",
            "description": "Quick dry crew neck t-shirt",
            "productId": "33218896"
        },
        {
            "price": "49.99",
            "description": "Black wool pea-coat",
            "productId": "33218897"
        }
    ]
    ```

### タスク 4: データに対して複雑な操作を実行する

1. Azure portal の [**ドキュメント**] 画面で、[**New Stored Procedure**] (新規ストアド プロシージャ) ボタンをクリックします。

    > **注記**: サンプルのストアド プロシージャを示す新しいストアド プロシージャ画面が表示されます。

1. [新規ストアド プロシージャ] 画面で、[ **ストアド プロシージャ ID]** テキスト ボックスに「**createMyDocument**」と入力します。 

1. 次のコードを使用して、ストアド プロシージャ本体にストアド プロシージャを作成します。

    ```Javascript
    function createMyDocument() {
        var context = getContext();
        var collection = context.getCollection();

        var doc = {
            "id": "3",
            "productId": "33218898",
            "description": "Contoso microfleece zip-up jacket",
            "price": "44.99"
        };

        var accepted = collection.createDocument(collection.getSelfLink(),
            doc,
            function (err, documentCreated) {
                if (err) throw new Error('Error' + err.message);
                context.getResponse().setBody(documentCreated)
            });
        if (!accepted) return;
}
    ```

1. [新規ストアド プロシージャ] 画面で、[**保存**] をクリックします。 

1. [新規ストアド プロシージャ] 画面で、[**実行**] をクリックします。 

1. [入力パラメーター] 画面で、[**パーティションキー値**] テキスト ボックスに「**33218898**」と入力し、[**実行**] をクリックします。

次の結果が返されます

    ```JSON
    {
        "id": "3",
        "productId": "33218898",
        "description": "Contoso microfleece zip-up jacket",
        "price": "44.99",
        "_rid": "I2YsALxG+-EDAAAAAAAAAA==",
        "_self": "dbs/I2YsAA==/colls/I2YsALxG+-E=/docs/I2YsALxG+-EDAAAAAAAAAA==/",
        "_etag": "\"0000874e-0000-1a00-0000-5ca7a7050000\"",
        "_attachments": "attachments/"
    }
    ```

1. Azure portal の [**ドキュメント**] 画面で、ドロップダウン ボタンの [**New Stored Procedure**](新規ストアド プロシージャ)をクリックし、[**新しい UDF**] をクリックします。

    > **注記**: **function userDefinedFunction(){}** を示す新しい UDF 1 画面が表示されます。

1. [新規ストアド プロシージャ] 画面で、[**User Defined Function Id**](ユーザー定義関数 ID) テキスト ボックスに「**producttax**」と入力します。

1. 次のコードを使用して、ストアド プロシージャ本体にストアド プロシージャを作成します。

    ```Javascript
    function producttax(price) {
        if (price == undefined) 
            throw 'no input';

        var amount = parseFloat(price);

        if (amount < 1000) 
            return amount * 0.1;
        else if (amount < 10000) 
            return amount * 0.2;
        else
            return amount * 0.4;
    }
    ```

1. [新規 UDF 1] 画面で、[**保存**] をクリックします。

1. [クエリ 1] タブをクリックし、既存のクエリを次のクエリに置き換えます。

    ```SQL
    SELECT c.id, c.productId, c.price, udf.producttax(c.price) AS producttax FROM c
    ```

1. [クエリ 1] 画面で、[**Execute Query**](クエリの実行) をクリックします。 

次の結果が返されます

    ```JSON
    [
        {
            "id": "1",
            "productId": "33218896",
            "price": "14.99",
            "producttax": 1.499
        },
        {
            "id": "2",
            "productId": "33218897",
            "price": "49.99",
            "producttax": 4.9990000000000005
        },
        {
            "id": "3",
            "productId": "33218898",
            "price": "44.99",
            "producttax": 4.4990000000000005
        }
    ]
    ```

## エクササイズ 3: Visual Studio Code で Azure Cosmos DB 用の .NET コア アプリを構築する

所要時間: 45 分

個別エクササイズ

このエクササイズの主なタスク:

1. Visual Studio Code で Azure Cosmos DB リソースを有効にする

1. Visual Studio Code でアプリケーションをセットアップする

1. プログラムによる NoSQL データの作成、読み取り、更新、および削除を実行する

1. Azure Cosmos DB .NET Core SDK を使用してクエリを実行する

1. アプリケーションからストアド プロシージャを作成および実行する

### タスク 1: Visual Studio Code で Azure Cosmos DB リソースを有効にする

1. Visual Studio Code を開きます。

1. 左側のメニューで、拡張機能ボタンをクリックします。

1. [マーケットプレースの検索拡張機能] テキスト ボックスに、「**Cosmos DB**」と入力し、[**Azure Cosmos DB**] をクリックします。ドキュメントが Visual Studio Code に表示されたら、[**インストール**] をクリックします。

    > **注記**: 拡張機能のインストール中に移動バーが表示されます。インストールが完了すると、[インストール済み] の横にチェックマークが表示されます。

1. インストールが完了したら、[**Reload**] (再読み込み) をクリックします。

1. [マーケットプレースの検索拡張機能] テキスト ボックスに、「**Azure Account**」と入力し、[**Azure アカウント拡張機能**] をクリックします。ドキュメントが Visual Studio Code に表示されたら、[**インストール**] をクリックします。

    > **注記**: 拡張機能のインストール中に移動バーが表示されます。インストールが完了すると、[インストール済み] の横にチェックマークが表示されます。

1. インストールが完了したら、[**Reload**] (再読み込み) をクリックします。

1. Visual Studio Code で、[**教示**]、[**コマンド パレット**] をクリックし、「**Azure: Sign In**」と入力します。

    > **注記**: Web ブラウザのプロンプトに従って、Visual Studio Code セッションを認証するアカウントを選択します。ブラウザにメッセージが表示され、サインインしていることが確認されます。このタブを閉じることができます。

1. Visual Studio Code で、左側のメニューの [**Azure アイコン** ] をクリックし、[Cosmos DB] の [サブスクリプション] を右クリックし、[**アカウントの作成**] をクリックします。   

1. Visual Studio Code に、[**フォルダを開く**] ダイアログ ボックスが表示されます。 

1. 選択した場所に **learning-module** という名前の新しいフォルダーを作成し、[**フォルダーを選択**] をクリックします。   

    > **注記**: この時点で、作業フォルダーの設定時に Visual Studio Code が再起動する可能性があります。その結果、ラボのドキュメントを再度開く必要があります。

1. Visual Studio Code で、左側のメニューの **Azure アイコン** をクリックし、[**Cosmos DB**] の [**サブスクリプション**] を右クリックし、[**アカウントの作成**] をクリックします。       

1. 画面上部の [ **新しい Cosmos DB アカウントを作成**] という名前のテキスト ボックスに、 **xxcosmos**(xx は自分のイニシャル) という名前の Azure Cosmos DB アカウントの一意の名前を入力し、キーボードの **Enter** を押します。   

1. 次に、[**SQL(DocumentDB) **] を選択し、**awrgstudxx** リソース グループを選択して、最も近い **場所** を選択します。   

    > **注記**: Visual Studio Code の下部に「Creating Cosmos DB Account...」(Cosmos DB アカウントを作成中...) というバーが表示されます。所要時間は約 5 分です。バーが変わり、作成が正常に行われたことを示します。

1. アカウントが作成された後、Azure で Azure サブスクリプションを展開します。Cosmos DB ウィンドウと拡張機能には、新しい Azure Cosmos DB アカウントが表示されます。

1. 新しいアカウントを右クリックし、[**データベースの作成**] をクリックします。 

1. 画面上部の入力パレットで、データベース名の [**ユーザー**] を入力し、**Enter** を押します。

1. コレクション名の [**WebCustomers**] を入力し、 **Enter** を押します。   

1. パーティション キーの [** userId**] を入力し、**Enter** を押します。

1. 最後に、最初のスループット容量が **1000** であることを確認し、 **Enter** を押します。   

1. Azure でアカウントを展開します。Cosmos DB ウィンドウ、新しいユーザー データベース、WebCustomers コレクションが表示されます。

### タスク 2: Visual Studio Code でアプリケーションをセットアップする

1. [**ファイル**] メニューをクリックし、[空の場合は **自動保存**] をオンにして、ファイルの自動保存が有効になっていることを確認します。複数のブロックのコードでコピーし、常に最新のファイルに対して操作していることを確認します。

1. メインメニューから [**表示**]、[**ターミナル**] を選択して、Visual Studio Code から統合ターミナルを開きます。   

1. ターミナル ウィンドウをクリックし、キーボードの **Enter** を押し、次のコマンドをコピーして貼り付けます。 

    ```bash
    dotnet new console
    ```

    > **注記**: このコマンドは、 **learning-module** フォルダーに Program.cs ファイルを作成します。基本的な "Hello World" プログラムが既に書き込まれているほか、learning-module.csproj という名前の C# プロジェクト ファイルが作成されます。 

1. ターミナル ウィンドウで、次のコマンドをコピーして貼り付け、 **"Hello World!"** プログラムを実行します。 

    ```bash
    dotnet run
    ```

1. ターミナル プロンプトで、次のコマンド ブロックをコピーして貼り付け、必要な NuGet パッケージをインストールします。

    ```bash
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package System.Configuration.ConfigurationManager
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet restore
    ```

1. ターミナル画面はパッケージを読み込み、**dotnet restore** の最後にコマンドが表示されます。ターミナル ウィンドウで **Enter** を押します。

1. エクスプローラ ウィンドウの上部にある [**Program.cs**] をクリック してファイルを開きます。**using System** の後に次の using ステートメントを追加します。 

    ```C#
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

> **重要**: 必要となる不足アセットの追加に関するメッセージが表示されるまで、約 15 秒間待ち、[**はい**] をクリックします。

1. learning-module フォルダーで、**App.config** という名前の新しいファイルを作成し、次のコードを追加します。

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. 左側の **Azure**  アイコンをクリックしてサブスクリプションを展開し、 **新しい Azure Cosmos DB アカウントを右クリック** してから [**接続文字列のコピー**] をクリックして、接続文字列をコピーします。     

1. 接続文字列を App.config ファイルの末端に貼り付け、接続文字列から **AccountEndpoint** 部分を App.config の **accountEndpoint** 値にコピーします。

1. 次に、接続文字列から **AccountKey**   値を **accountKey** 値にコピーし、コピーした **元の接続文字列を削除** します。

1. App.config ファイルは最終的に次のようになります。

    ```XML
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="https://my-account.documents.azure.com:443/" />
            <add key="accountKey" value="6e7sRxunccGEeO7IVlMdeFt5BdsllfSGLYc28KyjzkESiCu7tfWbTaZXAErt2v88gOcMbOYgwp1q4NYDifD7ew==" />
          </appSettings>
    </configuration>
    ```

1. ターミナル プロンプトで、次のコマンドをコピーして貼り付け、プログラムを実行します。

    ```bash
    dotnet run
    ```

    > **注記**: プログラムは、ターミナルに「Hello World!」と表示します。

1. Explorer  ウィンドウで、[Program.cs] をクリックしてファイルを開きます。プログラム クラスの先頭に次を追加します。

    ```C#
    private DocumentClient client;
    ```

1. 新しい非同期タスクを追加して新しいクライアントを作成し、Main メソッドの後に次のメソッドを追加して、Users データベースが存在するかどうかを確認します。

    ```C#
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、コードが確実に実行されるようにします。「Hello World!」がコンソールに返されます。

    ```bash
    dotnet run
    ```

1. 次のコードを Main メソッドにコピーして貼り付け、現在の **Console.WriteLine ("Hello World!")** コードを上書きします。

    ```C#
    try
    {
        Program p = new Program();
        p.BasicOperations().Wait();
    }
    catch (DocumentClientException de)
    {
        Exception baseException = de.GetBaseException();
        Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
    }
    catch (Exception e)
    {
        Exception baseException = e.GetBaseException();
        Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
    }
    finally
    {
        Console.WriteLine("End of demo, press any key to exit.");
        Console.ReadKey();
    }
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```bash
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

>**結果** このエクササイズでは、Azure Cosmos DB に接続できるクライアント サイド アプリケーションを作成しました。

### タスク 3: プログラムによる NoSQL データの作成、読み取り、更新、および削除を実行する

#### ドキュメントを作成する

1. Azure Cosmos DB に格納するオブジェクトを表す **ユーザー** クラスを作成します。  また、**ユーザー** 内で使用される **OrderHistory** クラスと **Shippreference** クラスも作成します。ドキュメントには、ID プロパティが JSON の ID としてシリアル化されている必要があります。

1. これらのクラスを作成するには、次の**ユーザー**、**OrderHistory**、**ShippingPreference**、および **CouponsUsed** クラスをコピーして、**BasicOperations** メソッドの下に貼り付けます。

    ```C#
    public class User
    {
        [JsonProperty("id")]
        public string Id { get; set; }
        [JsonProperty("userId")]
        public string UserId { get; set; }
        [JsonProperty("lastName")]
        public string LastName { get; set; }
        [JsonProperty("firstName")]
        public string FirstName { get; set; }
        [JsonProperty("email")]
        public string Email { get; set; }
        [JsonProperty("dividend")]
        public string Dividend { get; set; }
        [JsonProperty("OrderHistory")]
        public OrderHistory[] OrderHistory { get; set; }
        [JsonProperty("ShippingPreference")]
        public ShippingPreference[] ShippingPreference { get; set; }
        [JsonProperty("CouponsUsed")]
        public CouponsUsed[] Coupons { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class OrderHistory
    {
        public string OrderId { get; set; }
        public string DateShipped { get; set; }
        public string Total { get; set; }
    }

    public class ShippingPreference
    {
        public int Priority { get; set; }
        public string AddressLine1 { get; set; }
        public string AddressLine2 { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string ZipCode { get; set; }
        public string Country { get; set; }
    }

    public class CouponsUsed
    {
        public string CouponCode { get; set; }

    }

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

1. 次に、Program.cs ファイルの末端にある **WriteToConsoleAndPromptToContinue** メソッドの下にある **CreateUserDocumentIfNotExists** タスクをコピーして貼り付けます。

    ```C#
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("User {0} already exists in the database", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 次に、**BasicOperations** メソッドに戻り、その最後に次の値を追加します。

    ```C#
    User yanhe = new User
    {
        Id = "1",
        UserId = "yanhe",
        LastName = "He",
        FirstName = "Yan",
        Email = "yanhe@contoso.com",
        OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
            ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);

    User nelapin = new User
    {
        Id = "2",
        UserId = "nelapin",
        LastName = "Pindakova",
        FirstName = "Nela",
        Email = "nelapin@contoso.com",
        Dividend = "8.50",
        OrderHistory = new OrderHistory[]
        {
            new OrderHistory {
                OrderId = "1001",
                DateShipped = "08/17/2018",
                Total = "105.89"
            }
        },
            ShippingPreference = new ShippingPreference[]
        {
            new ShippingPreference {
                    Priority = 1,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            },
            new ShippingPreference {
                    Priority = 2,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            }
        },
        Coupons = new CouponsUsed[]
        {
            new CouponsUsed{
                CouponCode = "Fall2018"
            }
        }
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

#### ドキュメントを読む

1. データベースからドキュメントを読み取るには、次のコードでコピーし、Program.cs ファイルの **WriteToConsoleAndPromptToContinue** メソッドの後に配置します。

    ```C#
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("Read user {0}", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not read", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 次のコードを、「**await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);** 行の後、BasicOperations メソッドの最後にコピーして貼り付けます。

    ```C#
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

#### ドキュメントを置換する

1. Program.cs ファイルの **ReadUserDocument** メソッドの後に **ReplaceUserDocument** メソッドをコピーして貼り付けます。

    ```C#
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) });
            this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser.LastName);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for replacement", updatedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 次のコードを、**await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);** 行の後、**BasicOperations** メソッドの最後にコピーして貼り付けます。

    ```C#
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
        Database and collection validation complete
        User 1 already exists in the database
        Press any key to continue ...
         User 2 already exists in the database
        Press any key to continue ...
         Replaced last name for Suh
        Press any key to continue ...
         Read user 1
        Press any key to continue ...
         End of demo, press any key to exit
    ```

#### ドキュメントを削除する

1. **ReplaceUserDocument** メソッドの下に **DeleteUserDocument** メソッドをコピーして貼り付けます。

    ```C#
    private async Task DeleteUserDocument(string databaseName, string collectionName, User deletedUser)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, deletedUser.Id), new RequestOptions { PartitionKey = new PartitionKey(deletedUser.UserId) });
            Console.WriteLine("Deleted user {0}", deletedUser.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for deletion", deletedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. 次のコードを **BasicOperations** メソッドの最後にコピーして貼り付けます。 

    ```C#
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
    Database and collection validation complete
    User 2 already exists in the database
    Press any key to continue ...
        User 2 already exists in the database
    Press any key to continue ...
        Replaced last name for Suh
    Press any key to continue ...
        Read user 1
    Press any key to continue ...
        Deleted user 1
    End of demo, press any key to exit.
    ```

### タスク 4: Azure Cosmos DB .NET Core SDK を使用してクエリを実行する

1. 次のサンプルは、.NET コードから SQL、LINQ、または LINQ ラムダでクエリを実行する方法を示しています。コードをコピーし、Program.cs ファイルの末端に向かって **private async Task CreateUserDocumentIfNotExists** の後に追加します。

    ```C#
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1, EnableCrossPartitionQuery = true };

        // Here we find nelapin via their LastName
        IQueryable<User> userQuery = this.client.CreateDocumentQuery<User>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(u => u.LastName == "Pindakova");

        // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (User user in userQuery)
        {
            Console.WriteLine("\tRead {0}", user);
        }

        // Now execute the same query via direct SQL
        IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM User WHERE User.lastName = 'Pindakova'", queryOptions );

        Console.WriteLine("Running direct SQL query...");
        foreach (User user in userQueryInSql)
        {
                Console.WriteLine("\tRead {0}", user);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. 次のコードを、BasicOperations メソッドの「**await this.DeleteUserDocument("Users", "WebCustomers", yanhe);**」行の後にコピーして貼り付けます。 

    ```C#
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
     User 2 already exists in the database
    Press any key to continue ...
     Replaced last name for Suh
    Press any key to continue ...
     Read user 1
    Press any key to continue ...
     Running LINQ query...
            Read {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    Running direct SQL query...
            Read {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    Press any key to continue ...
     Deleted user 1
    End of demo, press any key to exit.
    ```

### タスク 5: アプリケーションからストアド プロシージャを作成および実行する

1. Visual Studio Code 内の **Azure** で次の操作を行います。**Cosmos DB タブ**で、**Azure Cosmos DB アカウント**、 **ユーザー**、および **Web Customers** を展開し、[**ストアド プロシージャ**] を右クリックして [**ストアド プロシージャの作成**] をクリックします。        

1. 画面の上部にあるテキスト ボックスで、**UpdateOrderTotal** と入力して Enter を押し、ストアド プロシージャに名前を付けます。 

    > **注記**: 既定では、最初の項目を取得するストアド プロシージャが提供されます。提供されない場合は、次のステップを実行します。

1. **Azure** で次の操作を行います。**Cosmos DB タブ** で、**ストアド プロシージャ** を展開し、[**UpdateOrderTotal**] をクリックします。    

1. アプリケーションからこの既定のストアド プロシージャを実行するには、**Program.cs** ファイルに次のコードを **クラス プログラム** の後の最初のエントリとして追加します。

    ```C#
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
        Console.WriteLine("Stored procedure complete");
    }
    ```

1. 次のコードをコピーし、BasicOperations メソッドの「await this.DeleteUserDocument("Users", "WebCustomers", yanhe); 」行の前に貼り付けます。

    ```C#
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. 統合ターミナルで、次のコマンドを再びコピーして貼り付けてプログラムを実行し、確実に実行されるようにします。

    ```bash
    dotnet run
    ```

1. 次の結果が表示されます

    ```text
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
     User 2 already exists in the database
    Press any key to continue ...
     Replaced last name for Suh
    Press any key to continue ...
     Read user 1
    Press any key to continue ...
     Running LINQ query...
            Read {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    Running direct SQL query...
            Read {"id":"2","userId":"nelapin","lastName":"Pindakova","firstName":"Nela","email":"nelapin@contoso.com","dividend":"8.50","OrderHistory":[{"OrderId":"1001","DateShipped":"08/17/2018","Total":"105.89"}],"ShippingPreference":[{"Priority":1,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"},{"Priority":2,"AddressLine1":"505 NW 5th St","AddressLine2":null,"City":"New York","State":"NY","ZipCode":"10001","Country":"USA"}],"CouponsUsed":[{"CouponCode":"Fall2018"}]}
    Press any key to continue ...
     Stored procedure complete
    Deleted user 1
    End of demo, press any key to exit.
   ```

>**結果** このエクササイズでは、Azure Cosmos DB に接続する Visual Studio Code を設定して、コンソール アプリケーションをゼロから構築しました。次に、プログラムで NoSQL データを作成、読み取り、更新、および削除する .Net コードを作成しました。次に、Cosmos DB を照会するコードを追加し、Cosmos DB に対して動作するストアド プロシージャなどのプログラミング オブジェクトを作成する方法を学習しました。

## エクササイズ 4: Azure Cosmos DB でデータをグローバルに配布する

所要時間: 15 分

個別エクササイズ

このエクササイズの主なタスク:

1. データを複数のリージョンに複製する

1. フェールオーバーの管理

### タスク 1: データを複数のリージョンに複製する

1. Microsoft Edge で、[**Data Explorer - Microsoft..**] のタブをクリックします。

1. 「接続エラー」のメッセージが表示されたら、[**更新**] ボタンをクリックします。 

1. [**awcdbstudxx - データ エクスプローラー**] ウィンドウで、[**データをグローバルに複製**] をクリックします。 

1. 世界地図上で、自分が居住する大陸のデータ センターの場所をシングル クリックし、[**保存**] をクリックします。 

>**注** 追加のデータ センターのプロビジョニングには約 7 分かかります。

### タスク 2: フェールオーバーの管理。

1. [**awcdbstudxx - データをグローバルに複製**] ウィンドウで、[**手動フェールオーバー**] をクリックします。 

1. [**リージョンの読み取り**] データセンターの場所をクリックし、[**OK**] をクリックします。   

>**注** 手動フェールオーバーには約 3 分かかります。

1. [**awcdbstudxx - データをグローバルに複製**] ウィンドウで、[**自動フェールオーバー**] をクリックします。

1. [自動フェールオーバー] 画面で、[**オン**] ボタンをクリックし、[**OK**] をクリックします。   

>**注** 自動フェールオーバーのプロビジョニングには約 3 分かかります。