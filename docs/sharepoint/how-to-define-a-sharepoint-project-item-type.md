---
title: '方法: SharePoint プロジェクト項目の種類を定義する | Microsoft Docs'
description: カスタムの SharePoint プロジェクト項目を作成する際の、プロジェクト項目の種類の定義方法について説明します。
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
ms.openlocfilehash: 16e7070769edf3ee65ee425a7f9cb5062da315cd
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216827"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>方法: SharePoint プロジェクト項目の種類を定義する
  カスタムの SharePoint プロジェクト項目を作成する場合には、プロジェクト項目の種類を定義します。 詳しくは、「[カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)」をご覧ください。

### <a name="to-define-a-project-item-type"></a>プロジェクト項目の種類を定義するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスを実装するクラスを作成します。

4. クラスに次の属性を追加します。

    - <xref:System.ComponentModel.Composition.ExportAttribute>. この属性を使用すると、Visual Studio で <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 実装を検出して読み込むことができます。 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 型を属性コンストラクターに渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. プロジェクト項目の種類の定義では、この属性で、新しいプロジェクト項目の文字列識別子を指定します。 <*会社名*>.<*機能名*> という形式を使用して、すべてのプロジェクト項目が一意の名前を持つようにすることをお勧めします。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>. この属性では、**ソリューション エクスプローラー** でこのプロジェクト項目に対して表示するアイコンを指定します。 この属性は省略可能です。これをクラスに適用しなかった場合、Visual Studio では、そのプロジェクト項目に既定のアイコンが表示されます。 この属性を設定する場合は、アセンブリに埋め込まれているアイコンまたはビットマップの完全修飾名を渡します。

5. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドの実装で、*projectItemTypeDefinition* パラメーターのメンバーを使って、プロジェクト項目の種類の動作を定義します。 このパラメーターは、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> および <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> インターフェイスで定義されたイベントへのアクセスを提供する <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> オブジェクトです。 プロジェクト項目の種類の特定のインスタンスにアクセスするには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> や <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> などの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> イベントを処理します。

## <a name="example"></a>例
 次のコード例は、シンプルなプロジェクト項目の種類の定義方法を示したものです。 このプロジェクト項目の種類では、ユーザーがこの種類のプロジェクト項目をプロジェクトに追加したときに、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージが書き込まれます。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb" id="Snippet2":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs" id="Snippet2":::

 この例では、SharePoint プロジェクト サービスを使用して、 **[出力]** ウィンドウと **[エラー一覧]** ウィンドウにメッセージが書き込みます。 詳しくは、「[SharePoint プロジェクト サービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」をご覧ください。

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>プロジェクト項目を配置する
 自分が定義したプロジェクト項目を他の開発者が使用できるようにするには、プロジェクト テンプレートまたはプロジェクト項目テンプレートを作成します。 詳しくは、「[SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」をご覧ください。

 プロジェクト項目を配置するには、プロジェクト項目と共に配布するアセンブリ、テンプレート、およびその他のファイルを含んだ [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳しくは、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [方法: プロパティをカスタムの SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [方法: ショートカット メニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
