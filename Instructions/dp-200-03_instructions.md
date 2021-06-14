# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 3 - Azure Databricks を使用したチーム ベースのデータ サイエンスの有効化

**推定時間**: 75 分

**前提条件**: このラボのケース スタディは既に確認していることを前提としています。モジュール 1: 「データ エンジニアのための Azure」の内容とラボを完了していることも前提としています。

**ラボ ファイル**: このラボのファイルは、_Allfiles\Labfiles\Starter\DP-200.3_ フォルダーにあります。

## ラボの概要

受講者は、Azure Databricks を使用するとデータ サイエンス プロジェクトに役立つ理由を理解します。Azure Databricks のインスタンスをプロビジョニングして、ワークスペースを作成します。このワークスペースは、Data Lake Store Gen II ストアから簡単なデータ準備タスクを実行するために使用します。最後に、Azure Databricks を使用して変換を行うチュートリアルを実施します。

## ラボの目的
  
このラボを完了すると、次のことができるようになります。

1. Azure Databricks について説明する
2. Azure Databricks を使用する
3. Azure Databricks を使用してデータを読み取る
4. Azure Databricks を使用して変換を実行する

## シナリオ
  
情報サービス部門 (IS) からの要求に対応して、予測分析プラットフォームを構築するプロセスを開始するために、このテクノロジを使用する利点を列挙します。情報サービス部門にはデータ サイエンティストが加わり、新しいチーム メンバーに予測分析環境を利用できるようにさせたいと考えています。

あなたは、Azure Databricks 環境を立ち上げてプロビジョニングし、既存の Data Lake Storage Gen 2 アカウントからデータを取り込むことで、サービス上で単純なデータ準備ルーチンを実行して、この環境が機能することをテストします。データ サイエンティストがデータの準備を試行するのを支援する必要があるかもしれないということは、データ エンジニアとして聞かされていたことです。そのために、基本的な変換を実行するのに役立つ、ノートブックを使用して確認することを勧められていました。

このラボでは、次のことを行います。

1. Azure Databricks について理解する
2. Azure Databricks を使用する
3. Azure Databricks を使用してデータを読み取る
4. Azure Databricks を使用して変換を実行する

> **重要**: このラボを進める中で発生したプロビジョニングまたは構成タスクの問題については、メモに書き留め、_\Labfiles\DP-200-Issues-Docx_にあるドキュメントの表に記録してください。ラボ番号、テクノロジ、発生した問題、解決した方法を記述しておきます。このドキュメントは、後のモジュールで参照できるように保存します。

## 演習 1: Azure Databricks について説明する

>**重要**: **最初に演習 2** を実行し、演習 2 で Databricks クラスターの作成を開始した後に演習 1 に戻ります (プロビジョニングに10 分間かかるため)。

推定時間: 15 分

個別演習
  
この演習の主なタスクは、以下の通りです。

1. このコースでこれまでに学習した内容から、Azure Databricks が目指すデジタル変革の要件と、Azure Databricks のデータ ソースの候補を特定します。

2. インストラクターは、わかったことについてグループと話し合います。

### タスク 1: デジタル変革と候補のデータ ソースを定義する

1. ラボの仮想マシンから **Microsoft Word** を起動し、**Allfiles\Labfiles\Starter\DP-200.3** フォルダーからファイル **DP-200-Lab03-Ex01.docx** を開きます。

2. このラボのケース スタディとシナリオの概説に従って、**10 分間**でデジタル環境の変革要件と候補データ ソースを文書化します。

### タスク 2: わかったことについてインストラクターと話し合う

1. インストラクターは、わかったことについて話し合うためにグループを中断させます。

> **結果**: この演習を完了すると、Azure Databricks が満たすデジタル環境の変革要件と候補データ ソースを識別する Microsoft Word ドキュメントが作成されます。

## 演習 2: Azure Databricks を使用
  
推定時間: 20 分

個別演習
  
この演習の主なタスクは次のとおりです。

1. リソース グループに Azure Databricks Premium 層インスタンスを作成します。

2. Azure Databricks を開きます。

3. Databricks ワークスペースを起動し、Spark クラスターを作成します。

### タスク 1: Azure Databricks インスタンスを作成して構成する

1. 画面の左上にある Azure portal で、「**ホーム**」 ハイパーリンクをクリックします。

2. Azure portal で、「**+ リソースの作成**」 アイコンをクリックします。

3. 「新規」 画面で、「**マーケットプレースの検索**」 テキスト ボックスに移動し、「**databricks**」という単語を入力します。表示される一覧で「**Azure Databricks**」 をクリックします。

4. 「**Azure Databricks**」 ブレードで 「**作成**」 をクリックします。

5. 「**Azure Databricks サービス**」 ブレードから、次の設定を使用してAzure Databricks ワークスペースを作成します。

    - **ワークスペース名**: **awdbwsstudxx** (**xx** は自分のイニシャル)。

    - **サブスクリプション**: このラボで使用するサブスクリプションの名前

    - **リソース グループ**: **awrgstudxx** (**xx** は自分のイニシャル)。

    - **場所**: ラボの場所に最も近い Azure リージョンの名前と、Azure VM をプロビジョニングできる場所。

    - **価格レベル**: **Premium (+ ロールベースのアクセス制御)**。


        ![Azure portal で Azure Databricks を作成します](Linked_Image_Files/M03-E02-T01-img01.png)

6. **Azure Databricks サービス**ブレードで、**作成**をクリックします。

   > **注**: プロビジョニングの所要時間は約 3 分です。Databricks ランタイムは、Apache Spark を基盤として、Azure クラウドにネイティブに対応するように構築されています。Azure Databricks は、インフラストラクチャの複雑性を完全に排除しており、データ インフラストラクチャの設定と構成に関する専門知識も必要ありません。運用ジョブのパフォーマンスに気を掛けるデータ エンジニアのために、Azure Databricks は、I/O レイヤーと処理レイヤー (Databricks I/O) でのさまざまな最適化によって、高速で高性能な Spark エンジンを提供します。
   
### タスク 2: Azure Databricks を開く

1. Azure Databricks サービスが作成されたことを確認します。

2. Azure portal で 「**リソース グループ**」 画面に移動します。

3. 「リソース グループ」 画面で、「**awrgstudxx**」 リソース グループ (**xx** は自分のイニシャル) をクリックします。

4. 「**awrgstudxx**」 画面で、「**awdbwsstudxx**」 (**xx** は自分のイニシャル) をクリックして、Azure Databricks を開きます。これで、Azure Databricks サービスが開きます。

    ![Azure portal での Azure Databricks サービス](Linked_Image_Files/M03-E02-T02-img01.png)

### タスク 3: Databricks ワークスペースを起動し、Spark クラスターを作成する

1. Azure portal の 「**awdbwsstudxx**」 画面で、「**ワークスペースの起動**」 ボタンをクリックします。

    > **注**: Microsoft Edge の別のタブで、Azure Databricks ワークスペースにサインインします。

2. 「**Common Tasks**」 で、「**New Cluster**」 をクリック します。

3. 「**Create Cluster**」 画面の 「New Cluster」 で、次の設定を使って Databricks クラスターを作成し、「**Create Cluster**」 をクリックします。

    - **Cluster Name**: **awdbclstudxx** (**xx** は自分のイニシャル)。

    - **Cluster Mode**: **Standard**

    - **Pool**: **None**

    - **Databricks Runtime Version**: **Runtime: 8.3 (Scala 2.12, Spark 3.1.1)**
    
    - 「**Terminate after 60 minutes of inactivity**」 チェック ボックスをオンにします。クラスターが使われていない場合にクラスターを終了するまでの時間 (分単位) を指定します。

    - **Min Workers**: **1**

    - **Max Workers**: **2**

    - 残りのオプションはすべて現在の設定のままにしておきます。

        ![Azure portal で Azure Databricks クラスターを作成する](Linked_Image_Files/M03-E02-T03-img01.png)

4. 「**クラスターの作成**」 画面で、「**クラスターの作成**」 をクリックし、Microsoft Edge の画面を開いたままにします。

> **注**: グラフィカル ユーザー インターフェイスを使用して Spark クラスターの作成が簡略化されるため、Azure Databricks インスタンスの作成は約 10 分で行えます。クラスターの作成中は、「**状態**」 が 「**保留中**」 になります。クラスターが作成されると、「**実行中**」 に変わります。

> **注**: クラスターの作成中に、**演習 1に戻って実行します**。

## 演習 3: Azure Databricks を使用してデータを読み取る

推定時間: 30 分

個別演習

この演習の主なタスクは次のとおりです。

1. Databricks クラスターが作成されたことを確認します。

2. Azure Data Lake Store Gen II アカウント名を収集します。

3. Databricks インスタンスを有効にして、Data Lake Gen II Store にアクセスします。

4. Databricks ノートブック を作成し、Data Lake Store に接続します。

5. Azure Databricks でデータを読み取ります。

### タスク 1: Databricks クラスターの作成を確認する

1. Microsoft Edge に戻り、「**Clusters**」 で **awdbclstudxx** という名前のクラスター (**xx** は自分のイニシャル) の 「state」 が 「**Running**」 になっていることを確認します。

### タスク 2: Azure Data Lake Store Gen II アカウント名を確認する

1. Microsoft Edge で 「Azure portal」 タブ、「**リソース グループ**」、**awrgstudxx** の順にクリックし、**awdlsstudxx** をクリックします。(**xx** は自分のイニシャルです)

2. 「**awdlsstudxx**」 画面で 「**アクセス キー**」 をクリックし、「**ストレージアカウント名**」 の横にあるコピー アイコンをクリックして、メモ帳に貼り付けます。

    ![Azure portal での Data Lake Storage アカウント名へのアクセス](Linked_Image_Files/M03-E03-T02-img01.png)

### タスク 3: Databricks インスタンスを有効にして、Data Lake Gen II Store にアクセスする

1. Azure portal で、「**ホーム**」 ハイパーリンクをクリックし、「**Azure Active Directory**」 アイコンをクリックします。

2. 「**概要**」 画面で、「**アプリの登録**」 をクリックします。

3. 「**アプリの登録**」 画面で、「**+ 新規登録**」 ボタンをクリックします。

4. アプリケーションの登録画面で、**名前** に **DLAccess** と入力し、「**リダイレクトURI (オプション)**」 セクションで、「**Web**」 が選択されていることを確認し、アプリケーションの値に **http://localhost** を入力します。

    ![Azure portal でアプリを登録します。](Linked_Image_Files/M03-E03-T03-img01.png)

5. 「**登録**」 をクリックします。DLAccess 画面が表示されます。

6. 「**DLAccess**」 登録アプリ画面で、**アプリケーション (クライアント) ID** と**ディレクトリ (テナント ID)** をコピーしてメモ帳 にペーストします。

7. 「**DLAccess**」 登録アプリ画面で、「**証明書とシークレット**」 をクリックして、「**+ 新しいクライアント シークレット**」 をクリックします。

8. 「クライアント シークレットの追加」 画面で、「**説明**」 を「**DL アクセス キー**」 と入力し、キーの 「**期間**」 を 「**1 年間**」 に指定します。完了したら、「**追加**」 をクリックします。

    ![Azure portal でのクライアント シークレットの追加しています](Linked_Image_Files/M03-E03-T03-img02.png)

    >**重要**: 「**追加**」 をクリックすると、キーは下の図のように表示されます。このキー値をコピーできるのは 1 度だけです。

    ![DL アクセス キーの場所](Linked_Image_Files/M03-E03-T03-img03.png)

9. 「**アプリケーション キーの値**」 をコピーしてメモ帳 に貼り付けます。

10. リソース グループにストレージ BLOB データ共同作成者のアクセス許可を割り当てます。Azure portalで 「**ホーム**」 ハイパーリンク、「**リソースグループ**」 アイコン、「**awrgstudxx**」 リソース グループをクリックします。**xx**は自分のイニシャルです。

11. 「**awrgstudxx**」 画面で、「**アクセスの制御 (IAM)**」 をクリックします。 

12. 「**ロールの割り当て**」 タブをクリックします。 

13. **「+追加」** をクリックして、**「ロールの割り当てを追加する」** をクリックします。

14. 「**ロールの割り当てを追加**」 ブレードの 「ロール」 で、「**ストレージ BLOB データ 共同作成者**」 を選択します。

15. 「**ロールの割り当てを追加**」 ブレードの 「選択」 で、「**DLAccess**」 を選択し、「**保存**」 をクリックします。

16. Azure ポータルで 「**ホーム**」 ハイパーリンクをクリックし、「**Azure Active Directory**」 アイコンをクリックして 「**自分のロール**」 を確認します。ユーザー ロールである場合は、管理者以外がアプリケーションを登録できることを確認する必要があります。

17. 「**ユーザー**」 をクリックし、「**ユーザー - すべてのユーザー**」 ブレードの 「**ユーザー設定**」 をクリックし、「**アプリの登録**」 を確認します。この値は、管理者だけが設定できます。「はい」 に設定すると、Azure AD テナント内の任意のユーザーがアプリを登録することができます。 

18. 「**ユーザー - すべてのユーザー**」 画面を閉じます。

19. 「Azure Active Directory」 ブレードで、「**プロパティ**」 をクリックします。

20. 「**ディレクトリ ID**」 の横にある 「コピー」 アイコンをクリックし、テナント ID を取得したら、メモ帳 に貼り付けます。

21. メモ帳ドキュメントを、フォルダー **Allfiles\Labfiles\Starter\DP-200.3** に **DatabricksDetails.txt** として保存します。

### タスク 4: Databricks ノートブック を作成し、Data Lake Store に接続する

1. Microsoft Edge で、「**クラスター - Databricks**」 タブ をクリックします。

    > **注**: クラスター ページが表示されます。

2. Microsoft Edge の左側にある 「Azure Databricks」 ブレードで、「**Workspace**」 をクリックし、**Workspace**の横にあるドロップダウンをクリックし、「**Create**」 をクリックして 「**Notebook**」 をクリックします。

3. 「**Create Notebook**」 画面で、「Name」 に 「**My Notebook**」 を入力します。

4. 「**Default Language**」 ドロップダウン リストで 「**Scala**」 を選択します。

5. 以前に作成したクラスターの名前がクラスターに表示されていることを確認し、「**Create**」 をクリックします。

    ![Azure Databricks でのノートブックの作成](Linked_Image_Files/M03-E03-T04-img01.png)

     > **注記**: これにより、"My Notebook (Scala)" というタイトルのノートブックが開きます。

6. Notebook のセル **Cmd 1** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Connect to Azure Data Lake Storage Gen2 account

    spark.conf.set("fs.azure.account.auth.type", "OAuth")
    spark.conf.set("fs.azure.account.oauth.provider.type", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
    spark.conf.set("fs.azure.account.oauth2.client.id.<storage-account-name>.dfs.core.windows.net", "<application-id>")
    spark.conf.set("fs.azure.account.oauth2.client.secret.<storage-account-name>.dfs.core.windows.net", "<authentication-key>")
    spark.conf.set("fs.azure.account.oauth2.client.endpoint.<storage-account-name>.dfs.core.windows.net", "https://login.microsoftonline.com/<tenant-id>/oauth2/token")
    ```

7. このコード ブロックでは、コード ブロック内の**application-id**、**authentication-key**、**tenant-id**、および **storage-account-name** のプレースホルダー値を、以前に収集した値で置き換えます。これらの値は メモ帳 に保持されます。

8. ノートブックの **Cmd 1** の下のセルで 「**Run**」 アイコンをクリックし、次の図でハイライトされているように 「**Run Cell**」 をクリックします。 

    ![Azure Databricks でノートブックで cvode を実行する](Linked_Image_Files/M03-E03-T04-img02.png)

    >**注** "Command took 0.0X seconds -- by XXXXX at 4/4/2019, 2:46:48 PM on awdbclstudxx" というメッセージがセルの下部に表示されます。

### タスク 5: Azure Databricks でデータを読み取る

1. ノートブックの **Cmd 1** セルの右上にマウスを移動し、「**▽**」 アイコンをクリックし **Add Cell Below** をクリックします。**Cmd2** という名前の新しいセルが表示されます。

    ![Azure Databricks のノートブックでのセルの追加](Linked_Image_Files/M03-E03-T04-img03.png)

2. Notebook のセル **Cmd 2** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Azure Data Lake Storage Gen2 ファイル システムの JSON データを読み取る

    val df = spark.read.json("abfss://<file-system-name>@<storage-account-name>.dfs.core.windows.net/preferences.json")
    ```

3. このコード ブロックでは、**file-system-name** を **logs** という単語で、またこのコード ブロック内の **storage-account-name** プレースホルダー値を以前に収集してメモ帳 に保持した値で置き換えます。

4. ノートブックの **Cmd 2** の下のセルで、「**Run**」 アイコンをクリックし、「**Run Cell**」 をクリックします。 

    >**注** Spark ジョブが実行されたこと、および「Command took 0.0X seconds -- by XXXXX at 4/4/2019, 2:46:48 PM on awdbclstudxx」を示すメッセージが、セルの下部に表示されます。

5. ノートブックの **Cmd 2** セルの右上にマウスを移動し、「**▽**」 アイコンをクリックし **Add Cell Below** をクリックします。**Cmd3** という名前の新しいセルが表示されます。

6. ノートブックのセル **Cmd 3** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //Show result of reading the JSON file
  
    df.show()
    ```



7. ノートブックの **Cmd 3** の下のセルで、「**Run**」 アイコンをクリックし、「**Run Cell**」 をクリックします。

    >**注** Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx" と表示されます。
    ![Azure Databricks での Notebook の結果の実行](Linked_Image_Files/M03-E03-T04-img04.png)
8. Azure Databricks ノートブックを開いたままにします。

>**結果** この演習では、Azure Databricks が Azure Data Lake Store Gen2 のデータにアクセスするためのアクセス許可を設定する上で必要なステップを実行しました。次に、scala を使用して Data Lake Store に接続し、データを読み取り、ユーザーの好みを示すテーブル出力を作成しました。

## 演習 4: Azure Databricksを使用して基本的な変換を実行する

推定時間: 10 分

個別演習

この演習の主なタスクは次のとおりです。

1. データセットの特定の列を取得します。

2. データセットで列の名前の変更を実行します。

3. コメントを追加します。

4. 時間がある場合: その他の変換を行います。

### タスク 1: データセットの特定の列を取得する

1. ノートブックの **Cmd 3** セルの右上にマウスを移動し、「**▽**」 アイコンをクリックし **Add Cell Below** をクリックします。**Cmd4** という名前の新しいセルが表示されます。

2. ノートブックのセル **Cmd 4** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    // Azure Data Lake Storage Gen2 ファイル システムの JSON データセットから特定の列を取得する
    
    val specificColumnsDf = df.select("firstname", "lastname", "gender", "location", "page")
    specificColumnsDf.show()
    ```

3. ノートブックの **Cmd 4** の下のセルで、「**Run**」 アイコンをクリックし、「**Run Cell**」 をクリックします。 

    >**注** Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、"Command took 0.0X seconds -- by XXXXX at 4/4/2019, 2:46:48 PM on awdbclstudxx" と表示されます。

    ![Azure Databricks のノートブックでのスカラ クエリの実行](Linked_Image_Files/M03-E04-T01-img01.png)

### タスク 2: データセットで列の名前の変更を実行する

1. ノートブックの **Cmd 4** セルの右上にマウスを移動し、「**▽**」 アイコンをクリックし **Add Cell Below** をクリックします。**Cmd5** という名前の新しいセルが表示されます。

2. ノートブックのセル **Cmd 5** で、次のコードをコピーし、セルに貼り付けます。

    ```scala
    //ページ列の名前をbike_preferenceに変更する

    val renamedColumnsDF = specificColumnsDf.withColumnRenamed("page", "bike_preference")
    renamedColumnsDF.show()
    ```

3. ノートブックの **Cmd 5** の下のセルで、「**実行**」 アイコンをクリックし、「**セルの実行**」 をクリックします。 

    >**注** Spark ジョブが実行されたことを示すメッセージがセルの下部に表示され、結果テーブルが返され、"Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx" と表示されます。

    ![Azure Databricks のノートブックのクエリの列の名前を変更する](Linked_Image_Files/M03-E04-T02-img01.png)

### タスク 3: コメントを追加する

1. ノートブックの **Cmd 5** セルの右上にマウスを移動し、「**▽**」 アイコンをクリックし **Add Cell Below** をクリックします。**Cmd6** という名前の新しいセルが表示されます。

2. ノートブックのセル **Cmd 6** で、次のコードをコピーし、セルに貼り付けます。

    ```text
    このコードは、「Data」という名前の Data Lake Storage ファイルシステムに接続し、その Data Lake に保存されている preference.json ファイルのデータを読み取ります。次に、データを取得する為の簡単なクエリが作成され、「ページ」列の名前が「bike_preference」に変更します。
    ```

3. ノートブックの **Cmd 6** の下のセルで、「**▽**」 アイコンをクリックし、「**Move Up**」 をクリックします。セルがノートブックの上部に表示されるまで繰り返します。

4. Azure Databricks ノートブックを開いたままにします。

    >**注**この後ラボでは、このデータを別のデータ プラットフォーム テクノロジーにエクスポートする方法を検討します。

> **結果**: この演習を完了すると、ノートブック内にコメントが作成されます。

### タスク 4: 時間に余裕がある場合、またはコースを後で復習している場合

このラボが早く終わった場合、次のセクションのリンクを参照してください。Azure の基本的な変換と詳しい変換について確認できます。

URL にアクセスできない場合は、_Allfiles\Labfiles\Starter\DP-200.3\Post Course Review_フォルダーにあるノートブックのコピーを参照してください。

**基本的な変換**

1. ワークスペース内で、左側のコマンド バーを使用して、「**Workspace**」、「**Users**」 を選択し、「**ユーザー名**」 (家のアイコンのエントリ) を選択します。

2. ブレードが表示されるので、**名前の横にある下向きのシェブロン**を選択し、「**Import**」 を選択します。

3. 「Import Notebooks」 ダイアログ ボックスで、「**URL**」 を選択し、次の URL に貼り付けます。 

```url
    https://github.com/MicrosoftDocs/mslearn-perform-basic-data-transformation-in-azure-databricks/blob/master/DBC/05.1-Basic-ETL.dbc?raw=true
```

4. 「**Import**」 を選択します。

5. インポート後に **05.1-Basic-ETL** という名前のフォルダーが表示されます。そのフォルダーを選択します。

6. フォルダーには、**scala** または **python** を使用して基本的な変換を学習するために使用できる 1 つ以上のノートブックが含まれます。

ノートブック内の指示に従い、ノートブック全体を完了します。残りのノートブックについて順番に続行します。

- **01-Course-Overview-and-Setup** -  (01-コースの概要とセットアップ) このノートブックは、Databricks ワークスペースに関するものです。
- **02-ETL-Process-Overview** -  (02-ETL プロセスの概要) このノートブックには、クエリ、大きなデータ ファイル、及び結果の視覚化に役立つ演習が含まれています。
- **03-Connecting-to-Azure-Blob-Storage** -  (03-Azure Blob Storage への接続) このノートブックでは、基本的な集計と結合を実行します。
- **04-Connecting-to-JDBC** -  (04-JDBC への接続) このノートブックは、Databricks を使用してさまざまなソースからデータにアクセスするためのステップを示しています。
- **05-Applying-Schemas-to-JSON** -  (05-スキーマから JSON への適用) このノートブックでは、DataFrames を使用して JSON と階層データをクエリする方法を学習します。
- **06-Corrupt-Record-Handling** -  (06-破損レコードの処理) このノートブックには、ADLSを作成し、Databricks DataFrames を使用して、このデータをクエリ及び分析する方法を理解するのに役立つ演習がリストされています。
- **07-Loading-Data-and-Productionalizing** -  (07-データの読み込みと本番への移行) ここでは、Databricks を使用して、Azure Data Lake Storage Gen2 のデータストアをクエリ、分析します。
- **Parsing-Nested-Data** -  (ネスト化されたデータの解析) このノートブックは、オプション サブフォルダーにあり、後で都合の良い時に試してみるためのサンプル プロジェクトが含まれています。

> 「注」 対応するノートブックは Solutions サブフォルダー内にあります。これらには、1 つまたは複数の課題を完了するよう求める演習用の完了したセルが含まれます。答えに窮した場合、または解決方法を確認したいだけの場合は、これらを参照してください。

**詳細な変換**

1. ワークスペース内で、左側のコマンド バーを使用して、「**Workspace**」、「**Users**」 を選択し、「**ユーザー名**」 (家のアイコンのエントリ) を選択します。

2. ブレードが表示されるので、**名前の横にある下向きのシェブロン**を選択し、「**Import**」 を選択します。

3. 「ノートブックのインポート」 ダイアログ ボックスで 「**URL**」 を選択し、次の URL に貼り付けます。 

```url
    https://github.com/MicrosoftDocs/mslearn-perform-advanced-data-transformation-in-azure-databricks/blob/master/DBC/05.2-Advanced-ETL.dbc?raw=true
```

4. 「**Import**」 を選択します。

5. インポート後に **05.2-Advanced-ETL** という名前のフォルダーが表示されます。そのフォルダーを選択します。

6. フォルダーには、**scala** または **python** を使用して基本的な変換を学習するために使用できる 1 つまたは複数のノートブックが含まれます。

ノートブック内の指示に従い、ノートブック全体を完了します。次に残りのノートブックを順番に続行します。

- **01-Course-Overview-and-Setup** -  (01-コースの概要とセットアップ) このノートブックは、Databricks ワークスペースに関するものです。
- **02-Common-Transformations** -  (02-一般的な変換) このノートブックでは、Spark 組み込み関数を使用して一般的なデータ変換を実行します。
- **03-User-Defined-Functions** -  (03-ユーザ定義関数) このノートブックでは、ユーザ定義関数を使用したカスタム変換を実行します。
- **04-Advanced-UDFs** -  (04-高度な UDF) このノートブックでは、高度なユーザー定義関数を使用して複雑なデータ変換を実行します。
- **05-Joins-and-Lookup-Tables** -  (05-結合とルックアップテーブル) このノートブックでは、テーブルに標準結合とブロードキャスト結合を使用する方法を学習します。
- **06-Database-Writes** -  (06-データベースの書き込み) このノートブックには、ETLジョブから変換されたデータを保存し、多数のターゲットデータベースにデータを並行して書き込む為の演習が含まれています。
- **07-Table-Management** -  (07-テーブル管理) ここでは、管理テーブルと非管理テーブルを処理して、保存スペースを最適化します。
- **Custom-Transformations** -  (カスタム変換) このノートブックは、オプションのサブフォルダーにあり、後で自分の時間で探索する為のサンプルプロジェクトが含まれています。

> 「注」 Solutions サブフォルダー内に対応する Notebooks があります。これらには、1 つまたは複数の課題を完了するよう求める演習用の完了したセルが含まれます。答えに窮した場合、または解決方法を確認したいだけの場合は、これらを参照してください。
