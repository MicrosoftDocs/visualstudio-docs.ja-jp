---
title: SharePoint プロジェクト項目の拡張 | Microsoft Docs
description: SharePoint プロジェクト項目を拡張するためのタスクを確認します。 プロジェクト項目の拡張機能とプロジェクト項目のインスタンスがどのように関連しているかを理解します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e8486120b0f08077bc30c2a5177a8aba915c37f4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948675"
---
# <a name="extend-sharepoint-project-items"></a>SharePoint プロジェクト項目の拡張
  Visual Studio に既にインストールされている SharePoint プロジェクト項目の種類に機能を追加したい場合は、プロジェクト項目の拡張機能を作成します。 たとえば、Visual Studio で組み込みの "**イベント レシーバー**" または "**リスト定義**" プロジェクト項目の拡張機能を作成したり、カスタムのプロジェクト項目の種類の拡張機能を作成したりすることができます。 また、すべての種類の SharePoint プロジェクト項目の拡張機能を作成することもできます。

## <a name="tasks-for-extending-sharepoint-project-items"></a>SharePoint プロジェクト項目を拡張するためのタスク
 プロジェクト項目を拡張するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> インターフェイスを実装する Visual Studio 拡張機能アセンブリをビルドします。 詳細については、「[方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)」を参照してください。

 プロジェクト項目を拡張する場合は、プロジェクト項目に次の機能を追加することもできます。

- ショートカット メニュー項目をプロジェクト項目に追加します。 メニュー項目は、**ソリューション エクスプローラー** でプロジェクト項目のショートカット メニューを開くと表示されます。 ショートカット メニューを開くには、プロジェクト項目を右クリックするか、選択してから **Shift**+**F10** キーを押します。 詳細については、[ショートカット メニュー項目を SharePoint プロジェクト項目の拡張機能に追加する方法](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)に関するページを参照してください。

- カスタム プロパティをプロジェクト項目に追加します。 プロパティは、**ソリューション エクスプローラー** でプロジェクト項目が選択されたときに、 **[プロパティ]** ウィンドウに表示されます。 詳細については、「[方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)」を参照してください。

  プロジェクト項目の拡張機能を作成、配置、およびテストする方法を示すチュートリアルについては、[SharePoint プロジェクト項目の種類の拡張のチュートリアル](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)に関するページを参照してください。

## <a name="understand-the-relationship-between-project-item-extensions-and-project-item-instances"></a>プロジェクト項目の拡張機能とプロジェクト項目のインスタンスの関係を理解する
 プロジェクト項目の拡張機能を作成すると、関連付けられている種類のプロジェクト項目が SharePoint プロジェクトに追加されたときに、Visual Studio によって拡張機能が読み込まれます。 たとえば、"**イベント レシーバー**" プロジェクト項目の拡張機能を作成すると、ユーザーが "**イベント レシーバー**" プロジェクト項目をプロジェクトに追加したときに、Visual Studio によって拡張機能が読み込まれます。 Visual Studio では、関連付けられているプロジェクト項目の種類のすべてのインスタンスに対して、拡張機能の同じインスタンスが使用されます。 前の例では、ユーザーが 2 つ目の "**イベント レシーバー**" プロジェクト項目をプロジェクトに追加した場合、2 つ目のプロジェクト項目をカスタマイズするために、拡張機能の同じインスタンスが使用されます。

 拡張するプロジェクト項目の種類の特定のインスタンスにアクセスするには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> メソッドの実装で *projectItemType* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> イベントの 1 つを処理します。 たとえば、拡張する種類のプロジェクト項目がいつプロジェクトに追加されたかを確認するには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> イベントを処理します。 詳細については、「[方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)」を参照してください。

## <a name="identifiers-for-sharepoint-project-items"></a>SharePoint プロジェクト項目の識別子
 それぞれの SharePoint プロジェクト項目には、対応する文字列識別子があります。 次のタスクを実行する場合は、プロジェクト項目の識別子を把握しておく必要があります。

- プロジェクト項目の拡張機能を作成する。 この場合、拡張するプロジェクト項目の識別子を <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> のコンストラクターに渡す必要があります。 すべてのプロジェクト項目の種類の拡張機能を作成するには、 **\\** * 文字列値を渡します。

- プロジェクト項目をプログラムによってプロジェクトに追加する。 この場合は、プロジェクト項目の識別子を <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemCollection.Add%2A> メソッドに渡す必要があります。

  次の表に、Visual Studio に含まれている SharePoint プロジェクト項目の識別子を示します。

|プロジェクト項目名|文字列識別子|
|-----------------------|-----------------------|
|ビジネス データ カタログ モデル|Microsoft.VisualStudio.SharePoint.BusinessDataConnectivity|
|コンテンツの種類|Microsoft.VisualStudio.SharePoint.ContentType|
|イベント レシーバー|Microsoft.VisualStudio.SharePoint.EventHandler|
|空の要素|Microsoft.VisualStudio.SharePoint.GenericElement|
|リスト定義<br /><br /> コンテンツ タイプからのリスト定義|Microsoft.VisualStudio.SharePoint.ListDefinition|
|リスト インスタンス|Microsoft.VisualStudio.SharePoint.ListInstance|
|モジュール|Microsoft.VisualStudio.SharePoint.Module|
|シーケンシャル ワークフロー<br /><br /> ステート マシン ワークフロー|Microsoft.VisualStudio.SharePoint.Workflow|
|サイトの定義|Microsoft.VisualStudio.SharePoint.SiteDefinition|
|可視 Web パーツ|Microsoft.VisualStudio.SharePoint.VisualWebPart|
|Web パーツ|Microsoft.VisualStudio.SharePoint.WebPart|
|ワークフロー関連付けフォーム|Microsoft.VisualStudio.SharePoint.WorkflowAssociation|

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [方法: ショートカット メニュー項目を SharePoint プロジェクト項目の拡張機能に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [チュートリアル: SharePoint プロジェクト項目の種類を拡張する](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
