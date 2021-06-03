---
title: '方法: SharePoint プロジェクトにショートカット メニュー項目を追加する | Microsoft Docs'
titleSuffix: ''
description: Visual Studio の SharePoint プロジェクトにショートカット メニュー項目を追加します。 メニュー項目は、ソリューション エクスプローラーのプロジェクト ノードを右クリックしたときに表示されます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 54ac53ad317f500e787baebfdfeb4a86dc917e06
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216814"
---
# <a name="how-to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>方法: SharePoint プロジェクトにショートカット メニュー項目を追加する
  任意の SharePoint プロジェクトにショートカット メニュー項目を追加できます。 メニュー項目は、ユーザーが **ソリューション エクスプローラー** のプロジェクト ノードを右クリックしたときに表示されます。

 次の手順では、プロジェクトの拡張機能が既に作成されていることを前提にしています。 詳細については、「[方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)」を参照してください。

### <a name="to-add-a-shortcut-menu-item-to-sharepoint-projects"></a>SharePoint プロジェクトにショートカット メニュー項目を追加するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 実装の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> メソッドで、*projectService* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> イベントを処理します。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectMenuItemsRequested> イベントのイベント ハンドラーで、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.ActionMenuItems%2A> または <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectMenuItemsRequestedEventArgs.AddMenuItems%2A> コレクションに新しい <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> オブジェクトを追加します。

3. 新しい <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> イベント ハンドラーで、ユーザーがショートカット メニュー項目をクリックしたときに実行するタスクを実行します。

## <a name="example"></a>例
 次のコード例は、**ソリューション エクスプローラー** の SharePoint プロジェクト ノードにショートカット メニュー項目を追加する方法を示しています。 ユーザーがプロジェクト ノードを右クリックし、 **[出力ウィンドウにメッセージを書き込む]** メニュー項目をクリックすると、Visual Studio では **[出力]** ウィンドウにメッセージを表示します。 この例では、SharePoint プロジェクト サービスを使用してメッセージを表示します。 詳細については、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectmenu/extension/projectitemextensionmenu.cs" id="Snippet1":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectmenu/extension/projectitemextensionmenu.vb" id="Snippet1":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照を含むクラス ライブラリ プロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトを拡張する](../sharepoint/extending-sharepoint-projects.md)
- [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
