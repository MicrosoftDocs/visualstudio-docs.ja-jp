---
title: '方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する | Microsoft Docs'
titleSuffix: ''
description: Visual Studio に既にインストールされている任意の SharePoint プロジェクト項目にプロパティを追加するには、SharePoint プロジェクト項目の拡張機能を使用します。
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
ms.openlocfilehash: 2634035435679bd5ab2627f803ff9d2c1dc5a863
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215449"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する
  プロジェクト項目の拡張機能を使用すると、Visual Studio に既にインストールされている任意の SharePoint プロジェクト項目にプロパティを追加できます。 このプロパティは、そのプロジェクト項目が **ソリューション エクスプローラー** で選択されたときに **[プロパティ]** ウィンドウに表示されます。

 次の手順では、プロジェクト項目の拡張機能が既に作成されていることを前提にしています。 詳細については、「[方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)」を参照してください。

### <a name="to-add-a-property-to-a-project-item-extension"></a>プロジェクト項目の拡張機能にプロパティを追加するには

1. プロジェクト項目の種類に追加しようとしているプロパティを表すパブリック プロパティを持つクラスを定義します。 プロジェクト項目の種類に複数のプロパティを追加する場合は、すべてのプロパティを同じクラスで定義することも、異なるクラスで定義することもできます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 実装の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> メソッドで、*projectItemType* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> イベントを処理します。

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> イベントのイベント ハンドラーで、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> コレクションにプロパティ クラスのインスタンスを追加します。

## <a name="example"></a>例
 次のコード例は、イベント レシーバー プロジェクト項目に **Example Property** という名前のプロパティを追加する方法を示しています。

:::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs" id="Snippet8":::
:::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb" id="Snippet8":::

### <a name="understand-the-code"></a>コードの理解
 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> イベントが発生するたびに `CustomProperties` クラスの同じインスタンスが確実に使用されるようにするために、このコード例では、このイベントが初めて発生したときにプロジェクト項目の <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティにプロパティ オブジェクトを追加します。 このコードでは、このイベントが再び発生するたびに、このオブジェクトを取得します。 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティを使用してプロジェクト項目にデータを関連付ける方法の詳細については、「[カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

 プロパティ値への変更を保持するために、`ExampleProperty` の **set** アクセサーでは、そのプロパティが関連付けられている <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティに新しい値を保存します。 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティを使用してプロジェクト項目に関するデータを保持する方法の詳細については、「[SharePoint プロジェクト システムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)」を参照してください。

### <a name="specify-the-behavior-of-custom-properties"></a>カスタム プロパティの動作を指定する
 <xref:System.ComponentModel> 名前空間の属性をプロパティ定義に適用することによって、 **[プロパティ]** ウィンドウでのカスタム プロパティの表示や動作を定義できます。 次の属性は、多くのシナリオで役立ちます。

- <xref:System.ComponentModel.DisplayNameAttribute>: **[プロパティ]** ウィンドウに表示されるプロパティの名前を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>: プロパティが選択されたときに **[プロパティ]** ウィンドウの下部に表示される説明文字列を指定します。

- <xref:System.ComponentModel.DefaultValueAttribute>: プロパティの既定値を指定します。

- <xref:System.ComponentModel.TypeConverterAttribute>: **[プロパティ]** ウィンドウに表示される文字列と、文字列以外のプロパティ値の間のカスタム変換を指定します。

- <xref:System.ComponentModel.EditorAttribute>: プロパティを変更するために使用するカスタム エディターを指定します。

## <a name="compile-the-code"></a>コードのコンパイル
 これらの例には、次のアセンブリへの参照を含むクラス ライブラリ プロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [方法: ショートカット メニュー項目を SharePoint プロジェクト項目の拡張機能に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [SharePoint プロジェクト項目を拡張する](../sharepoint/extending-sharepoint-project-items.md)
- [チュートリアル: SharePoint プロジェクト項目の種類を拡張する](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
