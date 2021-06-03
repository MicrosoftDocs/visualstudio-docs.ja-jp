---
title: SharePoint プロジェクト項目の拡張機能にショートカット メニュー項目を追加する
titleSuffix: ''
description: Visual Studio のプロジェクト項目の拡張機能を使用して、既存の SharePoint プロジェクト項目にショートカット メニュー項目を追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
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
ms.openlocfilehash: bac5ff10ea59ba422a9dc33855919eb999a996ee
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215397"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension"></a>方法: SharePoint プロジェクト項目の拡張機能にショートカット メニュー項目を追加する
  プロジェクト項目の拡張機能を使用して、既存の SharePoint プロジェクト項目にショートカット メニュー項目を追加できます。 メニュー項目は、ユーザーが **ソリューション エクスプローラー** のプロジェクト項目を右クリックしたときに表示されます。

 次の手順では、プロジェクト項目の拡張機能が既に作成されていることを前提にしています。 詳細については、「[方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)」を参照してください。

### <a name="to-add-a-shortcut-menu-item-in-a-project-item-extension"></a>プロジェクト項目の拡張機能にショートカット メニュー項目を追加するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 実装の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> メソッドで、*projectItemType* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> イベントを処理します。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> イベントのイベント ハンドラーで、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> または <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> コレクションに新しい <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> オブジェクトを追加します。

3. 新しい <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> イベント ハンドラーで、ユーザーがショートカット メニュー項目をクリックしたときに実行するタスクを実行します。

## <a name="example"></a>例
 次のコード例は、イベント レシーバー プロジェクト項目にショートカット メニュー項目を追加する方法を示しています。 **ソリューション エクスプローラー** でユーザーがプロジェクト項目を右クリックし、 **[出力ウィンドウにメッセージを書き込む]** メニュー項目をクリックすると、Visual Studio では **[出力]** ウィンドウにメッセージを表示します。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionmenu.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionmenu.cs" id="Snippet1":::

 この例では、SharePoint プロジェクト サービスを使用して、 **[出力]** ウィンドウにメッセージを書き込みます。 詳細については、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照を含むクラス ライブラリ プロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する](../sharepoint/how-to-add-a-property-to-a-sharepoint-project-item-extension.md)
- [SharePoint プロジェクト項目を拡張する](../sharepoint/extending-sharepoint-project-items.md)
- [チュートリアル: SharePoint プロジェクト項目の種類を拡張する](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
