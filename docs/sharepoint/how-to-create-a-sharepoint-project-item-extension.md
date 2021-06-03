---
title: '方法: SharePoint プロジェクト項目の拡張機能を作成する | Microsoft Docs'
description: Visual Studio に既にインストールされている SharePoint プロジェクト項目に機能を追加したい場合にプロジェクト項目の拡張機能を作成する方法について説明します。
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
ms.openlocfilehash: 8f01d3c15490a19c8cb5071cf7677fcf2b2a5384
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216619"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>方法: SharePoint プロジェクト項目の拡張機能を作成する
  Visual Studio に既にインストールされている SharePoint プロジェクト項目に機能を追加したい場合は、プロジェクト項目の拡張機能を作成します。 詳細については、[SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)に関するページを参照してください。

### <a name="to-create-a-project-item-extension"></a>プロジェクト項目の拡張機能を作成するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> インターフェイスを実装するクラスを作成します。

4. このクラスに次の属性を追加します。

    - <xref:System.ComponentModel.Composition.ExportAttribute>. この属性を使用すると、Visual Studio で <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 実装を検出して読み込むことができます。 属性コンストラクターに <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 型を渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. プロジェクト項目の拡張機能では、この属性で、拡張するプロジェクト項目を識別します。 属性コンストラクターにプロジェクト項目の ID を渡します。 Visual Studio に含まれているプロジェクト項目の ID の一覧については、[SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)に関するページを参照してください。

5. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> メソッドの実装で、*projectItemType* パラメーターのメンバーを使用して拡張機能の動作を定義します。 このパラメーターは、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> および <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> インターフェイスで定義されているイベントへのアクセスを提供する <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> オブジェクトです。 拡張しているプロジェクト項目の種類の特定のインスタンスにアクセスするには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> や <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> などの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> イベントを処理します。

## <a name="example"></a>例
 次のコード例は、イベント レシーバー プロジェクト項目の単純な拡張機能を作成する方法を示しています。 ユーザーが SharePoint プロジェクトにイベント レシーバー プロジェクト項目を追加するたびに、この拡張機能では、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージを書き込みます。

 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs" id="Snippet1":::
 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb" id="Snippet1":::

 この例では、SharePoint プロジェクト サービスを使用して、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージを書き込みます。 詳細については、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目を拡張する](../sharepoint/extending-sharepoint-project-items.md)
- [チュートリアル: SharePoint プロジェクト項目の種類を拡張する](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
