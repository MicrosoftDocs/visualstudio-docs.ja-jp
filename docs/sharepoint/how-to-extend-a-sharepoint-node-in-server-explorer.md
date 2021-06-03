---
title: '方法: サーバー エクスプローラーの SharePoint ノードを拡張する | Microsoft Docs'
description: '[SharePoint 接続] ノードを使用して、サーバー エクスプローラーの SharePoint ノードを拡張する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e38f1d18736c18f5273eb2e202de52af81e73f85
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217451"
---
# <a name="how-to-extend-a-sharepoint-node-in-server-explorer"></a>方法: サーバー エクスプローラーの SharePoint ノードを拡張する
  **サーバー エクスプローラー** の **[SharePoint 接続]** ノードの下でノードを拡張できます。 これは、既存のノードに新しい子ノード、ショートカット メニュー項目、またはプロパティを追加する場合に役立ちます。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

### <a name="to-extend-a-sharepoint-node-in-server-explorer"></a>サーバー エクスプローラーの SharePoint ノードを拡張するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.SharePoint.Explorer.Extensions

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> インターフェイスを実装するクラスを作成します。

4. クラスに <xref:System.ComponentModel.Composition.ExportAttribute> 属性を追加します。 この属性を使用すると、Visual Studio で <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 実装を検出して読み込むことができます。 属性コンストラクターに <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 型を渡します。

5. クラスに <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 属性を追加します。 この属性では、拡張するノードの種類の文字列識別子を指定します。

     Visual Studio によって提供される組み込みのノードの種類を指定するには、属性コンストラクターに次のいずれかの列挙値を渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: これらの値は、**サーバー エクスプローラー** のサイト接続ノード (サイト URL を表示するノード)、サイト ノード、またはその他のすべての親ノードを指定するために使用します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: これらの値は、SharePoint サイト上の個々のコンポーネントを表す組み込みノード (リスト、フィールド、またはコンテンツ タイプを表すノードなど) のいずれかを指定するために使用します。

6. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> メソッドの実装で、*nodeType* パラメーターのメンバーを使用してノードに機能を追加します。 このパラメーターは、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> インターフェイスで定義されているイベントへのアクセスを提供する <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> オブジェクトです。 たとえば、次のイベントを処理できます。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested>: ノードに新しい子ノードを追加するには、このイベントを処理します。 詳細については、「[方法: サーバー エクスプローラーにカスタム SharePoint ノードを追加する](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)」を参照してください。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeMenuItemsRequested>: ノードにカスタム ショートカット メニュー項目を追加するには、このイベントを処理します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodePropertiesRequested>: ノードにカスタム プロパティを追加するには、このイベントを処理します。 これらのプロパティは、そのノードが選択されたときに **[プロパティ]** ウィンドウに表示されます。

## <a name="example"></a>例
 次のコード例は、次の 2 つの異なる種類のノード拡張機能を作成する方法を示しています。

- SharePoint サイト ノードにコンテキスト メニュー項目を追加する拡張機能。 このメニュー項目をクリックすると、クリックされたノードの名前が表示されます。

- **Body** という名前のフィールドを表す各ノードに **ContosoExampleProperty** という名前のカスタム プロパティを追加する拡張機能。

  :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextension.cs" id="Snippet9":::
  :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextension.vb" id="Snippet9":::

  この拡張機能では、ノードに編集可能な文字列プロパティを追加します。 また、SharePoint サーバーからの読み取り専用データを表示するカスタム プロパティを作成することもできます。 これを行う方法を示す例については、「[チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.SharePoint.Explorer.Extensions

- System.ComponentModel.Composition

- System.Windows.Forms

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 **サーバー エクスプローラー** の拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: サーバー エクスプローラーにカスタム SharePoint ノードを追加する](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
