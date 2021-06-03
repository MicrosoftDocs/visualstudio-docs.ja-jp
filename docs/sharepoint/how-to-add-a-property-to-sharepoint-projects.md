---
title: '方法: SharePoint プロジェクトにプロパティを追加する | Microsoft Docs'
description: プロジェクトの拡張機能を使用して SharePoint プロジェクトにプロパティを追加します。 プロパティは、ソリューション エクスプローラーでプロジェクトを選択したときに [プロパティ] ウィンドウに表示されます。
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
ms.openlocfilehash: 7be241dd4a043b8104c628e73f98e8881dc8b88b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215423"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>方法: SharePoint プロジェクトにプロパティを追加する
  プロジェクトの拡張機能を使用すると、任意の SharePoint プロジェクトにプロパティを追加できます。 このプロパティは、**ソリューション エクスプローラー** でプロジェクトが選択されたときに **[プロパティ]** ウィンドウに表示されます。

 次の手順では、プロジェクトの拡張機能が既に作成されていることを前提にしています。 詳細については、「[方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)」を参照してください。

### <a name="to-add-a-property-to-a-sharepoint-project"></a>SharePoint プロジェクトにプロパティを追加するには

1. SharePoint プロジェクトに追加しようとしているプロパティを表すパブリック プロパティを持つクラスを定義します。 複数のプロパティを追加する場合は、すべてのプロパティを同じクラスで定義することも、異なるクラスで定義することもできます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 実装の <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> メソッドで、*projectService* パラメーターの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> イベントを処理します。

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> イベントのイベント ハンドラーで、イベント引数パラメーターの <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> コレクションにプロパティ クラスのインスタンスを追加します。

## <a name="example"></a>例
 次のコード例は、SharePoint プロジェクトに 2 つのプロパティを追加する方法を示しています。 1 つのプロパティでは、そのデータをプロジェクト ユーザー オプション ファイル ( *.csproj.user* ファイルまたは *.vbproj.user* ファイル) に保持します。 もう 1 つのプロパティでは、そのデータをプロジェクト ファイル ( *.csproj* ファイルまたは *.vbproj* ファイル) に保持します。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet1":::

### <a name="understand-the-code"></a>コードの理解
 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> イベントが発生するたびに `CustomProjectProperties` クラスの同じインスタンスが確実に使用されるようにするために、このコード例では、このイベントが初めて発生したときにプロジェクトの <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティにプロパティ オブジェクトを追加します。 このコードでは、このイベントが再び発生するたびに、このオブジェクトを取得します。 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロパティを使用してプロジェクトにデータを関連付ける方法の詳細については、「[カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

 プロパティ値への変更を保持するために、プロパティの **set** アクセサーでは、次の API を使用します。

- `CustomUserFileProperty` では、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> プロパティを使用して、その値をプロジェクト ユーザー オプション ファイルに保存します。

- `CustomProjectFileProperty` では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> メソッドを使用して、その値をプロジェクト ファイルに保存します。

  これらのファイル内のデータの保持の詳細については、「[SharePoint プロジェクト システムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)」を参照してください。

### <a name="specify-the-behavior-of-custom-properties"></a>カスタム プロパティの動作を指定する
 <xref:System.ComponentModel> 名前空間の属性をプロパティ定義に適用することによって、 **[プロパティ]** ウィンドウでのカスタム プロパティの表示や動作を定義できます。 次の属性は、多くのシナリオで役立ちます。

- <xref:System.ComponentModel.DisplayNameAttribute>: **[プロパティ]** ウィンドウに表示されるプロパティの名前を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>: プロパティが選択されたときに **[プロパティ]** ウィンドウの下部に表示される説明文字列を指定します。

- <xref:System.ComponentModel.DefaultValueAttribute>: プロパティの既定値を指定します。

- <xref:System.ComponentModel.TypeConverterAttribute>: **[プロパティ]** ウィンドウに表示される文字列と、文字列以外のプロパティ値の間のカスタム変換を指定します。

- <xref:System.ComponentModel.EditorAttribute>: プロパティを変更するために使用するカスタム エディターを指定します。

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.Shell

- Microsoft.VisualStudio.Shell.Interop

- Microsoft.VisualStudio.Shell.Interop.8.0

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトを拡張する](../sharepoint/extending-sharepoint-projects.md)
- [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [方法: ショートカット メニュー項目を SharePoint プロジェクトに追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
