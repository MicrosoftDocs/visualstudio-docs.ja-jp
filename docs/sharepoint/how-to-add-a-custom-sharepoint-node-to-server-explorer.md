---
title: '方法: サーバー エクスプローラーにカスタム SharePoint ノードを追加する | Microsoft Docs'
titleSuffix: ''
description: Visual Studio のサーバー エクスプローラーにカスタム SharePoint ノードを追加します。 既定ではサーバー エクスプローラーに表示されない追加の SharePoint コンポーネントを表示します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e7c0a13879850bbd31112ddcb3193d027abeb5d1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216359"
---
# <a name="how-to-add-a-custom-sharepoint-node-to-server-explorer"></a>方法: サーバー エクスプローラーにカスタム SharePoint ノードを追加する
  **サーバー エクスプローラー** の **[SharePoint 接続]** ノードの下にカスタム ノードを追加できます。 これは、既定では **サーバー エクスプローラー** に表示されない追加の SharePoint コンポーネントを表示したい場合に役立ちます。 詳細については、「[サーバー エクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

 カスタム ノードを追加するには、まず、新しいノードを定義するクラスを作成します。 その後、既存のノードの子としてノードを追加する拡張機能を作成します。

### <a name="to-define-the-new-node"></a>新しいノードを定義するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.SharePoint.Explorer.Extensions

    - System.ComponentModel.Composition

    - System.Drawing

3. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> インターフェイスを実装するクラスを作成します。

4. このクラスに次の属性を追加します。

    - <xref:System.ComponentModel.Composition.ExportAttribute>. この属性を使用すると、Visual Studio で <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 実装を検出して読み込むことができます。 属性コンストラクターに <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> 型を渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute>. ノード定義では、この属性で、新しいノードの文字列識別子を指定します。 すべてのノードに一意識別子が確実に割り当てられるようにするために、<*会社名*>.<*ノード名*> という形式を使用することをお勧めします。

5. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider.InitializeType%2A> メソッドの実装で、*typeDefinition* パラメーターのメンバーを使用して新しいノードの動作を構成します。 このパラメーターは、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents> インターフェイスで定義されているイベントへのアクセスを提供する <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition> オブジェクトです。

     次のコード例は、新しいノードを定義する方法を示しています。 この例では、プロジェクトに CustomChildNodeIcon という名前のアイコンが埋め込みリソースとして含まれていることを前提にしています。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet6":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet6":::

### <a name="to-add-the-new-node-as-a-child-of-an-existing-node"></a>新しいノードを既存のノードの子として追加するには

1. ノード定義と同じプロジェクトで、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> インターフェイスを実装するクラスを作成します。

2. クラスに <xref:System.ComponentModel.Composition.ExportAttribute> 属性を追加します。 この属性を使用すると、Visual Studio で <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 実装を検出して読み込むことができます。 属性コンストラクターに <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> 型を渡します。

3. クラスに <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypeAttribute> 属性を追加します。 ノード拡張機能では、この属性で、拡張するノードの種類の文字列識別子を指定します。

     Visual Studio によって提供される組み込みのノードの種類を指定するには、属性コンストラクターに次のいずれかの列挙値を渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeTypes>: これらの値は、**サーバー エクスプローラー** のサイト接続ノード (サイト URL を表示するノード)、サイト ノード、またはその他のすべての親ノードを指定するために使用します。

    - <xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.ExtensionNodeTypes>: これらの値は、SharePoint サイト上の個々のコンポーネントを表す組み込みノード (リスト、フィールド、またはコンテンツ タイプを表すノードなど) のいずれかを指定するために使用します。

4. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension.Initialize%2A> メソッドの実装で、<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType> パラメーターの <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> イベントを処理します。

5. <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeEvents.NodeChildrenRequested> イベント ハンドラーで、イベント引数パラメーターによって公開される <xref:Microsoft.VisualStudio.SharePoint.Explorer.ExplorerNodeEventArgs.Node%2A> オブジェクトの子ノードのコレクションに新しいノードを追加します。

     次のコード例は、**サーバー エクスプローラー** の SharePoint サイト ノードの子として新しいノードを追加する方法を示しています。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet7":::

## <a name="complete-example"></a>コード例全体
 次のコード例は、単純なノードを定義し、それを **サーバー エクスプローラー** の SharePoint サイト ノードの子として追加するための完全なコードを提供します。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorernode.vb" id="Snippet5":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorernode.cs" id="Snippet5":::

## <a name="compiling-the-code"></a>コードのコンパイル
 この例では、プロジェクトに CustomChildNodeIcon という名前のアイコンが埋め込みリソースとして含まれていることを前提にしています。 また、この例には、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

- System.Drawing

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 **サーバー エクスプローラー** の拡張機能を配置するには、その拡張機能で配布するアセンブリとその他のすべてのファイル用の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [方法: サーバー エクスプローラーの SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
