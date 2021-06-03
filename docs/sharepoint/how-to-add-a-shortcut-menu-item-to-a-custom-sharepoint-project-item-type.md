---
title: カスタム SharePoint プロジェクト項目の種類にショートカット メニュー項目を追加する
titleSuffix: ''
description: カスタム SharePoint プロジェクト項目の種類にショートカット メニュー項目を追加する方法について説明します。 メニュー項目は、ソリューション エクスプローラーのプロジェクト項目を右クリックしたときに表示されます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3e4523d0f992ed72c9af2eb7e542f902578f9338
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215384"
---
# <a name="how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type"></a>方法: カスタム SharePoint プロジェクト項目の種類にショートカット メニュー項目を追加する
  カスタム SharePoint プロジェクト項目の種類を定義する場合は、そのプロジェクト項目にショートカット メニュー項目を追加できます。 メニュー項目は、ユーザーが **ソリューション エクスプローラー** のプロジェクト項目を右クリックしたときに表示されます。

 次の手順では、独自の SharePoint プロジェクト項目の種類が既に定義されていることを前提にしています。 詳細については、「[方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)」を参照してください。

### <a name="to-add-a-shortcut-menu-item-to-a-custom-project-item-type"></a>カスタム プロジェクト項目の種類にショートカット メニュー項目を追加するには

1. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 実装の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドで、*projectItemTypeDefinition* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> イベントを処理します。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemMenuItemsRequested> イベントのイベント ハンドラーで、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.ViewMenuItems%2A> または <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemMenuItemsRequestedEventArgs.AddMenuItems%2A> コレクションに新しい <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> オブジェクトを追加します。

3. 新しい <xref:Microsoft.VisualStudio.SharePoint.IMenuItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.IMenuItem.Click> イベント ハンドラーで、ユーザーがショートカット メニュー項目を選択したときに実行するタスクを実行します。

## <a name="example"></a>例
 次のコード例は、カスタム プロジェクト項目の種類にコンテキスト メニュー項目を追加する方法を示しています。 **ソリューション エクスプローラー** でユーザーがプロジェクト項目のショートカット メニューを開き、 **[出力ウィンドウにメッセージを書き込む]** メニュー項目を選択すると、Visual Studio では **[出力]** ウィンドウにメッセージを表示します。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypemenu.cs" id="Snippet4":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypemenu.vb" id="Snippet4":::

 この例では、SharePoint プロジェクト サービスを使用して、 **[出力]** ウィンドウにメッセージを書き込みます。 詳細については、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照を含むクラス ライブラリ プロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>プロジェクト項目を配置する
 他の開発者がこのプロジェクト項目を使用できるようにするには、プロジェクト テンプレートまたはプロジェクト項目テンプレートを作成します。 詳細については、[SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートの作成](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)に関するページを参照してください。

 プロジェクト項目を配置するには、そのプロジェクト項目で配布するアセンブリ、テンプレート、その他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [方法: プロパティをカスタムの SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [カスタム SharePoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)
