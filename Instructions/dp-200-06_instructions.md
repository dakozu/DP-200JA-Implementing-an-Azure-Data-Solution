---
lab:
    title: 'Stream Analytics でのリアルタイム分析の実行'
    module: 'モジュール 6: Streaming Analytics を使用したリアルタイム分析の実行'
---

# DP 200 - データ プラットフォーム ソリューションの実装
# ラボ 6 - Stream Analytics でのリアルタイム分析の実行

**所要時間**: 60 分

**前提条件**: このラボのケース スタディは既に確認していることを前提としています。内容とラボを前提としています。モジュール 1：Azure for the Data Engineer のコースとラボも完了済みであることを前提としています。

**ラボ ファイル**: このラボのファイルは、_Allfiles\Labfiles\Starter\DP-200.6_ のフォルダーにあります。

## ラボの概要

受講者は、データ ストリームとは何か、またイベント処理がどう行われるかを説明し、AdventureWorks のケース スタディに適したデータ ストリーム インジェスト技術を選択できるようになります。選択したインジェスト テクノロジーをプロビジョニングし、これを Stream Analytics と統合して、ストリーミング データで動作するソリューションを作成します。

## ラボの目的
  
このモジュールを修了すると、次のことができるようになります:

1. データ ストリームとイベント処理について説明する
1. Event Hubs でのデータ インジェスト
1. Stream Analytics ジョブでのデータの処理

## シナリオ
  
あなたは、デジタル トランスフォーメーション プロジェクトの一環として、マーケティング部門が業務の生産性を高めるのを支援する業務を CIO に任されました。ここ数年、マーケティング部門は Twitter を使用して、販売されている自転車製品に関するマーケティング メッセージを増幅してきました。 

当部門はキャンペーン後にリーチ ナンバーを提供できますが、ボリュームを手動で追跡することが困難なため、リアルタイムでキャンペーンとインタラクトしているユーザーを把握することはできません。その結果、キャンペーンとインタラクトしているユーザーをリアルタイムで追跡できるシステムを実装したいと考えています。

このラボを完了すると:

1. データ ストリームとイベント処理について説明する
1. Event Hubs でのデータ インジェスト
1. Stream Analytics ジョブでのデータの処理

> **重要**: このラボを進めるにつれ、プロビジョニングまたは構成タスクで発生した問題を書き留め、_\Labfiles\DP-200-Issues-Docx_ にあるドキュメントの表に記録してください。ラボ番号を文書化し、テクノロジーを書き留め、問題とその解決を説明してください。このドキュメントは、後のモジュールで参照できるように保存します。

## エクササイズ 1: データ ストリームとイベント処理について説明する

所要時間: 15 分

グループ エクササイズ
  
このエクササイズの主なタスク:

1. ケース スタディとシナリオから、AdventureWorks のデータ ストリーム インジェスト技術と、データ エンジニアとして実行する高レベルのタスクを特定して、ソーシャル メディア分析の要件を完了します。

1. インストラクターは、調査結果についてグループと話し合います。

### タスク 1: AdventureWorks のデータ要件と構造を特定する。

1. ラボの仮想マシンから **Microsoft Word** を起動し、**Allfiles\Labfiles\Starter\DP-200.6** フォルダーからファイル  **DP-200-Lab06-Ex01.docx** を開きます。

1. ケース スタディ ドキュメント内でグループが特定したデータ要件とデータ構造について、グループで **10 分間** 話し合い、書き出してもらいます。

### タスク 2: 調査結果についてインストラクターと話し合う

1. インストラクターは、調査結果について話し合うためにグループ作業を中断させます。

> **結果**: このエクササイズを完了すると、データ ストリーミング インジェストと、ソーシャル メディア分析の要件を完了するためにデータ エンジニアとして実行する高レベルのタスクのテーブルを示す Microsoft Word ドキュメントが作成されます。

## エクササイズ 2: Event Hubs でのデータ インジェスト。
  
所要時間: 15 分

個別エクササイズ
  
このエクササイズの主なタスク:

1. イベント ハブ名前空間を作成して構成する。

1. イベント ハブを作成して構成する。

1. イベント ハブ のセキュリティを構成する。

### タスク 1: イベント ハブ名前空間を作成して構成する。

1. Azure portal で、[**Create a resource**] (+ リソースを作成) を選択し、「**Event Hubs**」と入力し、 結果の検索から [**イベント ハブ名前空間**] を選択します。次に、[**作成**] を選択します。

1. 次のオプションを使用してイベント ハブ名前空間を作成し、[**作成**] をクリックします。
    - **名前**: xx-socialtwitter-eh (xx は自分のイニシャル)
    - **価格レベル**: Standard
    - **サブスクリプション**: 自分のサブスクリプション
    - **リソース グループ**: awrgstudxx
    - **場所**: ユーザーに近い場所を選択します。
    - 他のオプションは既定のままにします。

    > **注記**: イベント ハブ名前空間の作成には約 1 分かかります。

### タスク 2: イベント ハブを作成して構成する。

1. Azure portal 内のブレードで、**[Resource groups]**(リソース グループ)、**[awrgstudxx]** の順にクリックし、**[awdlsstudxx]** をクリックします (**xx** は自分のイニシャル)。

1. **[xx-socialtwitter-eh]** をクリックします (**xx** は自分のイニシャル)。

1. **[xx-socialtwitter-eh]** 画面で、**[Event Hubs]** をクリックします。

1. 「**socialtwitter-eh**」という名前を入力し、[**作成**] を選択します。

    > **注記**: 約 10 秒後に、イベント ハブが作成されたことを示すメッセージが表示されます。

### タスク 3: イベント ハブ のセキュリティを構成する。

1. Azure portal の **xx-socialtwitter-eh** では、**xx** が自分のイニシャルとなります。ウィンドウの一番下までスクロールし、**socialtwitter-eh** イベントハブをクリックします。

1. イベント ハブへのアクセスを許可するには、[**Shared access policies**] (共有アクセス ポリシー) をクリックします。

1. [**socialtwitter-eh - 共有アクセス ポリシー**] 画面で、[**追加**] を選択して、**管理** アクセス許可のポリシーを作成します。   ポリシーに **socialtwitter-eh-sap** という名前を付け、[**管理**] をオンにしてから、[**作成**] をクリックします。

1. 作成後に新しいポリシー **socialtwitter-eh-sap** をクリックし、**CONNECTION STRING - PRIMARY KEY** のコピー ボタンを選択して、CONNECTION STRING - PRIMARY KEY を メモ帳 に貼り付けます。これは後のエクササイズで使用します。  

1. portal のイベント ハブ画面を閉じます

> **結果**: このエクササイズを完了すると、イベント ハブ名前空間内に Azure Event Hub が作成され、サービスへのアクセスを提供する際に使用するイベント ハブのセキュリティが設定されます。

## エクササイズ 3: Stream Analytics ジョブでのデータの処理

所要時間: 30 分

個別エクササイズ

このエクササイズの主なタスク:

1. Twitter 開発者アカウントを作成する

1. Twitter アクセス キーを設定する

1. Twitter クライアント アプリケーションの設定と起動を実行する

1. Stream Analytics ジョブをプロビジョニングする。

1. Stream Analytics ジョブの入力を指定する。

1. Stream Analytics クエリを定義する。

1. Stream Analytics ジョブの出力を指定する。

1. Stream Analytics クエリを修正する。

1. Streaming Analytics ジョブを開始する。

1. Stream Analytics クエリを定義する。

### タスク 1: Twitter 開発者アカウントを作成する。

1. ブラウザで新しいタブを開き、https://developer.twitter.com/en/apps/ に移動し、自分の Twitter アカウントにログインして、Twitter アプリケーションを設定します。

1. **[アプリ]** ページの右側にある [**アプリを作成**] ボタンをクリックします。

1. 「Please apply for a twitter account 」(Twitter アカウントをお申し込みください) で、[**Apply**] (申し込む) をクリックします。 

1. [User profile] (ユーザー プロファイル) ページで、Twitter アカウントが開発者アカウントに関連付ける正しいアカウントであることを確認し、[**Continue**] (続行) をクリックします。

1. 「Account details」(アカウントの詳細) ページの 「Who are you requesting access for?」(アクセスを要求しているのは誰か?) の下にある 「**I am requesting access for my own personal use**」(自分の個人使用としてアクセルを要求する) をクリックします。[Account name] (アカウント名) に **「learn how to code as *twitter_name***」と入力します。最後に、**[Primary country of operation]** (主に運用する国) に自分が住んでいる国を選択します。[**Continue**] (続行) をクリックします。

    > **注記**: 運用する国に適用されるすべての法律と倫理を遵守してください

1. 「Tell us about your project」] (プロジェクトについて) ページで、「What use case(s) are you interested in?」(興味がある使用ケース) のオプションを選択します。このコースの目的として、[**Student project / Learning to code**] (学生プロジェクト/コードの学習) を選択します。「Describe in your own words what you are building」(構築しているものに関して説明してください) では、使用理由について 300 語で説明します。以下は例です:

    >1.I’m using Twitter’s APIs to learn how to embed twitter statements within a learning application. this account is being used to learn how to do that (私は Twitter の API を使用して、学習アプリケーション内に Twitter のステートメントを埋め込む方法を学んでいます。このアカウントは、その方法を学ぶために使用されています)
    >2.  I plan to analyze Tweets to understand how to count and read streaming tweets in real time as part of a learning exercise (私は学習エクササイズの一環として、リアルタイムでストリーミング ツイートをカウントして読み込む方法を理解するために、Tweets を分析しようと思っています)
    >3.I do not intend on interacting with other peoples tweets in the form of retweeting or liking content. (私は、リツイートしたりコンテンツにいいねを押したりして、他の人のツイートとやり取りするつもりはありません。)I will be reading and counting tweets and looking at sentiment. (私はツイートの読み込みやカウントを行い、センチメントを見ます。)
    >4.Both individual and aggregate tweets will be analysed in the application (個人ツイートと集計ツイートの両方をアプリケーションで分析します) 

1. 最後に、「Will your product, service, or analysis make Twitter content or derived information available to a government entity?」(製品、サービス、または分析によって、Twitter のコンテンツや派生情報を政府機関が利用できるようにしますか?)という質問のオプションを選択し、[**Continue**] (続行) をクリックします。

1. 利用規約を読み、同意する場合は[**Accept**] (同意する) をクリックします。次に、必要に応じてチェックボックスを選択します。[**Submit application**] (申込書の提出) をクリックします。 

1. 受信トレイの確認メールを確認し、メール内の「**confirm your email**」(メールの確認) をクリックしてプロセスを完了します。  Twitter の「Welcome」(ようこそ) 画面に戻ります。

### タスク 2: Twitter アクセス キーを設定する

1. Twitter の「ようこそ」画面を開いていない場合は、ブラウザで新しいタブを開き、https://developer.twitter.com に移動し、Twitter アカウントでログインします。

1. 「Welcome」(ようこそ) または「Apps」(アプリ) ページで、[**Create an app**](アプリの作成) ボタンをクリックします。

1. 「Create an App」(アプリの作成) ページで、次の情報を入力し、[**Create**](作成) をクリックします。 
    - **name (名前)**: xx-social-app (xx は自分のイニシャル)
    - **Application description (アプリケーションの説明)**: 「used to collect and aggregate tweets」(ツイートの収集と集計に使用) などの説明を追加します。
    - **website URL (Web サイト URL)** アプリケーションに使用する個人用アドレス。
    - **Tell us how this app will be used (このアプリの使用方法)**: ストリーミングデータを使用する方法を学ぶためのデモ アプリであることを書き込みます

1. 開発者向けの利用条件を確認し、[**作成**] をクリックします。  アプリケーション名がタイトルの新しいページが表示されます。

1. [**Keys and tokens**] (キーとトークン) という名前のページ タブをクリックします。

1. 「Access token & access token secret」(アクセス トークンとアクセス トークン シークレット) の下にある [**Create**] (作成) ボタンをクリックします。 

    >**注記**: アカウントと現在のアプリケーション用の承認されたアクセス トークンとシークレットが生成されます。

1. 以前に開いた メモ帳 ファイルに次のキーをコピーします。
    - コンシューマ キー (API キー)
    - コンシューマ シークレット (API シークレット)
    - アクセス トークン
    - アクセス トークン シークレット

### タスク 3: Twitter クライアント アプリケーションの設定と起動を実行する

1. **Allfiles\Labfiles\Starter\DP-200.6\Twitter client\TwitterWPFClient\TwitterWPFClient** の **TwitterWPFClient.exe** アプリケーションをダブルクリックします。[TwitterWPFClient here](https://github.com/Azure/azure-stream-analytics/tree/master/Samples/TwitterClient) からダウンロードすることもできます。

1. メモ帳 のデータを TwitterWPFClient.exe アプリケーションに入力します。
    - **Twitter コンシューマ キー (API キー)**: 自分の Twitter コンシューマ キー
    - **Twitter コンシューマ シークレット (API シークレット)** 自分の Twitter コンシューマ シークレット
    - **Twitter アクセス トークン**: 自分の Twitter アクセス トークン
    - **Twitter アクセス シークレット** ): 自分の Twitter アクセス シークレット
    - **Azure EventHub 名**: socialtwitter-eh
    - **Azure Event Hub 接続文字列**: Endpoint=sb://xx-socialtwitter-eh.servicebus.windows.net/;SharedAccessKeyName=xx-social-eh-sap;SharedAccessKey=<Paste in the CONNECTION STRING - PRIMARY KEY from Notepad>  

        >**重要**: 文字列の最後の「;EntityPath=socialtwitter-eh」を必ず削除してください。

    - **検索グループ** は、センチメントを決定するキーワードを定義します。たとえば、「#Brexit」や「brexit」などや、コンマで区切った複数のキーワードを追加することもできます。

1. **TwitterWPFClient.exe** アプリケーションの [**Play**] (再生) ボタンをクリックし、コンソールにツイートが表示されるまで待ってから、アプリケーションを実行したままにします。

      > **注記**: **TwitterWPFClient.exe** アプリケーションは、定義された検索語の日付、検索語のセンチメント スコア、Twitter 名とツイートの詳細をキャプチャします。  

1. すべてのアプリケーションを実行し続けます

### タスク 4: Stream Analytics ジョブをプロビジョニングする。

1. Azure portal に戻り、[**リソースの作成**] を選択し、「**STREAM**」と入力して、[**Stream Analytics ジョブ**] をクリックし、[**作成**] をクリックします。
1. 
1. **[新しい Stream Analytics ジョブ]** 画面で、次の詳細に入力し、[**作成**] をクリックします。
    - **ジョブ名**: socialtwitter-asa-job。
    - **サブスクリプション**: 自分のサブスクリプションを選択します
    - **リソース グループ**: awrgstudxx
    - **場所**: 最も近い場所を選択します。
    - 他のオプションを既定のままにします

    > **注記**: 約 10 秒後に、Stream Analytics ジョブが作成されたことを示すメッセージが表示されます。

### タスク 5: Stream Analytics ジョブの入力を指定する。

1. Azure portal 内のブレードで、**[Resource groups]**(リソース グループ)、**[awrgstudxx]** の順にクリックし、**[awdlsstudxx]** をクリックします (**xx** は自分のイニシャル)。

1. **socialtwitter-asa-job** をクリックします。

1. [**socialtwitter-asa-job** Stream Analytics ジョブ] ウィンドウで、[**入力**] をクリックします。

1. **[入力]** 画面で、[**ストリーム入力の追加**] をクリックし、[**Event Hubs**] をクリックします。     

1. [イベント ハブ] 画面で、次の値を入力し、[**保存**] ボタンをクリックします。
    - **入力エイリアス**: このジョブ入力の名前として TwitterStream と入力します。
    - **Select Event Hub from your subscriptions** (サブスクリプションからイベント ハブを選択): オン
    - **サブスクリプション**: 自分のサブスクリプション名
    - **イベント ハブ名前空間**: xx-socialtwitter-eh
    - **イベント ハブ名**: 既存の名前、socialtwitter-eh を使用します
    - **イベント ハブ ポリシー名**: socialtwitter-eh-sap
    - 残りのオプションは既定のままにします

1. 完了すると、入力ウィンドウの下に TwitterStream 入力ジョブが表示されます。入力ウィンドウを閉じて、Streaming Analytics ジョブ ページに戻ります。

### タスク 6: Stream Analytics クエリを定義する。

1. **socialtwitter-asa-job** ウィンドウで、ウィンドウ中央の [**クエリ**] 画面で[**Edit query**] (クエリの編集) をクリックします。

1. コード エディタで次のクエリを置き換えます。

    ```SQL
    SELECT
        *
    INTO
        [YourOutputAlias]
    FROM
        [YourInputAlias]
    ```

1. Replace with

    ```SQL
    SELECT 
     [Topic]
    ,[SentimentScore]
    ,[created_at]
    ,[Author]
    ,[text]
    FROM [TwitterStream]
    ```

1. [保存] を選択します。

1. [クエリ] ウィンドウを閉じて、Stream Analytics ジョブ ページに戻ります。


### タスク 7: Stream Analytics ジョブの出力を指定する。

1. [**socialtwitter-asa-job** Stream Analytics ジョブ] ウィンドウで、[**出力**] をクリックします。

1. **[出力]** 画面で、[**追加**] をクリックし、[**Blob Storage**] をクリックします。

1. [**Blob Storage**] ウィンドウで、ペインに次の値を入力または選択します。 
- **出力エイリアス**: 出力
- **Select Event Hub from your subscriptions** (サブスクリプションからイベント ハブを選択): オン
- **サブスクリプション**: 自分のサブスクリプション名
- **ストレージ アカウント**: awsastudxx (xx は自分のイニシャル)
- **コンテナー**: 既存を使用して、ツイートを選択します

1. 残りのエントリは既定値のままにしておきます。最後に、[**保存***] をクリックします。

1. 出力画面を閉じて、Stream Analytics ジョブ ページに戻ります。

### タスク 8: Stream Analytics クエリを定義する。

1. **socialtwitter-asa-job** ウィンドウで、ウィンドウ中央の [**クエリ**] 画面で[**Edit query**] (クエリの編集) をクリックします。

1. コード エディタで次のクエリを置き換えます。

    ```SQL
    SELECT 
     [Topic]
    ,[SentimentScore]
    ,[created_at]
    ,[Author]
    ,[text]
    FROM [TwitterStream]
    ```

1. Replace with

    ```SQL
    SELECT 
     [Topic]
    ,[SentimentScore]
    ,[created_at]
    ,[Author]
    ,[text]
    INTO [Outputs]
    FROM [TwitterStream]
    ```

1. [保存] を選択します。

1. [クエリ] ウィンドウを閉じて、Stream Analytics ジョブ ページに戻ります。

### タスク 9: Streaming Analytics ジョブを開始する。

1. **socialtwitter-asa-job** ウィンドウで、ウィンドウ中央の [**クエリ**] 画面で[**開始**] をクリックします。
 
1. [**ジョブの開始**] ダイアログ ボックスで、[**今すぐ**] をクリックし、[**開始**] をクリックします。 

>**注記**: **socialtwitter-asa-job** ウィンドウに、ジョブが開始された 1 分後にメッセージが表示され、開始フィールドが開始時刻に変更されます。

>**注記**: データをキャプチャできるように、2 分間実行したままにします。

### タスク 10: Stream Analytics クエリを定義する。

1. Azure portal 内のブレードで、 [**Resource groups**] (リソース グループ) をクリックし、**awrgstudxx** をクリックし、**awsastudxx** をクリックします。**xx** がイニシャルとなります。

1. Azure portal で、 [**BLOB**] 画面をクリックします。 

1. Azure portal の [**awsastudxx - BLOB**] 画面で、リストから **ツイート** 項目をクリックします。

1. JSON ファイルが表示されたことを確認し、サイズ列をメモします。

1. Microsoft Edge を更新すると、ファイルのサイズではなく画面が更新されます、

    >**注記**: ファイルをダウンロードして JSON データを照会し、Power BI にデータを出力することもできます。

> **結果**: このエクササイズを完了すると、Azure Stream Analytics を構成し、Azure Blob の JSON ファイル ストアにストリーミング データを収集することができます。Twitter データのストリーミングを使って行います。

## 閉じます

1. Azure portal 内のブレードで、 [**Resource groups**] (リソース グループ) をクリックし、**awrgstudxx** をクリックし、**socialtwitter-asa-job** をクリックします。

1. **socialtwitter-asa-job** 画面で、[**停止**] をクリックします。    [**ストリーミング ジョブの停止**] ダイアログ ボックスで、[**はい**] をクリックします。

1. **TwitterWPFClient.exe** アプリケーションを閉じます。