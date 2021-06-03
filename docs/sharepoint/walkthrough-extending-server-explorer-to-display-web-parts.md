---
title: 'チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する | Microsoft Docs'
titleSuffix: ''
description: このチュートリアルでは、接続されている各 SharePoint サイトに Web パーツ ギャラリーを表示するようにサーバー エクスプローラーを拡張します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint commands
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 276315b7f470777da30fda33b15bac995deb07fd
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217672"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する
  Visual Studio では、**サーバー エクスプローラー** の **[SharePoint 接続]** ノードを使用して、SharePoint サイトのコンポーネントを表示できます。 ただし、一部のコンポーネントは既定で **サーバー エクスプローラー** に表示されません。 このチュートリアルでは、接続されている各 SharePoint サイトに Web パーツ ギャラリーを表示するように **サーバー エクスプローラー** を拡張します。

 このチュートリアルでは、次のタスクについて説明します。

- 次の方法で **サーバー エクスプローラー** を拡張する Visual Studio 拡張機能を作成する。

  - この拡張機能では、**サーバー エクスプローラー** の各 SharePoint サイト ノードの下に、 **[Web パーツ ギャラリー]** ノードが追加されます。 この新しいノードには、サイトの Web パーツ ギャラリー内の各 Web パーツを表す子ノードが含まれています。

  - この拡張機能では、Web パーツのインスタンスを表す新しい種類のノードを定義します。 この新しいノード タイプは、新しい **[Web パーツ ギャラリー]** ノードの下にある子ノードの基礎となります。 新しい Web パーツ ノード タイプでは、そのタイプが表す Web パーツに関する情報が **[プロパティ]** ウィンドウに表示されます。 ノード タイプには、Web パーツに関連する他のタスクを実行するための開始点として使用できるカスタム ショートカット メニュー項目も含まれています。

- 拡張機能アセンブリで呼び出される 2 つのカスタム SharePoint コマンドを作成する。 SharePoint コマンドは、SharePoint のサーバー オブジェクト モデルで API を使用するために拡張機能アセンブリで呼び出されるメソッドです。 このチュートリアルでは、開発用コンピューターのローカル SharePoint サイトから Web パーツ情報を取得するコマンドを作成します。 詳細については、[SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)に関するページを参照してください。

- 拡張機能を配置するための Visual Studio Extension (VSIX) パッケージを構築する。

- 拡張機能をデバッグしてテストする。

> [!NOTE]
> サーバー オブジェクト モデルではなく、SharePoint 用のクライアント オブジェクト モデルを使用するこのチュートリアルの別バージョンについては、「[チュートリアル: サーバー エクスプローラー拡張機能で SharePoint クライアント オブジェクト モデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、プロジェクト項目を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint のサーバー オブジェクト モデルの使用。 詳細については、「[SharePoint Foundation サーバー側のオブジェクト モデルを使用する](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))」を参照してください。

- SharePoint ソリューションでの Web パーツ。 詳細については、「[Web パーツの概要](/previous-versions/office/ms432401(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、3 つのプロジェクトを作成する必要があります。

- 拡張機能を配置するために VSIX パッケージを作成する VSIX プロジェクト。

- 拡張機能を実装するクラス ライブラリ プロジェクト。 このプロジェクトは .NET Framework 4.5 を対象にする必要があります。

- カスタム SharePoint コマンドを定義するクラス ライブラリ プロジェクト。 このプロジェクトは .NET Framework 3.5 を対象にする必要があります。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** ノードをクリックします。

    > [!NOTE]
    > **[機能拡張]** ノードは、Visual Studio SDK がインストールされている場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択します。

5. **[VSIX プロジェクト]** テンプレートを選択し、プロジェクトに **WebPartNode** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**ソリューション エクスプローラー** に **WebPartNode** プロジェクトが追加されます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードを選択します。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択します。

4. プロジェクト テンプレートの一覧で **[クラス ライブラリ]** を選択し、プロジェクトに **WebPartNodeExtension** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**WebPartNodeExtension** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

#### <a name="to-create-the-sharepoint-commands-project"></a>SharePoint コマンド プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードをクリックします。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 3.5]** を選択します。

4. プロジェクト テンプレートの一覧で **[クラス ライブラリ]** を選択し、プロジェクトに **WebPartCommands** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**WebPartCommands** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-projects"></a>プロジェクトを構成する
 拡張機能を作成するためのコードを記述する前に、コード ファイルおよびアセンブリ参照を追加し、プロジェクト設定を構成する必要があります。

#### <a name="to-configure-the-webpartnodeextension-project"></a>WebPartNodeExtension プロジェクトを構成するには

1. WebPartNodeExtension プロジェクトに、次の名前を持つ 4 つのコード ファイルを追加します。

    - SiteNodeExtension

    - WebPartNodeTypeProvider

    - WebPartNodeInfo

    - WebPartCommandIds

2. **WebPartNodeExtension** プロジェクトのショートカット メニューを開いてから、 **[参照の追加]** を選択します。

3. **[参照マネージャー - WebPartNodeExtension]** ダイアログ ボックスで、 **[フレームワーク]** タブを選択し、次の各アセンブリのチェック ボックスをオンにします。

    - System.ComponentModel.Composition

    - System.Windows.Forms

4. **[拡張機能]** タブを選択し、Microsoft.VisualStudio.SharePoint アセンブリのチェック ボックスをオンにして、 **[OK]** をクリックします。

5. **ソリューション エクスプローラー** で、 **[WebPartNodeExtension]** プロジェクト ノードのショートカット メニューを開き、 **[プロパティ]** を選択します。

     **プロジェクト デザイナー** が開きます。

6. **[アプリケーション]** タブを選択します。

7. **[既定の名前空間]** ボックス (C#) または **[ルート名前空間]** ボックス ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) で、「**ServerExplorer.SharePointConnections.WebPartNode**」と入力します。

#### <a name="to-configure-the-webpartcommands-project"></a>WebPartCommands プロジェクトを構成するには

1. WebPartCommands プロジェクトで、WebPartCommands という名前のコード ファイルを追加します。

2. **ソリューション エクスプローラー** で **[WebPartCommands]** プロジェクト ノードのショートカット メニューを開き、 **[追加]** 、 **[既存の項目]** の順に選択します。

3. **[既存項目の追加]** ダイアログ ボックスで、WebPartNodeExtension プロジェクトのコード ファイルが格納されているフォルダーを参照し、WebPartNodeInfo コード ファイルと WebPartCommandIds コード ファイルを選択します。

4. **[追加]** ボタンの横にある矢印をクリックし、表示されるメニューで **[リンクとして追加]** を選択します。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、WebPartCommands プロジェクトにリンクとしてコード ファイルが追加されます。 その結果、コード ファイルは WebPartNodeExtension プロジェクトに配置されますが、ファイル内のコードも WebPartCommands プロジェクトにコンパイルされます。

5. **WebPartCommands** プロジェクトのショートカット メニューをもう一度開き、 **[参照の追加]** を選択します。

6. **[参照マネージャー - WebPartCommands]** ダイアログ ボックスで、 **[拡張機能]** タブをクリックしてから、次の各アセンブリのチェック ボックスをオンにし、 **[OK]** をクリックします。

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

7. **ソリューション エクスプローラー** で、**WebPartCommands** プロジェクトのショートカット メニューをもう一度開き、 **[プロパティ]** を選択します。

     **プロジェクト デザイナー** が開きます。

8. **[アプリケーション]** タブを選択します。

9. **[既定の名前空間]** ボックス (C#) または **[ルート名前空間]** ボックス ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) で、「**ServerExplorer.SharePointConnections.WebPartNode**」と入力します。

## <a name="create-icons-for-the-new-nodes"></a>新しいノードのアイコンを作成する
 **サーバー エクスプローラー** の拡張機能用に 2 つのアイコンを作成します。新しい **[Web パーツ ギャラリー]** ノード用のアイコンと、 **[Web パーツ ギャラリー]** ノードの下にある各子 Web パーツ ノード用のアイコンです。 このチュートリアルの後半では、これらのアイコンをノードに関連付けるコードを記述します。

#### <a name="to-create-icons-for-the-nodes"></a>ノードのアイコンを作成するには

1. **ソリューション エクスプローラー** で、**WebPartNodeExtension** プロジェクトのショートカット メニューを開き、 **[プロパティ]** を選択します。

2. **プロジェクト デザイナー** が開きます。

3. **[リソース]** タブをクリックし、 **[このプロジェクトには既定のリソース ファイルが含まれていません。ファイルを作成するには、ここをクリックしてください]** リンクをクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でリソース ファイルが作成され、デザイナーで開かれます。

4. デザイナーの上部で、 **[リソースの追加]** メニュー コマンドの横にある矢印をクリックし、表示されたメニューで **[新しいアイコンの追加]** を選択します。

5. **[新しいリソースの追加]** ダイアログ ボックスで、新しいアイコンに **WebPartsNode** という名前を付けて、 **[追加]** をクリックします。

     **イメージ エディター** に新しいアイコンが表示されます。

6. 16x16 バージョンのアイコンを編集して、見た目にわかりやすいデザインにします。

7. 32x32 バージョンのアイコンのショートカット メニューを開き、 **[イメージの種類の削除]** を選択します。

8. 手順 5 ～ 8 を繰り返して、プロジェクト リソースに 2 つ目のアイコンを追加し、そのアイコンに **WebPart** という名前を付けます。

9. **ソリューション エクスプローラー** で、**WebPartNodeExtension** プロジェクトの **[リソース]** フォルダーの下にある **WebPartsNode.ico** のショートカット メニューを開きます。

10. **[プロパティ]** ウィンドウで、 **[ビルド アクション]** の横にある矢印をクリックし、表示されるメニューで **[埋め込みリソース]** を選択します。

11. **WebPart.ico** に対して、最後の 2 つの手順を繰り返します。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>[Web パーツ ギャラリー] ノードをサーバー エクスプローラーに追加する
 新しい **[Web パーツ ギャラリー]** ノードを各 SharePoint サイト ノードに追加するクラスを作成します。 新しいノードを追加するために、このクラスでは <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> インターフェイスを実装します。 ノードに子ノードを追加するなど、**サーバー エクスプローラー** の既存のノードの動作を拡張する場合は、必ずこのインターフェイスを実装します。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>[Web パーツ ギャラリー] ノードをサーバー エクスプローラーに追加するには

1. WebPartNodeExtension プロジェクトで SiteNodeExtension コード ファイルを開き、それに次のコードを貼り付けます。

    > [!NOTE]
    > このコードを追加すると、プロジェクトにコンパイル エラーが発生しますが、後の手順でコードを追加したときに、そのエラーは解消されます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>Web パーツを表すノード タイプを定義する
 Web パーツを表す新しいノード タイプを定義するクラスを作成します。 Visual Studio では、 **[Web パーツ ギャラリー]** ノードの下の子ノードを表示するために、この新しいノード タイプが使用されます。 各子ノードは、SharePoint サイト上の 1 つの Web パーツを表します。

 新しいノード タイプを定義するために、このクラスでは <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> インターフェイスを実装します。 このインターフェイスは、**サーバー エクスプローラー** で新しいノード タイプを定義するたびに必ず実装します。

#### <a name="to-define-the-web-part-node-type"></a>Web パーツ ノード タイプを定義するには

1. WebPartNodeExtension プロジェクトで WebPartNodeTypeProvder コード ファイルを開き、それに次のコードを貼り付けます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::

## <a name="define-the-web-part-data-class"></a>Web パーツのデータ クラスを定義する
 SharePoint サイトの 1 つの Web パーツに関するデータを含むクラスを定義します。 このチュートリアルの後半では、サイトの各 Web パーツに関するデータを取得し、このクラスのインスタンスにデータを割り当てるカスタム SharePoint コマンドを作成します。

#### <a name="to-define-the-web-part-data-class"></a>Web パーツのデータ クラスを定義するには

1. WebPartNodeExtension プロジェクトで WebPartNodeInfo コード ファイルを開き、それに次のコードを貼り付けます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs" id="Snippet3":::

## <a name="define-the-ids-for-the-sharepoint-commands"></a>SharePoint コマンドの ID を定義するには
 カスタム SharePoint コマンドを識別する複数の文字列を定義します。 これらのコマンドは、このチュートリアルの後半で実装します。

#### <a name="to-define-the-command-ids"></a>コマンド ID を定義するには

1. WebPartNodeExtension プロジェクトで WebPartCommandIds コード ファイルを開き、それに次のコードを貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb" id="Snippet4":::

## <a name="create-the-custom-sharepoint-commands"></a>カスタム SharePoint コマンドを作成する
 SharePoint のサーバー オブジェクト モデルを呼び出すカスタム コマンドを作成して、SharePoint サイトの Web パーツに関するデータを取得します。 各コマンドは、<xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> が適用されているメソッドです。

#### <a name="to-define-the-sharepoint-commands"></a>SharePoint コマンドを定義するには

1. WebPartCommands プロジェクトで WebPartCommands コード ファイルを開き、それに次のコードを貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs" id="Snippet6":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb" id="Snippet6":::

## <a name="checkpoint"></a>Checkpoint
 この段階で、 **[Web パーツ ギャラリー]** ノードと SharePoint コマンドに必要なすべてのコードがプロジェクト内に揃ったことになります。 エラーが発生することなく両方のプロジェクトをコンパイルできるかどうか、ソリューションをビルドして確認してください。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

    > [!WARNING]
    > この時点では、WebPartNode プロジェクトのビルド エラーが発生する可能性があります。これは、VSIX マニフェスト ファイルに Author の値がないためです。 このエラーは、後の手順で値を追加したときに解消されます。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>拡張機能を配置するための VSIX パッケージを作成する
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトの source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-the-vsix-package"></a>VSIX パッケージを構成するには

1. **ソリューション エクスプローラー** で、WebPartNode プロジェクトの **source.extension.vsixmanifest** ファイルをマニフェスト エディターで開きます。

     source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. **[製品名]** ボックスに、「**サーバー エクスプローラーの Web パーツ ギャラリー ノード**」と入力します。

3. **[作成者]** ボックスに、「**Contoso**」と入力します。

4. **[説明]** ボックスに「**Adds a custom Web Part Gallery node to the SharePoint Connections node in Server Explorer. This extension uses a custom SharePoint command to call into the server object model**」(サーバー エクスプローラーでカスタム [Web パーツ ギャラリー] ノードを SharePoint 接続ノードに追加します。この拡張機能は、カスタム SharePoint コマンドを使用してサーバー オブジェクト モデルを呼び出します) と入力します。

5. エディターの **[アセット]** タブをクリックして、 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

6. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

8. **[プロジェクト]** ボックスの一覧で **[WebPartNodeExtension]** を選択し、 **[OK]** をクリックします。

9. マニフェスト エディターで、 **[新規作成]** をもう一度クリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

10. **[種類]** ボックスに「**SharePoint.Commands.v4**」と入力します。

    > [!NOTE]
    > この要素により、Visual Studio 拡張機能に含めるカスタム拡張機能が指定されます。 詳細については、[Asset 要素 (VSX スキーマ)](/previous-versions/dd393737(v=vs.110)) に関するページを参照してください。

11. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** リスト項目を選択します。

12. **[プロジェクト]** ボックスの一覧で、 **[WebPartCommands]** を選択し、 **[OK]** をクリックします。

13. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順に選択し、ソリューションがエラーなしでコンパイルされることを確認します。

14. WebPartNode プロジェクトのビルド出力フォルダーに、WebPartNode.vsix ファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-extension"></a>拡張機能をテストする
 これで、**サーバー エクスプローラー** の新しい **[Web パーツ ギャラリー]** ノードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで拡張機能のデバッグを開始します。 次に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスで、新しい **[Web パーツ]** ノードを使用します。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 管理者の資格情報で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を再起動し、WebPartNode ソリューションを開きます。

2. WebPartNodeExtension プロジェクトで、SiteNodeExtension コード ファイルを開き、`NodeChildrenRequested` メソッドと `CreateWebPartNodes` メソッド内の最初のコード行にブレークポイントを追加します。

3. **F5** キーを押してデバッグを開始します。

     Visual Studio で、%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part Gallery Node Extension for Server Explorer\1.0 に拡張機能がインストールされ、Visual Studio の実験用インスタンスが起動します。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-extension"></a>拡張機能をテストするには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスのメニュー バーで、 **[表示]**  >  **[サーバー エクスプローラー]** の順に選択します。

2. テストに使用する SharePoint サイトが **サーバー エクスプローラー** の **[SharePoint 接続]** ノードに表示されない場合は、次の手順を実行します。

    1. **サーバー エクスプローラー** で、 **[SharePoint 接続]** のショートカット メニューを開き、 **[接続の追加]** を選択します。

    2. **[SharePoint 接続の追加]** ダイアログ ボックスで、接続先の SharePoint サイトの URL を入力し、 **[OK]** をクリックします。

         開発用コンピューター上の SharePoint サイトを指定するには、「 **http://localhost** 」と入力します。

3. サイト接続ノード (サイトの URL が表示されます) を展開し、子サイト ノード (たとえば、 **[Team Site]** ) を展開します。

4. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のもう一方のインスタンスのコードが、先ほど `NodeChildrenRequested` メソッドに設定したブレークポイントで停止していることを確認し、**F5** キーを押して、プロジェクトのデバッグを続行します。

5. Visual Studio の実験用インスタンスで、 **[Web パーツ ギャラリー]** という名前の新しいノードが最上位サイト ノードの下に表示されていることを確認し、 **[Web パーツ ギャラリー]** ノードを展開します。

6. Visual Studio のもう一方のインスタンスのコードが、先ほど `CreateWebPartNodes` メソッドに設定したブレークポイントで停止していることを確認し、**F5** キーを押して、プロジェクトのデバッグを続行します。

7. Visual Studio の実験用インスタンスで、接続されたサイトのすべての Web パーツが、**サーバー エクスプローラー** の **[Web パーツ ギャラリー]** ノードの下に表示されていることを確認します。

8. **サーバー エクスプローラー** で、いずれかの Web パーツのショートカット メニューを開き、 **[プロパティ]** を選択します。

9. デバッグしている [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のインスタンスで、Web パーツの詳細が **[プロパティ]** ウィンドウに表示されていることを確認します。

## <a name="uninstall-the-extension-from-visual-studio"></a>拡張機能を Visual Studio からアンインストールする
 拡張機能のテストが完了したら、Visual Studio から拡張機能をアンインストールします。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** を選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、 **[サーバー エクスプローラーの [Web パーツ ギャラリー] ノードの拡張機能]** を選択し、 **[アンインストール]** をクリックします。

3. 表示されるダイアログ ボックスで、 **[はい]** をクリックして拡張機能のアンインストールを確定し、 **[今すぐ再起動]** をクリックしてアンインストールを完了します。

4. Visual Studio の両方のインスタンス (実験用インスタンスと、WebPartNode ソリューションが開かれたインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [チュートリアル: サーバー エクスプローラー拡張機能で SharePoint クライアント オブジェクト モデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)
- [アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)
- [アイコンまたはその他のイメージの作成 &#40;アイコン用イメージ エディター&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)