---
title: カスタムの SharePoint プロジェクト項目の種類にプロパティを追加する
description: カスタムの SharePoint プロジェクト項目の種類にプロパティを追加します。 プロパティは、ソリューション エクスプローラーでプロジェクト項目が選択されたときに、プロパティ ウィンドウに表示されます。
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
ms.openlocfilehash: 17d9ac144b97c090292395dd5ae5e85319dd1308
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215514"
---
# <a name="how-to-add-a-property-to-a-custom-sharepoint-project-item-type"></a>方法: カスタムの SharePoint プロジェクト項目の種類にプロパティを追加する
  カスタムの SharePoint プロジェクト項目の種類を定義する際には、プロジェクト項目にプロパティを追加できます。 プロパティは、**ソリューション エクスプローラー** でプロジェクト項目が選択されたときに、 **[プロパティ]** ウィンドウに表示されます。

 次の手順では、独自の SharePoint プロジェクト項目の種類が既に定義されていることを前提としています。 詳しくは、「[方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)」をご覧ください。

### <a name="to-add-a-property-to-a-definition-of-a-project-item-type"></a>プロジェクト項目の種類の定義にプロパティを追加するには

1. カスタムのプロジェクト項目の種類に追加するプロパティを表すパブリック プロパティを使って、クラスを定義します。 カスタムのプロジェクト項目の種類に複数のプロパティを追加する場合は、すべてのプロパティを同じクラスで定義することも、異なるクラスで定義することもできます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 実装の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> メソッドで、*projectItemTypeDefinition* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> イベントを処理します。

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> イベントのイベント ハンドラーで、カスタム プロパティ クラスのインスタンスを、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> コレクションに追加します。

## <a name="example"></a>例
 次のコード例は、カスタムのプロジェクト項目の種類に、"**Example Property**" というプロパティを追加する方法を示したものです。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet11":::

### <a name="understand-the-code"></a>コードの理解
 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> イベントが発生するたびに `CustomProperties` クラスの同じインスタンスが使用されるようにするために、このコード例では、このイベントの初回発生時に、プロジェクト項目の <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティにプロパティ オブジェクトが保存されます。 このコードでは、このイベントが再び発生するたびに、このオブジェクトが取得されます。 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティを使ってプロジェクト項目に関連するデータを保存する方法について詳しくは、「[カスタム データと SharePoint ツールの拡張機能の関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」をご覧ください。

 プロパティ値への変更を保持するために、`ExampleProperty` の **set** アクセサーは、プロパティが関連付けられている <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティに新しい値を保存します。 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティを使ってプロジェクト項目に関連するデータを保持する方法について詳しくは、「[SharePoint プロジェクトシステムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)」をご覧ください。

### <a name="specify-the-behavior-of-custom-properties"></a>カスタム プロパティの動作を指定する
 **[プロパティ]** ウィンドウでのカスタム プロパティの表示と動作は、<xref:System.ComponentModel> 名前空間からプロパティ定義に属性を適用することによって定義できます。 次の属性は、多くのシナリオで役立ちます。

- <xref:System.ComponentModel.DisplayNameAttribute>: **[プロパティ]** ウィンドウに表示されるプロパティの名前を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>: プロパティが選択されたときに **[プロパティ]** ウィンドウの下部に表示される説明の文字列を指定します。

- <xref:System.ComponentModel.DefaultValueAttribute>: プロパティの既定値を指定します。

- <xref:System.ComponentModel.TypeConverterAttribute>: **[プロパティ]** ウィンドウに表示される文字列と、文字列以外のプロパティ値との間でのカスタム変換を指定します。

- <xref:System.ComponentModel.EditorAttribute>: プロパティの変更に使用するカスタム エディターを指定します。

## <a name="compile-the-code"></a>コードのコンパイル
 これらのコード例には、次のアセンブリへの参照を含んだクラス ライブラリ プロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>プロジェクト項目を配置する
 自分が定義したプロジェクト項目を他の開発者が使用できるようにするには、プロジェクト テンプレートまたはプロジェクト項目テンプレートを作成します。 詳しくは、「[SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」をご覧ください。

 プロジェクト項目を配置するには、プロジェクト項目と共に配布するアセンブリ、テンプレート、およびその他のファイルを含んだ [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳しくは、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」をご覧ください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [方法: ショートカット メニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [SharePoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)
