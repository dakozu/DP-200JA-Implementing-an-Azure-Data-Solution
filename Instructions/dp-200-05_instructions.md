# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 5 - クラウドでのリレーショナル データ ストアの使用

**予想時間**: 75 分

**前提条件**: この課題のケース スタディは既に確認していることを前提としています。モジュール 1 のコンテンツとラボは次のとおりです：データ エンジニア向け Azure も完了済みであること

**ラボ ファイル**: この課題のファイルは、_Allfiles\Labfiles\Starter\DP-200.5_ フォルダーにあります。

## ラボの概要

学生は、Azure SQL Database と Azure Synapse Analytics サーバーをプロビジョニングし、作成されたインスタンスの 1 つに対してクエリを発行できます。また、SQL Data Warehouse をその他複数のデータ プラットフォーム テクノロジーと統合し、PolyBase を使用して 1 つのデータ ソースから Azure Synapse Analytics にデータを読み込むこともできます。

## 課題の目的
  
この課題を完了すると、次のことができるようになります。

1. Azure SQL Database を使用できる
2. Azure Synapse Analytics について説明する 
3. Azure Synapse Analytics を作成してクエリを実行する 
4. PolyBase を使用して Azure Synapse Analytics にデータを読み込む 

## シナリオ
  
ユーザーは AdventureWorks のシニア データ エンジニアであり、チームと協力して、オンプレミスの SQL Server から Azure にある Azure SQL Database にリレーショナル データベース システムを移行します。まず、会社のサンプル データベースを使用して Azure SQL Database のインスタンスを作成します。あなたは、このインスタンスをジュニア データ エンジニアに渡して、部門データベースのテストを実行することを目的とします。

次に、SQL Synapse Analytics サーバーをプロビジョニングし、一連のクエリを使用してサンプル データベースをテストすることで、サーバーのプロビジョニングが成功したことをテストします。次に、このデータ プラットフォーム テクノロジと Azure Synapse Analytics が統合したことをテストするために、PolyBase を使用して Azure BLOB からディメンション テーブルを読み込みます。

このラボを完了すると:

1. Azure SQL Database を使用した
2. Azure Synapse Analytics について説明した 
3. Azure Synapse Analytics を作成してクエリを実行した 
4. PolyBase を使用して Azure Synapse Analytics にデータを読み込んだ 

> **重要**: このラボを進めるにつれ、プロビジョニングまたは構成タスクで発生した問題を書き留め、 _\Labfiles\DP-200-Issues-Docx_ にあるドキュメントの表に記録してください。課題番号を文書化し、テクノロジを記述し、問題とその解決を説明します。このドキュメントは、後のモジュールで参照できるように保存します。

## 演習 1: Azure SQL Database を使用できる

推定時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスクは、以下の通りです。

1. SQL Database インスタンスを作成して構成する。

### タスク 1: SQL Database インスタンスを作成して構成する。

1. Azure portal で、「**+ リソースを作成する**」 ブレードに移動します。

2. 「新規」 スクリーンで、「**マーケット プレースの検索**」 テキスト ボックスをクリックし、「**SQL Database**」 という単語を入力します。表示される一覧で 「**SQL Database**」 をクリックします。

3. 「**SQL Database**」 画面で、「**作成**」 をクリックします。

4. 「**SQL Database の作成**」 画面から、次の設定を使用して Azure SQL Database を作成します。

    - 「プロジェクトの詳細」 セクションで、次の情報を入力します
    
        - **Subscription**: このラボで使用するサブスクリプションの名前

        - **リソース グループ**: **awrgstudxx** (**xx** は自分のイニシャル)。

    - 「**追加設定**」 タブをクリックし、「**サンプル**」 をクリックします。AdventureworksLT サンプル データベースが自動的に選択されます。 
    
    - これが完了したら、「**基本**」 タブをクリックします。
    
    - 「データベースの詳細」 セクションで、次の情報を入力する
    
        - データベース名: 「**AdventureworksLT**」 と入力します。
     
        - サーバー: 次の設定で **新規作成** をクリックして新しいサーバーを作成し、**OK** をクリックします。
            - **サーバー名**: **sqlservicexx** (**xx** は自分のイニシャル)
            - **サーバー管理者のログイン**: **xxsqladmin** (**xx** は自分のイニシャル)
            - **パスワード**: **Pa55w.rd**
            - **パスワードを確認**: **Pa55w.rd**
            - **場所**: 近くの **場所** を選択します。
            - 「**OK**」 をクリックします。

                ![Azure portal でサーバー インスタンスを作成する](Linked_Image_Files/M05-E01-T01-img1.png)

            - その他の設定は既定のままにして、「**OK**」 をクリックします。
            

    ![Azure portal で SQL Database を作成する](Linked_Image_Files/M05-E01-T01-img02.png)

5. 「**SQL Database の作成**」 ブレードで、「**確認および作成**」 をクリックします。

6. 「**SQL Database の作成**」 ブレードの検証後、「**作成**」 をクリックします。

   > **注**: プロビジョニングの所要時間は約 4 分です。

> **結果**: このエクササイズを完了すると、Azure SQL Database インスタンスが作成されます。

## 演習 2: Azure Synapse Analytics について説明する
  
推定時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスクは次のとおりです。

1. Azure Synapse Analytics インスタンスを作成して構成する。

2. サーバー ファイアウォールを構成する

3. ウェアハウス データベースを一時停止する

### タスク 1: Azure Synapse Analytics インスタンスを作成して構成する。

1. Azure portal で、スクリーンの左上にあるリンク 「**ホーム**」 をクリックします。

2. Azure portal で、「**+ リソースの作成**」 をクリックします。

3. 「新規」 ブレードで、「**マーケット プレースの検索**」 テキスト ボックスに移動し、「**Synapse**」 という単語を入力します。表示される一覧の **Azure Synapse Analytics** をクリックします。

4. **Azure Synapse Analytics** ブレードで、**Create** をクリックします。

5. **Create Synapse ワークスペース** **基本** ブレードで、次の設定を使用して Azure Synapse Analytics Workspace を作成します。

    - 「プロジェクトの詳細」 セクションで、次の情報を入力します

        - **Subscription**: このラボで使用するサブスクリプションの名前

        - **リソース グループ**: **awrgstudxx** (**xx** は自分のイニシャル)。

    - ワークスペース詳細セクションで、以下の設定を使用してワークスペースを作成します。
        
        - **「ワークスペース名」**: **wrkspcxx** (**xx** は自分のイニシャル)。
        - **リージョン**：最寄りの地域とリソースグループをデプロイした場所を選択します
        - **Data Lake Storage Gen2 の選択**：「サブスクリプションから」
        - **アカウント名**：**awdlsstudxx** を選択します（**xx** は自分のイニシャル）
        - **ファイルシステム名**： **data** を選択します
        - 「Data Lake Storage Gen 2 アカウント「awdlsstudxx」の Storage BLOB Data Contributor の役割を自分に割り当てる」のチェックボックスをクリックします 

        ![Synapse ワークスペースを作成する](Linked_Image_Files/M05-E02-T01-img01a.png) 

    - **Synapse ワークスペースの作成** ブレードで、**セキュリティ** タブに移動します。 

    - SQL 管理者の資格情報セクションで以下の情報を入力します。
        - **パスワード**: **Pa55w.rd**
        - **パスワードを確認**: **Pa55w.rd**
        - 他の設定はすべて **規定値** のままにします。 

    - スクリーンで、「**確認および作成**」 をクリックします。
    - このブレードで **「作成」** をクリックします。

   > **注**: プロビジョニングの所要時間は約 7 分です。

6. プロビジョニングが完了したら、**「リソースに移動」** を選択すると、Azure Synapse Analytics ワークスペースの **概要** ページが開きます。  

7. **新しい専用 SQL プール** を選択する

8. **専用 SQL プールの作成** ブレードの **基本** ページで、次の設定を構成します。
        - 専用 SQL プール名：**dedsqlxx** （**xx** は自分のイニシャル）
        - 他の設定はすべて規定値のままにします

9. **専用 SQL プールの作成** スクリーンで、**「確認および作成」** をクリックします。

10. **「専用 SQL プールの作成」** で、**「作成」** をクリ ックします。
  

   > **注**: プロビジョニングの所要時間は約 7 分です。

### タスク 2: サーバー ファイアウォールを構成する

1. Azure portal のブレードで、**リソース グループ** をクリックし、**awrgstudxx** をクリックし、**wrkspcxx** をクリックします。(**xx** は自分のイニシャル)

2. **Wrkspcxx** スクリーンで、**ファイアウォール** をクリックします。

3. **wrkspcxx**- ファイアウォール スクリーンで、オプション + **「クライアント IP の追加」** をクリックし、 **「Azure サービスとリソースのこのワークスペースへのアクセスを許可する」** が **「オン」** に設定されていることを確認してから、**「保存」** をクリックします。成功画面で、「**OK**」 をクリックします。

    ![Azure portal での Azure Synapse Analytics ファイアウォール設定の構成](Linked_Image_Files/M05-E02-T02-img01.png)

    > **注**: サーバーのファイアウォール規則が正常に更新されたことを示すメッセージを受け取ります。

4. ファイアウォール スクリーンを閉じます。

> **結果**: このエクササイズを完了すると、Azure Synapse Analytics インスタンスを作成し、サーバー ファイアウォールを構成して、それに対する接続を有効にします。

### タスク 3: **dedsqlxx** 専用SQLプールを一時停止します。

1. リソース グループで **dedsqlxx** リソースに移動します。 

2. **dedsqlxx** (**xx** は自分のイニシャル) をクリックします。

3. **dedsqlkxx (wrkspcxx/dedsqlxx)** スクリーンで、「**一時停止**」 をクリックします。

4. 「**dedsqlxx** の一時停止」 スクリーンで、「**はい**」 をクリックします



## 演習 3: Azure Synapse Analytics データベースとテーブルの作成

推定時間: 25 分

個別エクササイズ

このエクササイズの主なタスクは次のとおりです。

1. Synapse Studio を理解し、専用 SQL プールに接続します。

2. 専用 SQL プール データベースを作成する

3. 専用 SQL プール テーブルの作成

    > **注**: Transact-SQL に慣れていない場合は、次の課題のステートメントは、次の場所 「**Allfiles\Labfiles\Starter\DP-200.5\SQL DW Files**」 にあるものを使用することができます。

### タスク 1: 専用 SQL プールを Azure Synapse Studio に接続する

1. リソース グループで **dedsqlxx** リソースに移動します。  

2. **「概要」** セクションで、**「Synapse Studio の起動」** に移動します

3. スクリーン左側の **管理** をクリックします

4. **SQL プール** を選択し、「新規」をクリックします。 

	**基本** タブで以下の値を入力します。
	
	Dedicated SQL pool name: DWDB	
	
	**確認および作成** をクリックし、**作成**をクリックします。

5. データベースの作成が完了したら左側のメニューから**データ**に移動し、ワークスペース配下に **DWDB**が作成されていることを確認します。

    ![Dedicated SQL Pool New SQL Script](Linked_Image_Files/M05-E03-T01-img01a.png)


### タスク 2: 専用 SQL プール テーブルの作成。

1. Synapse Studio で、**「Data」** タブで **「DWDB」** をクリックします。

2. **DWDB** データベースの横にある Eclipse(...) を選択します。

3. **新しい SQL スクリプト** と **空のスクリプト** を選択します

4. 次の列に **replicate** の分散を持つ 「**Clustered columnstore**」 インデックスを有する 「**dbo.Users**」 という名前のテーブルを作成します。

    
    | 列名 | データ型 (data type) | NULL 値の許容|
    |-------------|-----------|------------|
    | UserId | int | NULL 値|
    | City | nvarchar(100) | NULL 値|
    | Region | nvarchar(100) | NULL 値|
    | Country | nvarchar(100) | NULL 値|

    	> **注**: Transact-SQL に慣れていない場合は、"Allfiles\Solution\DP-200.5\SQL DW Files\Lab 5.3.3. Creating Tables" に 1_Creating Tables.sql スクリプトがあります。テーブルの作成に必要なコードの大部分が含まれていますが、適宜修正してください。
	
	> **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

5. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。**dbo.Users** テーブルが作成されたかどうかを確認するには、「更新」 をクリックして **テーブル** を展開すると dbo.Users が表示されるはずです。 

7. 再度、**DWDB** データベースの横にある Eclipse を選択します。

8. **新しい SQL スクリプト** と **空のスクリプト** を選択します

9. 次の列に **round robin** の分散を持つ 「**Clustered columnstore**」 インデックスを有する 「**dbo.Products**」 という名前のテーブルを作成します。

    | 列名 | データ型 (data type) | NULL 値の許容|
    |-------------|-----------|------------|
    | ProductId | int | NULL 値|
    | EnglishProductName | nvarchar(100) | NULL 値|
    | Color | nvarchar(100) | NULL 値|
    | StandardCost | int | NULL 値|
    | ListPrice | int | NULL 値|
    | Size | nvarchar(100) | NULL 値|
    | Weight | int | NULL 値|
    | DaysToManufacture | int | NULL 値|
    | Class | nvarchar(100) | NULL 値|
    | Style | nvarchar(100) | NULL 値|

    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

10. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。**dbo.Products** テーブルが作成されたかどうかを確認するには、「更新」 をクリックして **テーブル** に移動し、展開するとテーブルが表示されるはずです。 

12. 再度 **DWDB** データベースの横にある Eclipse を選択します。

13. **新しい SQL スクリプト** と **空のスクリプト** を選択します

14. 次の列を持つ **SalesUnit** での**Hash**分散を使用して、**clustered columnstore** インデックスを有する **dbo.FactSales** という名前のテーブルを作成します。

    | 列名 | データ型 (data type) | NULL 値の許容|
    |-------------|-----------|------------|
    | DateId | int | NULL 値|
    | ProductId | int | NULL 値|
    | UserId | int | NULL 値|
    | UserPreferenceId | int | NULL 値|
    | SalesUnit | int | NULL 値|

    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

15. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。**dbo.FactSales** テーブルが作成されたかどうかを確認するには、「更新」 をクリックして **テーブル** に移動し、展開するとテーブルが表示されるはずです。 

> **結果**: このエクササイズを完了すると、Synapse Studio を使用して、DWDB という名前のデータ ウェアハウスと、Users、Products、FactSales という名前の 3 つのテーブルが作成されます。

## 演習 4: PolyBase を使用した Azure Synapse Analytics へのデータ読み込み 

推定時間: 10 分

個別エクササイズ

このエクササイズの主なタスクは次のとおりです。

1. Data Lake Storage コンテナーとキーの詳細の収集

2. Azure Data Lake Storage の PolyBase を使用して dbo.Dates テーブルを作成する

### タスク 1: Azure BLOB アカウント名とキーの詳細を収集する

1. Azure portal で、「**リソース グループ」**」 をクリックしてから、「**awrgstudxx**」 をクリックし、次に 「**awdlsstudxx**」 をクリックします (xx は名前のイニシャル)。

2. 「**awdlsstudxx**」 画面で、「**アクセス キー**」 をクリックします。「**ストレージ アカウント名**」 の横にあるアイコンをクリックし、メモ帳に貼り付けます。

3. 「**awsastudxx - アクセス キー**」 画面で、**キーの表示** をクリックし、「**key1**」 で、「**キー**」 の横にあるアイコンをクリックしてコピーしたらメモ帳に貼り付けます。

### タスク 2: Azure BLOB から PolyBase を使用し、dbo.Dates テーブルを作成する

1. Synapse Studio で、新しく作成された **「DWDB」** に移動します。

2. **DWDB** データベースの横にある Eclipse を選択します。

3. **新しい SQL スクリプト** と **空のスクリプト** を選択します

4. **DWDB** データベースに対して**マスター キー**を作成します。クエリ エディターで、次のコードを入力します。

    ```SQL
    CREATE MASTER KEY;
    ```
    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

5. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

7. 再度 **DWDB** データベースの横にある Eclipse を選択します。

8. **新しい SQL スクリプト** と **空のスクリプト** を選択します

9. 次のコードをクエリ エディターに入力して、次の詳細を含む、「**AzureStorageCredential**」 という名前のデータベース スコープの資格情報を作成します。
    - IDENTITY: **MOCID**
    - SECRET: **ストレージ アカウントのアクセス キー**

    ```SQL
    CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
    WITH
    IDENTITY = 'MOCID',
    SECRET = 'Your storage account key';
    ```
    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

10. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

11. 再度 **DWDB** データベースの横にある Eclipse を選択します。

13. **新しい SQL スクリプト** と **空のスクリプト** を選択します

14. 「クエリ」 ウィンドウに、**AzureStorageCredential** を使用する **HADOOP** の種類で作成された BLOB ストレージ アカウントとデータ コンテナー用に **AzureStorage** という名前の外部データ ソースを作成するコードを入力します。場所キーの **awdlsstudxx** を自分のストレージ アカウントで自分のイニシャルに置き換える必要があります。 

    ```SQL
	CREATE EXTERNAL DATA SOURCE AzureStorage
    WITH (
        TYPE = HADOOP,
        LOCATION = 'abfs://data@awdlsstudxx.dfs.core.windows.net',
        CREDENTIAL = AzureStorageCredential
    );
    ```
    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

15. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

16. **DWDB** データベースの横にある Eclipse を選択します。

17. **新しい SQL スクリプト** と **空のスクリプト** を選択します

19. 「クエリ」 ウィンドウに、formattype が **DelimitedText**、フィールド ターミネータが **コンマ**の **TextFile** という名前の外部ファイル形式を作成するコードを入力します。

    ```SQL
    CREATE EXTERNAL FILE FORMAT TextFile
    WITH (
        FORMAT_TYPE = DelimitedText,
        FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
    );
    ```
    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

20. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

22. **DWDB** データベースの横にある Eclipse を選択します。

23. **新しい SQL スクリプト** と **空のスクリプト** を選択します   

24. 「クエリ」 ウィンドウに、**Location** がルート ファイル、データ ソースが **AzureStorage**、File-format が **TextFile** で次の列を有する **dbo.DimDate2External** という名前の外部テーブルを作成するコードを入力します。

    | 列名 | データ型 (data type) | NULL 値の許容|
    |-------------|-----------|------------|
    | Date | datetime2(3) | NULL 値|
    | DateKey | decimal(38, 0) | NULL 値|
    | MonthKey | decimal(38, 0) | NULL 値|
    | Month | nvarchar(100) | NULL 値|
    | Quarter | nvarchar(100) | NULL 値|
    | Year | decimal(38, 0) | NULL 値|
    | Year-Quarter | nvarchar(100) | NULL 値|
    | Year-Month | nvarchar(100) | NULL 値|
    | Year-MonthKey | nvarchar(100) | NULL 値|
    | WeekDayKey| decimal(38, 0) | NULL 値|
    | WeekDay| nvarchar(100) | NULL 値|
    | Day Of Month| decimal(38, 0) | NULL 値|

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
        LOCATION='/DimDate2.txt',
        DATA_SOURCE=AzureStorage,
        FILE_FORMAT=TextFile
    );
    ```
    > **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

25. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

26. **DWDB** データベースの横にある Eclipse を選択します。

27. **新しい SQL スクリプト** と **空のスクリプト** を選択します  

28. テーブルに対して select ステートメントを実行して、テーブルが作成されたことをテストします。

    ```SQL
    SELECT * FROM dbo.DimDate2External;
    ```
> **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

29. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

30. **DWDB** データベースの横にある Eclipse を選択します。

31. **新しい SQL スクリプト** と **空のスクリプト** を選択します  

32. 「クエリ」 ウィンドウに、**columnstore** インデックス、および **dbo.DimDate2External** テーブルからデータを読み込む **ラウンド ロビン** の **分散** を持つ **dbo.Dates** という名前のテーブルを作成する **CTAS** ステートメントを入力します。

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
> **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

33. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

34. **DWDB** データベースの横にある Eclipse を選択します。

35. **新しい SQL スクリプト** と **空のスクリプト** を選択します  
 
36. 「クエリ」 ウィンドウに、**DateKey**、**Quarter**、**Month** 列の統計を作成するクエリを入力します。

    ```SQL
    CREATE STATISTICS [DateKey] on [Dates] ([DateKey]);
    CREATE STATISTICS [Quarter] on [Dates] ([Quarter]);
    CREATE STATISTICS [Month] on [Dates] ([Month]);
    ```
> **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。 

40. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

41. **DWDB** データベースの横にある Eclipse を選択します。

42. **新しい SQL スクリプト** と **空のスクリプト** を選択します

44. テーブルに対して select ステートメントを実行して、テーブルが作成されたことをテストします

    ```SQL
    SELECT * FROM dbo.Dates;
    ```
> **注**: スクリプトが **DWDB** に接続され、データベース **DWDB** を使用していることを確認します。

45. **Synapse Studio** で、**「実行」** をクリックすると、クエリが実行されます。

