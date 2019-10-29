﻿---
lab:
    title: 'Azure アーキテクチャに関する考慮事項'
    module: 'モジュール 1: Azure アーキテクチャに関する考慮事項'
---

# DP 201 - Azure Data プラットフォーム ソリューションの設計
# ラボ 1 - Azure アーキテクチャに関する考慮事項

**推定時間**：60 分

**前提条件**：このラボのケース スタディを確認済みであること。

**ラボ ファイル**：このラボのファイルは _Allfiles\Labfiles\Starter\DP-201.1_フォルダにあります。

## ラボの概要

学生は、このモジュールで取得した情報を使用して、AdventureWorks に関するケース スタディで定義されたシナリオに適用します。アーキテクチャを作成するコア プリンシパルを AdventureWorks に適用する例を説明し、提供することになります。これには、セキュリティを念頭に置いた設計が含まれます。また、ソリューションでパフォーマンスとスケーラビリティを設計する方法の具体的な例も示します。学生達は組織で必要とされる可用性と回復可能性のオプションについても説明します。最後に、学生は、オプションによって得られる効率性と操作機会を識別します。

## ラボの目標
  
このモジュールを終了した後、次のことができるようになります：

1. 安全性を念頭に置いて設計する
2. パフォーマンスとスケーラビリティ用の設計
3. 可用性と回復性のために設計する
4. 効率性と運用のために設計する

## シナリオ
  
最近、AdventureWorks のシニア データ エンジニアとして採用され、コンサルタントやアーキテクトと協力して、組織の技術的およびビジネス要件を満たすクラウド データ プラットフォーム ソリューションを設計しています。

グループで作業する場合、コンサルタントやアーキテクトと一緒にケーススタディを通じて検出演習を行います。まず、AdventureWorks の組織目標を理解します。次に、ソリューション アーキテクチャを構築する場合にチームが認識する必要があるアーキテクチャの側面の例を明確にし、提供します。アーキテクチャの側面には、セキュリティ、パフォーマンス、スケーラビリティ、可用性、回復性、効率性、操作が含まれます。

このラボの最後には、次の操作が行われます。

1. 安全性を念頭に置いて設計する
2. パフォーマンスとスケーラビリティ用の設計
3. 可用性と回復性のために設計する
4. 効率性と運用のために設計する

>**注**：このラボは 2 つの部分に分かれています。これはグループして質問に答えるパート 1 です。各演習のタイミングは、グループの裁量に任せます。ラボ全体は 60 分以内に完了する必要があります。第 2 部分では、講師がラボに関する学習と調査結果についてグループとディスカッションを行います。

>**リソース**：このラボのコース ケース スタディの使用に加えて、[マイクロソフト ドキュメント](https://docs.microsoft.com) [Azure リファレンス アーキテクチャ サイト](https://docs.microsoft.com/ja-jp/azure/architecture/reference-architectures/)および [マイクロソフト カスタマー ストーリー サイト](https://customers.microsoft.com/)などのリソースを使用して、このラボの質問回答の通知に役立ちます。 

## 演習 1：安全性を念頭に置いて設計する

**グループ演習**
  
この演習の主なタスクは次のとおりです。

1. ケース スタディから、AdventureWorks のセキュリティ要件を特定します。

### タスク 1：AdventureWorks のセキュリティ要件を特定します。

1. コンピュータから **Microsoft Word** を起動 し、ファイル **DP-201-Lab01.docx** を **Allfiles\Labfiles\Starter\DP-201.1** フォルダから開きます。

1. グループとして、ケース スタディ ドキュメントでグループが特定したセキュリティ要件について **15 分間** 説明し、リストします。ケーススタディから証拠を提供する必要があります。

> **結果**：この演習を完了したら、AdventureWorks のセキュリティ要件の表を示す Microsoft Word ドキュメントを作成しました。

## 演習 2：パフォーマンスとスケーラビリティ用の設計
  
**グループ演習**
  
この演習の主なタスクは次のとおりです：

1. ケース スタディから識別されるパフォーマンスとスケーラビリティの要件を決定します。

### タスク 1：AdventureWorks のパフォーマンスとスケーラビリティの要件を特定します。

1. コンピュータから **Microsoft Word** を起動 し、ファイル **DP-200-Lab01.docx** を **Allfiles\Labfiles\Starter\DP-200.1** フォルダから開きます。

1. グループとして、ケーススタディ ドキュメント内でグループが特定したパフォーマンスとスケーラビリティの要件について **15 分間** 説明し、リストします。ケーススタディから証拠を提供する必要があります。

> **結果**：この演習を完了したら、AdventureWorks のセキュリティ要件の表を示す Microsoft Word ドキュメントを作成しました。

## 演習 3：可用性と回復性のために設計する
  
**グループ演習**
  
この演習の主なタスクは次のとおりです：

1. ケース スタディから識別される可用性と回復性の要件を決定します。

### タスク 1：AdventureWorks の可用性と回復性の要件を特定します。

1. コンピュータから **Microsoft Word** を起動 し、ファイル **DP-200-Lab01.docx** を **Allfiles\Labfiles\Starter\DP-200.1** フォルダから開きます。

1. グループとして、AdventureWorks の スケーリングのメリットを得るサービスについて **15 分間** 話し合い、記録します。ケーススタディから証拠を提供する必要があります。

> **結果**：この演習を完了したら、AdventureWorks のセキュリティ要件の表を示す Microsoft Word ドキュメントを作成しました。

## 演習 4：効率性と運用のために設計する
  
**グループ演習**
  
この演習の主なタスクは次のとおりです：

1. AdventureWorks の効率性と操作要件を決定します。

### タスク 1：AdventureWorks の効率性と操作要件を特定します。

1. コンピュータから **Microsoft Word** を起動 し、ファイル **DP-200-Lab01.docx** を **Allfiles\Labfiles\Starter\DP-200.1** フォルダから開きます。

1. グループとして、AdventureWorks の スケーリングのメリットを得るサービスについて **15 分間** 話し合い、記録します。ケーススタディから証拠を提供する必要があります。

> **結果**：この演習を完了したら、AdventureWorks のセキュリティ要件の表を示す Microsoft Word ドキュメントを作成しました。

## ラボ レビュー

約 60 分後、インストラクターがこの演習の近くに集めます。各グループの調査結果について話し合います。