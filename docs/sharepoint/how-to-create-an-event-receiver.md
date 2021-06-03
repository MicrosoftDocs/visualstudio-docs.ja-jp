---
title: '方法: イベント レシーバーを作成する | Microsoft Docs'
description: ユーザーがリストやリスト項目などの SharePoint 項目を操作したときに応答できるように、イベント レシーバーを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.EventReceiver
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, event receivers
- event receivers [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d0eebee6e37fbd6696923da0e470f05688fa0387
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216580"
---
# <a name="how-to-create-an-event-receiver"></a>方法: イベント レシーバーを作成する
  *イベント レシーバー* を作成することによって、ユーザーがリストやリスト項目などの SharePoint 項目を操作したときに応答できます。 たとえば、ユーザーが予定表を変更するか、または連絡先リストから名前を削除したときに、イベント レシーバー内のコードをトリガーできます。 このトピックに従うことによって、リスト インスタンスにイベント レシーバーを追加する方法を学習できます。

 次の手順を完了するには、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と、Windows および SharePoint のサポートされるエディションがインストールされている必要があります。 この例には SharePoint プロジェクトが必要なため、トピック「[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)」の手順を完了していることも必要です。

## <a name="adding-an-event-receiver"></a>イベント レシーバーの追加
 「[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)」で作成したプロジェクトには、カスタム サイト列、カスタム リスト、コンテンツ タイプが含まれています。 次の手順では、リストなどの SharePoint 項目で発生するイベントを処理する方法を示すために、リスト インスタンスに単純なイベント ハンドラー (イベント レシーバー) を追加することによってこのプロジェクトを拡張します。

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>リスト インスタンスにイベント レシーバーを追加するには

1. 「[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)」で作成したプロジェクトを開きます。

2. **ソリューション エクスプローラー** で、**Clinic** という名前の SharePoint プロジェクト ノードを選択します。

3. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

4. **[Visual C#]** または **[Visual Basic]** のどちらかで、 **[SharePoint]** ノードを展開し、 **[2010]** 項目を選択します。

5. **[テンプレート]** ウィンドウで、 **[イベント レシーバー]** を選択し、それに **TestEventReceiver1** という名前を付けてから **[OK]** ボタンを選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

6. **[使用するイベント レシーバーの種類]** 一覧で、 **[リスト項目イベント]** を選択します。

7. **[イベント ソースとなる項目]** 一覧で、 **[患者 (Clinic\Patients)]** を選択します。

8. **[次のイベントを処理]** 一覧で、 **[項目が追加されました]** の横にあるチェック ボックスをオンにして **[完了]** ボタンを選択します。

     新しいイベント レシーバーのコード ファイルには、`ItemAdded` という名前の 1 つのメソッドが含まれています。 次の手順では、このメソッドにコードを追加して、既定ではすべての連絡先に Scott Brown という名前が付けられるようにします。

9. 既存の `ItemAdded` メソッドを次のコードに置き換えてから、**F5** キーを選択します。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb" id="Snippet1":::

     このコードが実行され、SharePoint サイトが Web ブラウザーに表示されます。

10. クイック起動バーで、 **[患者]** リンクを選択してから **[新しい項目の追加]** リンクを選択します。

     新しい項目の入力フォームが開きます。

11. フィールドにデータを入力し、 **[保存]** ボタンを選択します。

     **[保存]** ボタンを選択すると、 **[患者名]** 列が自動的に Scott Brown という名前に更新されます。

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)