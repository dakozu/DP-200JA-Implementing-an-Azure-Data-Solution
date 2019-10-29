---
lab:
    title: 'クラウドでのリレーショナル データ ストアの操作'
    module: 'モジュール 5: クラウドで関係データを扱う'
---

# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 5 - クラウドでのリレーショナル データ ストアの操作

**所要時間**: 75 分

**前提条件**: このラボのケース スタディは既に確認していることを前提としています。内容とラボを前提としています。モジュール 1：Azure for the Data Engineer のコースとラボも完了済みであることを前提としています。

**ラボ ファイル**: このラボのファイルは、_Allfiles\Labfiles\Starter\DP-200.5_のフォルダーにあります。

## ラボの概要

受講者は、Azure SQL Database と Azure SQL Data Warehouse をプロビジョニングし、作成されたインスタンスの 1 つに対してクエリを発行できます。また、SQL Data Warehouse をその他複数のデータ プラットフォーム テクノロジーと統合し、PolyBase を使用して 1 つのデータ ソースから Azure SQL Data Warehouse にデータを読み込むこともできます。

## ラボの目的
  
このモジュールを修了すると、次のことができるようになります:

1. Azure SQLデータベースを使用する
1. Azure Data Warehouse が説明できる
1. Azure SQL Data Warehouse の作成とクエリの実行
1. PolyBase を使用して Azure SQL Data Warehouse にデータを読み込める

## シナリオ
  
あなたは AdventureWorks のシニア データ エンジニアであり、チームと協力して、オンプレミスの SQL Server から Azure にあるリレーショナル データベースにリレーショナル データベース システムを移行します。まず、当社のサンプル データベースを使用して SQL Server のインスタンスを作成し、それをジュニア データ エンジニアに手渡し、部門データベースのテストを実行してもらいます。

次に、SQL Data Warehouse をプロビジョニングし、一連のクエリを使用してサンプル データベースをテストすることで、サーバーのプロビジョニングが成功したことを確認します。次に、PolyBase を使用して Azure BLOB および Azure Databricks からディメンション テーブルを読み込み、これらのデータ プラットフォーム テクノロジーと Azure SQL データ ウェアハウスが統合したことをテストします。

このラボを完了すると:

1. Azure SQLデータベースを使用する
1. Azure Data Warehouse が説明できる
1. Azure SQL Data Warehouse の作成とクエリの実行
1. PolyBase を使用して Azure SQL Data Warehouse にデータを読み込める

> **重要**: このラボを進めるにつれ、プロビジョニングまたは構成タスクで発生した問題を書き留め、_\Labfiles\DP-200-Issues-Docx_ にあるドキュメントの表に記録してください。ラボ番号を文書化し、テクノロジーを書き留め、問題とその解決を説明してください。このドキュメントは、後のモジュールで参照できるように保存します。

## エクササイズ 1: Azure SQLデータベースを使用する

所要時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. SQL データベース インスタンスを作成して構成する。

### タスク 1: SQL データベース インスタンスを作成して構成する。

1. Azure portal で、[**+ リソースを作成する**] ブレードに移動します。

1. [新規] ブレードで、[**マーケットプレースの検索**] テキスト ボックスに移動し、「**SQL Database**」という単語を入力します。表示される一覧の [**SQL Database**] をクリックします。

1. [**SQL Database**] ブレードで、[**作成**] をクリックします。 

1. [**SQL Database の作成**] ブレードから、次の設定を使用して Azure SQL Database を作成します。

    - Subscription (サブスクリプション): このラボで使用するサブスクリプションの名前

    - リソース グループ名: **awrgstudxx **(**xx** は自分のイニシャル)

    - データベース名: **DeptDatabasesxx** (**xx** は自分のイニシャル)

    - サーバー: 次の設定で新しいサーバーを作成し、[**選択**] をクリックします。 
        - サーバー名: **SQLServicexx** (**xx** は自分のイニシャル)
        - サーバー管理者ログイン: **xxsqladmin**(**xx** は自分のイニシャル)
        - パスワード: **P@ssw0rd**
        - パスワードを確定する: **P@ssw0rd**
        - 場所: 近くの **場所** を選択します。 
        - Azure サービスがサーバーにアクセスできるようにする: **オンにする**

    - [**追加設定**] タブの [**データソース**] で、[**サンプル**] をクリックします。     

    - 残りの設定は既定のままにしておきます

1. **[SQL Database の作成]*** ブレードで、[**レビュー + 作成**] をクリックします。  

1. **[SQL Database の作成***] ブレードの検証後、[**作成**] をクリックします。

   > **注記**: プロビジョニングの所要時間は約 4 分です。

> **結果**: このエクササイズを完了すると、Azure SQL データベース インスタンスが作成されます。

## エクササイズ 2: Azure Data Warehouse を説明する
  
所要時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. SQL Data Warehouse インスタンスを作成して構成する。

1. サーバー ファイアウォールを構成する

### タスク 1: SQL Data Warehouse インスタンスを作成して構成する。

1. Azure portal で、[**+ リソースを作成する**] ブレードに移動します。

1. [新規] ブレードで、[**マーケットプレースの検索**] テキスト ボックスに移動し、「**SQL Data**」という単語を入力します。表示される一覧の [**SQL Database Warehouse**] をクリックします。

1. [**SQL Data Warehouse**] ブレードで、[**作成**] をクリックします。

1. [**SSQL Data Warehouse**] ブレードから、次の設定を使用して Azure SQL Database を作成します。

    - データベース名: **Warehousexx** (**xx** は自分のイニシャル)

    - Subscription (サブスクリプション): このラボで使用するサブスクリプションの名前

    - リソース グループ名: **awrgstudxx **(**xx** は自分のイニシャル)

    - ソースを選択: **サンプル**

    - サンプルを選択: **AdventureWorksDW**

    - サーバー: **SQLServicexx**

    - パフォーマンス レベル: **Gen1 DW200**

1. **[SQL Data Warehouse*** ] ブレードで、[**作成**] をクリックします。

   > **注記**: プロビジョニングの所要時間は約 4 分です。

### タスク 2: サーバー ファイアウォールを構成する

1. Azure portal 内のブレードで、**[Resource groups]**(リソース グループ)、**[awrgstudxx]** の順にクリックし、**[awdlsstudxx]** をクリックします (**xx** は自分のイニシャル)。

1. **sqlservicexx** (**xx** は自分のイニシャル) をクリックします。

1. [**sqlservicexx**] 画面で、[**ファイアウォールと仮想ネットワーク**] をクリックします。 

1. [sqlservicexx - ファイアウォールと仮想ネットワーク] 画面で、オプション [** + クライアント IP の追加**] をクリックし、[**保存**] をクリックします。

    > **注記**: サーバー ファイアウォール ルールが正常に更新されたことを示すメッセージが表示されます。

> **結果**: このエクササイズを完了すると、Azure SQL Data Warehouse インスタンスを作成し、サーバー ファイアウォールを構成して、それに対する接続を有効にします。

## エクササイズ 3: Azure SQL Data Warehouse を作成する

所要時間: 25 分

個別エクササイズ

このエクササイズの主なタスク:

1. SQL Server Management Studio をインストールし、SQL Data Warehouse インスタンスに接続する。

1. SQL Data Warehouse データベースを作成する

1. SQL Data Warehouse テーブルを作成する

    > **注記**: Transact-SQL に慣れていない場合は、次の場所 (**Allfiles\Labfiles\Starter\DP-200.5\SQL DW Files**) ラボにあるステートメントを使用することができます。

### タスク 1: SQL Server Management Studio をインストールし、SQL Data Warehouse インスタンスに接続する。

1. Azure Portal で、 [**sqlservicexx - ファイアウォールと仮想ネットワーク**] のブレードで [**プロパティ**] をクリックします。

1. **サーバー名** をコピーして メモ帳 に貼り付けます。

1. [SQL Server Management Studio](https://docs.microsoft.com/ja-jp/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) をダウンロードし、コンピューターにインストールします

1. Windows デスクトップで [**スタート**]をクリックし、**「SQL Server」** と入力し、[**Microsoft SQL Server Management Studio 17**] をクリックします。

1. [**Connect to Server**] (サーバーに接続) ダイアログ ボックスで、次の詳細情報を入力します。
    - サーバー名: **sqlservicexx.database.windows.net**
    - 認証: **SQL Server の認証**
    - ユーザー名: **xxsqladmin**
    - パスワード: **P@ssw0rd**

1. [**Connect to Server**] (サーバーに接続) ダイアログ ボックスで、[**Connect**] (接続) をクリックします。 

### タスク 2: SQL Data Warehouse データベースを作成する。

1. **SQL Server Management Studio** の Object Explorer で、**sqlservicexx.database.windows.net** を右クリックし、[**New Query**] (新しいクエリ) をクリックします。 

1. クエリ ウィンドウで、**DWDB** のという名前の DataWarehouse データベースを作成し、サービス目標を DW100 に、最大サイズを 1024 GB に設定します。

    ```SQL
    CREATE DATABASE DWDB COLLATE SQL_Latin1_General_CP1_CI_AS
    (
        EDITION 			= 'DataWarehouse'
    ,	SERVICE_OBJECTIVE 	= 'DW100'
    ,	MAXSIZE 			= 1024 GB
    );
    ```

    > **注記**: データベースの作成には約 2 分かかります。

1. [**awdlsstudxx**] ブレードで [**アクセス キー**] をクリックし、[**ストレージアカウント名**] の横にあるコピー アイコンをクリックして メモ帳 に貼り付けます。

### タスク 3: SQL Data Warehouse テーブルを作成する。

1. **SQL Server Management Studio** の Object Explorer で、**sqlservicexx.database.windows.net** を右クリックし、[**New Query**] (新しいクエリ) をクリックします。

1. 次の列に **replicate** の分散を持つ **クラスター化された columnstore** インデックスを有する **dbo.Users** という名前のテーブルを作成します。

    | 列名 | データ型 | NULL 値の許容|
    |-------------|-----------|------------|
    | userId | int | NULL|
    | 都市 | nvarchar(100) | NULL|
    | リージョン | nvarchar(100) | NULL|
    | 国 | nvarchar(100) | NULL|

1. **SQL Server Management Studio** で、[**Execute**] (実行) をクリックします。

1. **SQL Server Management Studio** の Object Explorer で、**sqlservicexx.database.windows.net** を右クリックし、[**New Query**] (新しいクエリ) をクリックします。

1. 次の列に **ラウンド ロビン** の分散を持つ **クラスター化された columnstore** インデックスを有する **dbo.Products** という名前のテーブルを作成します。

    | 列名 | データ型 | NULL 値の許容|
    |-------------|-----------|------------|
    | Productid | int | NULL|
    | EnglishProductName | nvarchar(100) | NULL|
    | 色 | nvarchar(100) | NULL|
    | StandardCost | int | NULL|
    | ListPrice | int | NULL|
    | サイズ | nvarchar(100) | NULL|
    | 重量 | int | NULL|
    | DaysToManufacture | int | NULL|
    | クラス | nvarchar(100) | NULL|
    | Style (スタイル) | nvarchar(100) | NULL|

1. **SQL Server Management Studio** で、[**Execute**] (実行) をクリックします。

1. **SQL Server Management Studio** の Object Explorer で、**sqlservicexx.database.windows.net** を右クリックし、[**New Query**] (新しいクエリ) をクリックします。

1. 次の列の **SalesUnit** に **Hash** の分散を持つ **クラスター化された columnstore** を有する **dbo.FactSales** という名前のテーブルを作成します。

    | 列名 | データ型 | NULL 値の許容|
    |-------------|-----------|------------|
    | DateId | int | NULL|
    | ProductId | int | NULL|
    | UserId | int | NULL|
    | UserPreferenceId | int | NULL|
    | SalesUnit | int | NULL|

1. **SQL Server Management Studio** で、[**Execute**] (実行) をクリックします。

> **結果**: このエクサ細部を完了すると、SQL Server Management Studio をインストールして、DWDB という名前のデータ ウェアハウスと、Users、Products、FactSales という名前の 3 つのテーブルが作成されます。

## エクササイズ 4: PolyBase を使用して Azure SQL Data Warehouse にデータを読み込む

所要時間: 10 分

個別エクササイズ

このエクササイズの主なタスク:

1. Azure BLOB コンテナーとキーの詳細を収集する

1. Azure BLOB から PolyBase を使用し、dbo.Dates テーブルを作成する

1. Azure Databricks から PolyBase を使用し、dbo.Preferences テーブルを作成する

### タスク 1: Azure BLOB アカウントとキーの詳細を収集する

1. Azure portal で、**リソース グループ** をクリック し、**awrgstudxx** をクリックし、**awsastudxx** をクリックします (xx が名前のイニシャル)。

1. [**awsastudxx**] 画面で、[**アクセス キー**] をクリックします。[**ストレージ アカウント名**] の横にあるアイコンをクリックし、メモ帳 に貼り付けます。 

1. [**awsastudxx - アクセス キー**] 画面の [**key1**] で、[**キー**] の横にあるアイコンをクリックし、メモ帳 に貼り付けます。     

### タスク 2: Azure BLOB から PolyBase を使用し、dbo.Dates テーブルを作成する

1. **SQL Server Management Studio** の Object Explorer で、**sqlservicexx.database.windows.net** を右クリックし、[**New Query**] (新しいクエリ) をクリックします。

1. **DWDB** データベースに対して **マスター キー** を作成します。

    ```SQL
    CREATE MASTER KEY;
    ```

1. 次の詳細を含む、**AzureStorageCredential** という名前のデータベース スコープの資格情報を作成します。
    - IDENTITY: **MOCID**
    - SECRET: **The access key of your storage account**

    ```SQL
    CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
    WITH
    IDENTITY = 'MOCID',
    SECRET = 'Your storage account key'
;
    ```

1. **SQL Server Management Studio** で、両方のステートメントをハイライトし、[**実行**] をクリック します。

1. **SQL Server Management Studio** の [クエリ] ウィンドウに、**AzureStorageCredential** を使用する **HADOOP** の種類で作成された BLOB ストレージ アカウントとデータ コンテナー用に **AzureStorage** という名前の外部データ ソースを作成するコードを入力します。

    ```SQL
    CREATE EXTERNAL DATA SOURCE AzureStorage
    WITH (
        TYPE = HADOOP,
        LOCATION = 'wasbs://data@awsastudxx.blob.core.windows.net',
        CREDENTIAL = AzureStorageCredential
    );
    ```

1. **SQL Server Management Studio** で、ステートメントをハイライトし、[**実行**] をクリック します。

    ```SQL
    CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
    WITH
    IDENTITY = 'MOCID',
    SECRET = 'Your Blob Storage key'
    ;
    ```

1. **SQL Server Management Studio** の [クエリ] ウィンドウに、formattype が **DelimitedText**、フィールド ターミネータが **コンマ** の **TextFile** という名前の外部ファイル形式を作成するコードを入力します。 

    ```SQL
    CREATE EXTERNAL FILE FORMAT TextFile
    WITH (
        FORMAT_TYPE = DelimitedText,
        FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
    );
    ```

1. **SQL Server Management Studio**で、ステートメントをハイライトし、[**実行**] をクリック します。

1. **SQL Server Management Studio** の [クエリ] ウィンドウに、**場所** がルート ファイル、データ ソースが **AzureStorage**、File-format が **TextFile** で次の列を有する **dbo.DimDate2External** という名前の外部テーブルを作成するコードを入力します。

    | 列名 | データ型 | NULL 値の許容|
    |-------------|-----------|------------|
    | 日付 | datetime2(3) | NULL|
    | DateKey | decimal(38, 0) | NULL|
    | MonthKey | decimal(38, 0) | NULL|
    | 月 | nvarchar(100) | NULL|
    | 四半期 | nvarchar(100) | NULL|
    | 年 | decimal(38, 0) | NULL|
    | Year-Quarter | nvarchar(100) | NULL|
    | Year-Month | nvarchar(100) | NULL|
    | Year-MonthKey | nvarchar(100) | NULL|
    | WeekDayKey| decimal(38, 0) | NULL|
    | WeekDay| nvarchar(100) | NULL|
    | Day Of Month| decimal(38, 0) | NULL|

    ```SQL
    CREATE EXTERNAL TABLE dbo.DimDate2External (
	[Date] datetime2(3) NULL,
	[DateKey] decimal(38, 0) NULL,
	[MonthKey] decimal(38, 0) NULL,
	[Month] nvarchar(100) NULL,
	[Quarter] nvarchar(100) NULL,
	[Year] decimal(38, 0) NULL,
	[Year-Quarter] nvarchar(100) NULL,
	[Year-Month] nvarchar(100) NULL,
	[Year-MonthKey] nvarchar(100) NULL,
	[WeekDayKey] decimal(38, 0) NULL,
	[WeekDay] nvarchar(100) NULL,
	[Day Of Month] decimal(38, 0) NULL
    )
    WITH (
        LOCATION='/',
        DATA_SOURCE=AzureStorage,
        FILE_FORMAT=TextFile
    );
    ```

1. **SQL Server Management Studio** で、ステートメントをハイライトし、[**実行**] をクリック します。

1. テーブルに対して select ステートメントを実行して、テーブルが作成されたことを確認します。

    ```SQL
    SELECT * FROM dbo.DimDate2External;
    ```

1. **SQL Server Management Studio** の [クエリ] ウィンドウに、**columnstore** インデックス、および**dbo.DimDate2External** テーブルからデータを読み込む **ラウンド ロビン** の **分散** を持つ **dbo.Dates** という名前のテーブルを作成する  **CTAS** ステートメントを入力します。         

    ```SQL
    CREATE TABLE dbo.Dates
    WITH
    (   
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    )
    AS
    SELECT * FROM [dbo].[DimDate2External];
    ```

1. **SQL Server Management Studio** で、ステートメントをハイライトし、[**実行**] をクリック します。
 
1. **SQL Server Management Studio** の [クエリ] ウィンドウに、**DateKey**、**Quarter**、**Month** 列の統計を作成するクエリを入力します。 

    ```SQL
    CREATE STATISTICS [DateKey] on [Dates] ([DateKey]);
    CREATE STATISTICS [Quarter] on [Dates] ([Quarter]);
    CREATE STATISTICS [Month] on [Dates] ([Month]);
    ```

1. テーブルに対して select ステートメントを実行して、テーブルが作成されたことを確認します。

    ```SQL
    SELECT * FROM dbo.Dates;
    ```
