---
title: '方法: 特定のリスト インスタンスに対するイベント レシーバーを作成する | Microsoft Docs'
titleSuffix: ''
description: 特定のリスト インスタンスに対するイベント レシーバーを作成します。 リスト インスタンスのイベント レシーバーは、リスト定義の任意のインスタンスで発生するイベントに応答します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
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
ms.openlocfilehash: 664a7ac4e763b2378cf30603c417aacde27c2e47
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925494"
---
# <a name="how-to-create-an-event-receiver-for-a-specific-list-instance"></a>方法: 特定のリスト インスタンスに対するイベント レシーバーを作成する
  リスト インスタンスのイベント レシーバーは、リスト定義の任意のインスタンスで発生するイベントに応答します。 イベント レシーバー テンプレートでは、特定のリスト インスタンスのターゲット設定が有効になっていませんが、特定のリスト インスタンスのイベントに応答するように、リスト定義にスコープ設定されているイベント レシーバーを変更することができます。

 特定のリスト インスタンスを対象にするには、イベント レシーバーの *Elements.xml* で、`ListTemplateId` を `ListUrl` に置き換え、リスト インスタンスの URL を追加します。

## <a name="create-a-list-instance-event-receiver"></a>リスト インスタンスのイベント レシーバーを作成する
 次の手順では、カスタムのお知らせリスト インスタンスで発生したイベントにのみ応答するようにリスト項目イベント レシーバーを変更する方法を示します。

#### <a name="to-modify-an-event-receiver-to-respond-to-a-specific-list-instance"></a>特定のリスト インスタンスに応答するようにイベント レシーバーを変更するには

1. ブラウザーで SharePoint サイトを開きます。

2. ナビゲーション ウィンドウの **[リスト]** リンク。

3. **[すべてのサイト コンテンツ]** ページで、 **[作成]** リンクを選択します。

4. **[作成]** ダイアログ ボックスで、 **[お知らせ]** の種類を選択し、お知らせの **TestAnnouncements** に名前を指定して、 **[作成]** ボタンを選択します。

5. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でイベント レシーバー プロジェクトを作成します。

6. **[使用するイベント レシーバーの種類]** 一覧で、 **[リスト項目イベント]** を選択します。

    > [!NOTE]
    > **[リスト電子メール イベント]** や **[リスト ワークフロー イベント]** などのリスト定義にスコープを持つ他の種類のイベント レシーバーを選択することもできます。

7. **[イベント ソースとなる項目]** 一覧で、 **[お知らせ]** を選択します。

8. **[次のイベントを処理]** 一覧で、 **[項目が追加されています]** チェック ボックスをオンにして **[完了]** ボタンを選択します。

9. **ソリューション エクスプローラー** の [EventReceiver1] で、*Elements.xml* を開きます。

     イベント レシーバーでは、現在、次の行を使用してお知らせリスト定義を参照しています。

    ```xml
    <Receivers ListTemplateId="104">
    ```

     この行を次のテキストに変更します。

    ```xml
    <Receivers ListUrl="Lists/TestAnnouncements">
    ```

     これにより、イベント レシーバーは、先ほど作成した新しい **TestAnnouncements** お知らせリストで発生したイベントにのみ応答します。 `ListURL` 属性を変更して、SharePoint サーバー上の任意のリスト インスタンスを参照することができます。

10. イベント レシーバーのコード ファイルを開き、ItemAdding メソッドにブレークポイントを設定します。

11. ソリューションをビルドして実行するには、**F5** キーを押します。

12. SharePoint で、ナビゲーション ウィンドウの **[TestAnnouncements]** リンクを選択します。

13. **[新しいお知らせの追加]** リンクを選択します。

14. お知らせのタイトルを入力して、 **[保存]** ボタンを選択します。

     新しい項目がカスタムのお知らせリストに追加されると、ブレークポイントにヒットします。

15. **F5** キーを押して再開します。

16. ナビゲーション ウィンドウで、 **[リスト]** リンクを選択し、 **[お知らせ]** リンクを選択します。

17. 新しいお知らせを追加します。

     レシーバーはカスタムのお知らせリスト インスタンス **TestAnnouncements** のイベントにのみ応答するように構成されているため、新しいお知らせでイベント レシーバーがトリガーされないことに注意してください。

## <a name="see-also"></a>関連項目
- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
