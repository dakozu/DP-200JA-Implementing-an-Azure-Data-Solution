---
lab:
    title: 'Azure Databricks でのチーム ベースのデータ サイエンスの有効化'
    module: 'モジュール 3: Azure Databricks でのチーム ベースのデータ サイエンスの有効化'
---

# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 3 - Azure Databricks でのチーム ベースのデータ サイエンスの有効化

**所要時間**: 75 分

**前提条件**: このラボのケース スタディは既に確認していることを前提としています。内容とラボを前提としています。モジュール 1：Azure for the Data Engineer のコースとラボも完了済みであることを前提としています。

**ラボ ファイル**: このラボのファイルは、_Allfiles\Labfiles\Starter\DP-200.3_のフォルダーにあります。

## ラボの概要

このラボを修了すると、受講者は Azure Databricks をデータ サイエンス プロジェクトの支援に使用する理由を説明できるようになります。受講者は、プロビジョニングと Azure Databricks インスタンスを作成し、Data Lake Store Gen II ストアから簡単なデータ準備タスクを実行するために使用されるワークスペースを作成します。最後に、受講者は Azure Databricks を使用して変換のチュートリアルを実行します。

## ラボの目的
  
このモジュールを修了すると、次のことができるようになります:

1. Azure Databricks について説明する
1. Azure Databricks の操作
1. Azure Databricks でデータを読み取る
1. Azure Databricks を使用して変換を実行できる

## シナリオ
  
情報サービス (IS) 部門に対応して、このテクノロジーを使用する利点を列挙して、予測分析プラットフォームを構築するプロセスを開始します。情報サービス部門にはデータ サイエンティストが加わるので、新しいチーム メンバーが予測分析環境を利用できるようにしたいと考えています。

あなたは、Azure Databricks 環境を立ち上げてプロビジョニングし、既存の Data Lake Storage Gen II アカウントからデータを取り込むことで、サービス上で単純なデータ準備ルーチンを実行して、この環境が機能することをテストします。データ エンジニアは、データ サイエンティストがデータ準備演習を行うのを支援する必要があります。そのため、基本的な変換を実行するのに役立つノートブックを順を追って確認することが勧められています。

このラボを完了すると:

1. Azure Databricks について説明する
1. Azure Databricks の操作
1. Azure Databricks でデータを読み取る
1. Azure Databricks を使用して変換を実行できる

> **重要**: このラボを進めるにつれ、プロビジョニングまたは構成タスクで発生した問題を書き留め、_\Labfiles\DP-200-Issues-Docx_ にあるドキュメントの表に記録してください。ラボ番号を文書化し、テクノロジーを書き留め、問題とその解決を説明してください。このドキュメントは、後のモジュールで参照できるように保存します。

## エクササイズ 1: Azure Databricks について説明する

>**重要**: 最初に **エクササイズ 2** を実行し、エクササイズ 2 で Databricks クラスターの作成を開始した後(10 分間でプロビジョニング)にエクササイズ 1 に戻ります。 

所要時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. このコースでこれまでに学習した内容から、Azure Databricks が満たすデジタル トランスフォーメーション要件と、Azure Databricks の候補データ ソースを特定します。

1. インストラクターは、調査結果についてグループと話し合います。

### タスク 1: デジタル トランスフォーメーションと候補データ ソースを定義する。

1. ラボの仮想マシンから **Microsoft Word** を起動し、**Allfiles\Labfiles\Starter\DP-200.3** フォルダーからファイル  **DP-200-Lab03-Ex01.docx** を開きます。

1. このエクササイズのケース スタディとシナリオの概説に従って、**10 分間** でデジタル トランスフォーメーション要件と候補データ ソースの文書化を行います。

### タスク 2: 調査結果についてインストラクターと話し合う

1. インストラクターは、調査結果について話し合うためにグループ作業を中断させます。

> **結果**: このエクササイズを完了すると、Azure Databricks が満たすデジタル トランスフォーメーション要件と候補データ ソースを識別する Microsoft Word ドキュメントが作成されます。

## エクササイズ 2: Azure Databricks を使用する
  
所要時間: 20 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. リソース グループに Azure Databricks Premium 階層インスタンスを作成する。

1. Azure Databricks を開く

1. Databricks ワークスペースを起動し、Spark クラスターを作成する

### タスク 1: Azure Databricks インスタンスを作成して構成する。

1. Azure portal で、[**+ リソースを作成する**] ブレードに移動します。

1. [新規] ブレードで、[**マーケットプレースの検索**] テキスト ボックスに移動し、「**databricks**」という単語を入力します。表示される一覧の [**Azure Databricks**] をクリックします。

1. **[Azure Databricks]** ブレードで **[作成]** をクリックします。

1. [**Azure Databricks の作成**] ブレードから、次の設定を使用して最初のストレージ アカウントを作成します。

    - ワークスペース名: **awdbwsstudxx** (**xx** は自分のイニシャル)

    - Subscription (サブスクリプション): このラボで使用するサブスクリプションの名前

    - リソース グループ名: **awrgstudxx **(**xx** は自分のイニシャル)

    - 場所: ラボの場所に最も近い Azure リージョンの名前と、Azure VM をプロビジョニングできる場所。

    - 価格レベル: **Premium (+ ロールベースのアクセス制御)**。

    - 仮想ネットワークに Azure Databricks ワークスペースをデプロイする: **いいえ**。

1. **Azure Databricks サービス*** ブレードで、[**作成**] をクリックします。

1. **Azure Databricks の作成*** ブレードの検証後、[**作成**] をクリックします。

   > **注記**: プロビジョニングの所要時間は約 3 分です。Databricks Runtime は Apache Spark の上に構築され、Azure クラウド用にネイティブに構築されます。Azure Databricks は、インフラストラクチャの複雑性を完全に排除しており、データ インフラストラクチャのセットアップと構成に関する専門知識も必要ありません。プロダクション ジョブのパフォーマンスを気にするデータ エンジニアに対して、Azure Databricks は、I/O 層と処理層 (Databricks I/O) でさまざまな最適化を行い、より高速でパフォーマンスの高い Spark エンジンを提供します。

### タスク 2: Azure Databricks を開く。

1. Azure Databricks サービスが作成されたことを確認する。

1. Azure portal で、[**リソース グループ**] ブレードに移動します。

1. [リソース グループ] ブレードで、****awrgstudxx** リソース グループ (**xx** は自分のイニシャル) をクリックします。

1. [**awrgstudxx**] ブレードで、**awdbwsstudxx** (**xx** は自分のイニシャル) をクリックして、Azure Databricks を開きます。  Azure Databricks インスタンスが開きます。

### タスク 3: Databricks ワークスペースを起動し、Spark クラスターを作成する。

1. Azure portal の [**awdbwsstudxx**] ブレードで、[**ワークスペースの起動**] ボタンをクリックします。   

    > **注記**: Microsoft Edge の別のタブで、Azure Databricks ワークスペースにサインインします。

1. [**一般的なタスク**] で、[**新規クラスター**] をクリック します。   

1. [**クラスターの作成**] 画面の [新規クラスター] で、次の設定を使って　Databricks クラスターを作成し、[**クラスターの作成**] をクリックします。 

    - クラスター名: **awdbclstudxx** (**xx** は自分のイニシャル)   

    - クラスター モード: **Standard**

    - Databricks Runtime のバージョン: **Runtime: 5.1 (Scala 2.11、Spark 2.4.0)**

    - Python のバージョン: **3**

    - [アクティビティが **60 分** ない場合は修了する] チェック ボックスをオンにします。クラスターが使われていない場合にクラスターを終了するまでの時間 (分単位) を指定します。

    - 残りのオプションはすべて現在の設定のままにしておきます。

1. [**クラスターの作成**] 画面で、[**クラスターの作成**] をクリックし、Microsoft Edge 画面を開いたままにします。

> **注記**: グラフィカル ユーザー インターフェイスを使用して Spark クラスターの作成が簡略化されるため、Azure Databricks インスタンスの作成には約 10 分かかります。クラスターの作成中は、**状態** が [**保留中**] になります。クラスターが作成されると、[**実行中**] に変わります。

> **注記**: クラスターの作成中に、**エクササイズ 1に戻って実行します**。 

## エクササイズ 3: Azure Databricks でデータを読み取る

所要時間: 30 分

個別エクササイズ

このエクササイズの主なタスク:

1. Databricks クラスターが作成されたことを確認する。

1. Azure Data Lake Store Gen II アカウント名を収集する

1. Databricks インスタンスを有効にして、Data Lake Gen II Store にアクセスする。

1. Databricks Notebook を作成し、Data Lake Store に接続する。

1. Azure Databricks でデータを読み取る。

### タスク 1: Databricks クラスターの作成を確認する

1. Microsoft Edge に戻り、[**インタラクション クラスター**] で **awdbclstudxx** という名前のクラスター (**xx** は自分のイニシャル) の [状態] が [実行中] になっていることを確認します。

### タスク 2: Azure Data Lake Store Gen II アカウント名を収集する

1. Microsoft Edge で [Azure portal] タブをックリックし、 [**リソース グループ**] をクリックして、**awrgstudxx** をクリックし、**awdlsstudxx** をクリックします。**xx** がイニシャルとなります。

1. [**awdlsstudxx**] ブレードで [**アクセス キー**] をクリックし、[**ストレージアカウント名**] の横にあるコピー アイコンをクリックして メモ帳 に貼り付けます。     

### タスク 3: Databricks インスタンスを有効にして、Data Lake Gen II Store にアクセスする。

1. Microsoft Edge で、Azure portal があるタブをクリックし、ブレードで [**Azure Active Directory**] をクリックします。 

1. [**概要**]  ブレードで、[**アプリの登録**] をクリックします。

1. [**アプリの登録**] 画面で、[**+ 新規アプリの登録**] ボタンをクリックします。 

1. アプリケーションの登録画面で、**DLAccess** の **名前** を入力し、**リダイレクトURI（オプション）** セクションで、**ウェブ** が選択され、アプリケーションの値に **https://adventure-works.com/exampleapp** が入力されていることを確認します。値を設定したら、作成 を選択します。DLAccess 画面が表示されます。

1. **DLAccess** 登録アプリ画面で、**アプリケーション ID** と **テナント ID** をコピーしてメモ帳 にペーストします。 

1. **DLAccess** 登録済みアプリ画面で、 **証明書とシークレット** をクリックして、新しいクライアント シークレット をクリックします。

1. **DL アクセス キー** の **説明** を入力し、キーの **期間** を **1 年間** に指定します。完了したら、[**保存**] をクリックします。 

    >**重要**: **保存** をクリックすると、キーが表示されます。このキー値をノートパッドにコピーできるのは 1 度だけです。

1. [**アプリケーション キーの値**] をコピーして メモ帳 に貼り付けます。 

1. リソース グループにストレージ BLOB データ共同作成者のアクセス許可を割り当てます。Azure portal で、[**リソース グループ**] ブレードをクリックし、リソース グループ **awrgstudxx** (**xx** は自分のイニシャル) をクリックします。 

1. [**awrgstudxx**] ブレードで、[**アクセスの制御 (IAM)**] をクリックします。 

1. [**ロールの割り当てを追加**] で [**追加**] をクリックします。   

1. [**ロールの割り当てを追加**] 画面の [ロール] で、[**ストレージ BLOB データ 共同作成者**] を選択します。   

1. [**ロールの割り当てを追加**] 画面の [選択] で、[**DLAccess**] を選択し、[**保存**] をクリックします。

1. Azure portal のブレードで、[**Azure Active Directory**] をクリックし、**ロール** を入力します。ユーザー ロールである場合は、管理者以外がアプリケーションを登録できることを確認する必要があります。

1. [Azure Active Directory] ブレードで [**ユーザー設定**] をクリックし、[**アプリの登録**] 設定を確認します。   この値を設定できるのは管理者のみです。[はい] に設定すると、Azure AD テナント内の任意のユーザーがアプリを登録することができます。

1. [Azure Active Directory] ブレードで、[**プロパティ**] をクリックします。 

1. **ディレクトリ ID** の横にある [コピー] アイコンをクリックして、テナント ID を取得し、これを メモ帳 に貼り付けます。 

1. メモ帳 ドキュメントを、フォルダー **Allfiles\Labfiles\Starter\DP-200.3** に **DatabricksDetails.txt**として保存します。

### タスク 4: Databricks Notebook を作成し、Data Lake Store に接続する。

1. Microsoft Edge で、[**クラスター - Databricks**] タブ をクリックします。

    > **注記**: クラスターページが表示されます。

1. Microsoft Edge の左側にある [Azure Databricks] ブレードで、[**ワークスペース** の下] をクリックし、**ワークスペース** の横にあるドロップダウンをクリックし、[**作成**] をクリックして [**Notebook**] をクリックします。

1. [**Notebook の作成**] 画面で、 [名前] の横 に [**My Notebook**] を入力します。   

1. [**言語**] ドロップダウン リストの横にある [**Scala**] を選択します。   

1. 以前に作成したクラスターの名前がクラスターに表示されていることを確認し、[**作成**] をクリックします。

     > **注記**: これにより、「My  Notebook」 (Scala) というタイトルの Notebook が開きます。

1. Notebook のセル  **Cmd 1** で、次のコードをコピーし、セルに貼り付けます。 

    ```scala
    //Connect to Azure Data Lake Storage Gen2 account

    spark.conf.set("fs.azure.account.auth.type", "OAuth")
    spark.conf.set("fs.azure.account.oauth.provider.type", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
    spark.conf.set("fs.azure.account.oauth2.client.id.<storage-account-name>.dfs.core.windows.net", "<application-id>")
    spark.conf.set("fs.azure.account.oauth2.client.secret.<storage-account-name>.dfs.core.windows.net", "<authentication-key>")
    spark.conf.set("fs.azure.account.oauth2.client.endpoint.<storage-account-name>.dfs.core.windows.net", "https://login.microsoftonline.com/<tenant-id>/oauth2/token")
    ```

1. このコード ブロックでは、このコード ブロック内の **application-id**、**authentication-id**、**tenant-id**、**file-system-name** および **storage-account-name** のプレースホルダー値を、以前に収集した値で置き換えます。これらの値は メモ帳 に保持されます。         

1. Notebook 内の **Cmd 1** の下のセルで、[**Run**] (実行) アイコンをクリックし、[**Run Cell**] (セルの実行) をクリックします。 

    >**注 **"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx" というメッセージがセルの下部に表示されます。

### タスク 5: Azure Databricks でデータを読み取る。

1. Notebook で、**Cmd 1** セルの下部にマウスを移動し、**+** アイコンをクリックします。**Cmd2** という名前の新しいセルが表示されます。

1. Notebook のセル  **Cmd 2** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Read JSON data in Azure Data Lake Storage Gen2 file system

    val df = spark.read.json("abfss://<file-system-name>@<storage-account-name>.dfs.core.windows.net/preferences.json")
    ```

1. このコード ブロックでは、**file-system-name** を **data** という単語で、またこのコード ブロック内の**storage-account-name** プレースホルダー値を以前に収集した値で置き換え、メモ帳 に保持します。     

1. Notebook 内の **Cmd 1** の下のセルで、[**Run**] (実行) アイコンをクリックし、[**Run Cell**] (セルの実行) をクリックします。 

    >**注** Spark ジョブが実行されたことを示すメッセージ、"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx"がセルの下部に表示されます

1. Notebook で、**Cmd 1** セルの下部にマウスを移動し、**+** アイコンをクリックします。**Cmd2** という名前の新しいセルが表示されます。

1. Notebook のセル  **Cmd 3** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Show result of reading the JSON file
  
    df.show()
    ```

1. Notebook 内の **Cmd 1** の下のセルで、[**Run**] (実行) アイコンをクリックし、[**Run Cell**] (セルの実行) をクリックします。

    >**注 ** Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx" と表示されます。

1. Azure Databricks Notebook を開いたままにします

>**結果** このエクササイズでは、Azure Databricks が Azure Data Lake Store Gen II のデータにアクセスするためのアクセス許可を設定する上で必要なステップを実行しました。次に、scala を使用して Data Lake Store に接続し、データを読み取り、ユーザーの好みを示すテーブル出力を作成しました。

## エクササイズ 4: Azure Databricks を使用して変換を実行する

所要時間: 10 分

個別エクササイズ

このエクササイズの主なタスク:

1. データセットの特定の列を取得する

1. データセットで列名を変更する

1. コメントを追加する

1. 時間がある場合: その他の変換

### タスク 1: データセットの特定の列を取得する

1. Notebook で、**Cmd 1** セルの下部にマウスを移動し、**+** アイコンをクリックします。**Cmd2** という名前の新しいセルが表示されます。

1. Notebook のセル  **Cmd 4** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Retrieve specific columns from a JSON dataset in Azure Data Lake Storage Gen2 file system
    
    val specificColumnsDf = df.select("firstname", "lastname", "gender", "location", "page")
    specificColumnsDf.show()
    ```

1. Notebook 内の **Cmd 1** の下のセルで、[**Run**] (実行) アイコンをクリックし、[**Run Cell**] (セルの実行) をクリックします。 

    >**注 ** Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx" と表示されます。

### タスク 2: データセットで列名を変更する

1. Notebook で、**Cmd 1** セルの下部にマウスを移動し、**+** アイコンをクリックします。**Cmd2** という名前の新しいセルが表示されます。

1. Notebook のセル  **Cmd 5** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Rename the page column to bike_preference

    val renamedColumnsDF = specificColumnsDf.withColumnRenamed("page", "bike_preference")
    renamedColumnsDF.show()
    ```

1. Notebook 内の **Cmd 1** の下のセルで、[**Run**] (実行) アイコンをクリックし、[**Run Cell**] (セルの実行) をクリックします。 

    >**注 ** Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx" と表示されます。

### タスク 3: コメントを追加する

1. Notebook で、**Cmd 1** セルの下部にマウスを移動し、**+** アイコンをクリックします。**Cmd2** という名前の新しいセルが表示されます。

1. Notebook のセル  **Cmd 6** で、次のコードをコピーし、セルに貼り付けます。

    ```text
    このコードは、"データ" という名前の Data Lake Storage ファイル システムに接続し、そのデータ レイクに格納されている preferences.json ファイル内のデータを読み取ります。その後、データを取得するための単純なクエリが作成され、列 "page" が "bike_preference" に変更されます。
    ```

1. Notebook 内の **Cmd 6** の下のセルで、 **下向きの矢印** アイコンをクリックし、[**上へ移動**] をクリックします。    セルが Notebook の上部に表示されるまで、この手順を繰り返します。

1. Azure Databricks Notebook を開いたままにします

    >**注** この後のラボでは、このデータを別のデータ プラットフォーム テクノロジーにエクスポートする方法を検討します。

> **結果**: このエクササイズを完了すると、2 つのウェブログ ファイルを含む "data" という名前のファイル システムを有する awdlsstudxx という名前の Data Lake Gen II Storage アカウントが作成され、AdventureWorks のデータ サイエンティストがそれを使用できるようになります。

### タスク 4: 時間がある場合、またはコース レビューの終了語

このラボが早く終わった場合は、次のセクションのリンクを参照して、Azure の基本的な変換および高度な変換について学ぶことができます。

URL にアクセスできない場合は、ノートブックのコピーが _Allfiles\Labfiles\Starter\DP-200.3\Post Course Review_フォルダーにあります。

**基本的な変換**

1. ワークスペース内で、左側のコマンド バーを使用して、[**ワークスペース**] 、[**ユーザー**] を 選択し、 [**ユーザー名**] (家のアイコンのエントリ) を選択します。

1. ブレードが表示されるので、**名前の横にある下向きのシェブロン** を選択し、[**インポート**] を選択します。

1. [Notebooks のインポート] ダイアログ ボックスで、**下の URL** を選択し、次の URL に貼り付けます。 

```url
    https://github.com/MicrosoftDocs/mslearn-perform-basic-data-transformation-in-azure-databricks/blob/master/DBC/05.1-Basic-ETL.dbc?raw=true
```

1. [**インポート**] を選択します。

1. インポート後に **05.1-Basic-ETL** という名前のフォルダーが表示されます。  このフォルダーを選択します。

1. フォルダーには、**scala** または **python** を使用して基本的な変換を学習するために使用できる 1 つ以上のノートブックが含まれます。

ノートブック全体が完了するまで、ノートブック内の指示に従います。次に、残りのノートブックを順番に続けます。

- **01-Course-Overview-and-Setup** (01-コースの概要とセットアップ)  - このノートブックは、Databricks ワークスペースに関するものです。
- **02-ETL-Process-Overview** - (02-ETL プロセスの概要) このノートブックには、クエリ、大きなデータ ファイル、および結果の視覚化に役立つエクササイズが含まれています。
- **03-Connecting-to-Azure-Blob-Storage** - (03-Azure Blob Storage への接続) このノートブックでは、基本的な集計と結合を実行します。
- **04-Connecting-to-JDBC** - (04-JDBC への接続) このノートブックは、Databricks を使用してさまざまなソースからデータにアクセスするためのステップを示しています。
- **05-Applying-Schemas-to-JSON** - (05-スキーマから JSON への適用) このノートブックでは、DataFrames を使用して JSON と階層データを照会する方法を学習します。
- **06-Corrupt-Record-Handling** - (06-破損レコード処理) このノートブックでは、ADLS を作成し、Databricks DataFrames を使用してこのデータを照会して分析する方法を理解するのに役立つエクササイズが含まれています。
- **07-Loading-Data-and-Productionalizing** - (07-データの読み込みと運用化) ここでは、Databricks を使用して、Azure Data Lake Storage Gen2 のデータ ストアを照会および分析します。
- **Parsing-Nested-Data** - (ネストされたデータの解析) このノートブックはオプションのサブフォルダーにあり、後で自分で学習するためのサンプル プロジェクトが含まれています。

>[注] Solutions のサブフォルダー内に、該当するノートブックがあります。これらには、1 つ以上の課題を含むエクササイズ用の完了したセルを含みます。分からなくなったり、解決策を見たい場合は、これらを参照してください。

**高度な変換**

1. ワークスペース内で、左側のコマンド バーを使用して、[**ワークスペース**] 、[**ユーザー**] を 選択し、 [**ユーザー名**] (家のアイコンのエントリ) を選択します。

1. ブレードが表示されるので、**名前の横にある下向きのシェブロン** を選択し、[**インポート**] を選択します。

1. [Notebooks のインポート] ダイアログ ボックスで、**下の URL** を選択し、次の URL に貼り付けます。 

```url
    https://github.com/MicrosoftDocs/mslearn-perform-advanced-data-transformation-in-azure-databricks/blob/master/DBC/05.2-Advanced-ETL.dbc?raw=true
```

1. [**インポート**] を選択します。

1. インポート後に **05.2-Advanced-ETL** という名前のフォルダーが表示されます。このフォルダーを選択します。

1. フォルダーには、**scala** または **python** を使用して基本的な変換を学習するために使用できる 1 つ以上のノートブックが含まれます。

ノートブック全体が完了するまで、ノートブック内の指示に従います。次に、残りのノートブックを順番に続けます。

- **01-Course-Overview-and-Setup** (01-コースの概要とセットアップ)  - このノートブックは、Databricks ワークスペースに関するものです。
- **02-Common-Transformations** - (一般的な変換) このノートブックでは、Spark 組み込み関数を使用して一般的なデータ変換を実行します。
- **03-User-Defined-Functions** - (03-ユーザ定義関数) このノートブックでは、ユーザ定義関数を使用してカスタム変換を実行します。
- **04-Advanced-UDFs** - (04-高度な UDF) このノートブックでは、高度なユーザー定義関数を使用して複雑なデータ変換を実行します。
- **05-Joins-and-Lookup-Tables** - (05-結合とルックアップテーブル) このノートブックでは、テーブルに標準結合とブロードキャスト結合を使用する方法を学習します。
- **06-Database-Writes** - (06-データベース書き込み) このノートブックには、ETL ジョブから変換されたデータを格納し、多数のターゲット データベースにデータを並列に書き込むエクササイズが含まれています。
- **07-Table-Management** - (07-テーブル管理) ここでは、データ ストレージを最適化するために、マネージド テーブルとアンマネージド テーブルを処理します。
- **Custom-Transformations** - (カスタム変換) このノートブックはオプションサブフォルダーにあり、後で自分で学習するためのサンプル プロジェクトが含まれています。

>[注] Solutions のサブフォルダー内に、該当するノートブックがあります。これらには、1 つ以上の課題を含むエクササイズ用の完了したセルを含みます。分からなくなったり、解決策を見たい場合は、これらを参照してください。