---
title: サーバー エクスプローラー： [SharePoint 接続] ノードの拡張
titleSuffix: ''
description: このチュートリアルでは、サーバー エクスプローラーの [SharePoint 接続] ノードの拡張機能から、SharePoint クライアント オブジェクト モデルを呼び出す方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint commands [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dee53642e042c8d4db88bdba7c093f327527798d
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217022"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>チュートリアル: サーバー エクスプローラーの拡張機能から SharePoint クライアント オブジェクト モデルを呼び出す
  このチュートリアルでは、**サーバー エクスプローラー** の **[SharePoint 接続]** ノードの拡張機能から、SharePoint クライアント オブジェクト モデルを呼び出す方法について説明します。 SharePoint クライアント オブジェクト モデルの使用方法について詳しくは、「[SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

 このチュートリアルでは、次のタスクについて説明します。

- 次の方法で、**サーバー エクスプローラー** の **[SharePoint 接続]** ノードを拡張する [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能を作成する。

  - この拡張機能では、**サーバー エクスプローラー** の各 SharePoint サイト ノードの下に、 **[Web Part Gallery]** ノードが追加されます。 この新しいノードには、サイトの Web パーツ ギャラリー内の各 Web パーツを表す子ノードが含まれています。

  - この拡張機能では、Web パーツのインスタンスを表す新しい種類のノードを定義します。 この新しいノード タイプは、新しい **[Web Part Gallery]** ノードの下にある子ノードの基礎となります。 新しい Web パーツ ノード タイプでは、ノードが表す Web パーツに関する情報が **[プロパティ]** ウィンドウに表示されます。

- 拡張機能を配置するための Visual Studio Extension (VSIX) パッケージを構築する。

- 拡張機能をデバッグしてテストする。

> [!NOTE]
> このチュートリアルで作成する拡張機能は、「[チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」で作成する拡張機能と似ています。 このチュートリアルでは SharePoint サーバー オブジェクト モデルを使っていますが、本チュートリアルでは、クライアント オブジェクト モデルを使って同じタスクを行います。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、拡張機能を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint クライアント オブジェクト モデルの使用。 詳細については、「[マネージ クライアント オブジェクト モデル](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14))」を参照してください。

- SharePoint の Web パーツ。 詳細については、「[Web パーツの概要](/previous-versions/office/ms432401(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、2 つのプロジェクトを作成する必要があります。

- **サーバー エクスプローラー** の拡張機能を配置するための VSIX パッケージを作成する VSIX プロジェクト。

- **サーバー エクスプローラー** の拡張機能を実装するクラス ライブラリ プロジェクト。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** を選択します。

    > [!NOTE]
    > **[機能拡張]** ノードは、Visual Studio SDK がインストールされている場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択します。

     SharePoint ツールの拡張機能を使用するには、このバージョンの .NET Framework の機能が必要です。

5. **[VSIX プロジェクト]** テンプレートを選択します。

6. **[名前]** ボックスに「**WebPartNode**」と入力して、 **[OK]** を選択します。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**ソリューション エクスプローラー** に **WebPartNode** プロジェクトが追加されます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** を選択します。

3. ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 4.5]** を選択します。

4. プロジェクト テンプレートの一覧で **[クラス ライブラリ]** を選択します。

5. **[名前]** ボックスに「**WebPartNodeExtension**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**WebPartNodeExtension** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

6. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-extension-project"></a>拡張機能プロジェクトを構成する
 拡張機能を作成するためのコードを記述する前に、コード ファイルとアセンブリ参照をプロジェクトに追加する必要があります。また、既定の名前空間を更新する必要があります。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. **WebPartNodeExtension** プロジェクトで、SiteNodeExtension および WebPartNodeTypeProvider という 2 つのコード ファイルを追加します。

2. WebPartNodeExtension プロジェクトのショートカット メニューを開いてから、 **[参照の追加]** を選択します。

3. **[参照マネージャー - WebPartNodeExtension]** ダイアログ ボックスで、 **[フレームワーク]** ノードを選択し、System.ComponentModel.Composition アセンブリと System.Windows.Forms アセンブリのチェック ボックスをオンにします。

4. **[拡張機能]** ノードを選択し、次の各アセンブリのチェック ボックスをオンにして、 **[OK]** をクリックします。

    - Microsoft.SharePoint.Client

    - Microsoft.SharePoint.Client.Runtime

    - Microsoft.VisualStudio.SharePoint

5. **WebPartNodeExtension** プロジェクトのショートカット メニューを開いてから、 **[プロパティ]** を選択します。

     **プロジェクト デザイナー** が開きます。

6. **[アプリケーション]** タブを選択します。

7. **[既定の名前空間]** ボックス (C#) または **[ルート名前空間]** ボックス (Visual Basic) で、「**ServerExplorer.SharePointConnections.WebPartNode**」と入力します。

## <a name="create-icons-for-the-new-nodes"></a>新しいノードのアイコンを作成する
 **サーバー エクスプローラー** の拡張機能用に 2 つのアイコンを作成します。新しい **[Web Part Gallery]** ノード用のアイコンと、 **[Web Part Gallery]** ノードの下にある各子 Web パーツ ノード用のアイコンです。 このチュートリアルの後半では、これらのアイコンをノードに関連付けるコードを記述します。

#### <a name="to-create-icons-for-the-nodes"></a>ノードのアイコンを作成するには

1. WebPartNodeExtension プロジェクトの **プロジェクト デザイナー** で、 **[リソース]** タブを選択します。

2. 「**このプロジェクトには既定のリソース ファイルが含まれていません。ファイルを作成するには、ここをクリックしてください。** 」というリンクを選択します。

     Visual Studio でリソース ファイルが作成され、デザイナーで開かれます。

3. デザイナーの上部で、 **[リソースの追加]** メニュー コマンドの矢印をクリックし、 **[新しいアイコンの追加]** を選択します。

4. 新しいアイコン名として「**WebPartsNode**」と入力し、 **[追加]** をクリックします。

     **イメージ エディター** に新しいアイコンが表示されます。

5. 16x16 バージョンのアイコンを編集して、見た目にわかりやすいデザインにします。

6. 32x32 バージョンのアイコンのショートカット メニューを開き、 **[イメージの種類の削除]** を選択します。

7. 手順 3 ～ 7 を繰り返して、プロジェクト リソースに 2 つ目のアイコンを追加し、そのアイコンに **WebPart** という名前を指定します。

8. **ソリューション エクスプローラー** で、**WebPartNodeExtension** プロジェクトの **Resources** フォルダーにある、*WebPartsNode.ico* を選択します。

9. **[プロパティ]** ウィンドウで、 **[ビルド アクション]** ボックスの一覧を開き、 **[埋め込みリソース]** を選択します。

10. *WebPart.ico* に対して、最後の 2 つの手順を繰り返します。

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Web パーツ ギャラリー ノードをサーバー エクスプローラーに追加する
 新しい **[Web Part Gallery]** ノードを各 SharePoint サイト ノードに追加するクラスを作成します。 新しいノードを追加するために、このクラスでは <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> インターフェイスを実装します。 ノードに新しい子ノードを追加するなど、**サーバー エクスプローラー** の既存のノードの動作を拡張する場合は、必ずこのインターフェイスを実装します。

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Web パーツ ギャラリー ノードをサーバー エクスプローラーに追加するには

1. 次のコードを、**WebPartNodeExtension** プロジェクトの **SiteNodeExtension** コード ファイル内に貼り付けます。

    > [!NOTE]
    > このコードを追加した直後は、いくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb" id="Snippet1":::

## <a name="define-a-node-type-that-represents-a-web-part"></a>Web パーツを表すノード タイプを定義する
 Web パーツを表す新しいノード タイプを定義するクラスを作成します。 Visual Studio では、 **[Web Part Gallery]** ノードの下の子ノードを表示するために、この新しいノード タイプが使用されます。 これらの各子ノードは、SharePoint サイト上の 1 つの Web パーツを表します。

 新しいノード タイプを定義するために、このクラスでは <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> インターフェイスを実装します。 このインターフェイスは、**サーバー エクスプローラー** で新しいノード タイプを定義するたびに必ず実装します。

#### <a name="to-define-the-web-part-node-type"></a>Web パーツ ノード タイプを定義するには

1. 次のコードを、**WebPartNodeExtension** プロジェクトの **WebPartNodeTypeProvider** コード ファイル内に貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb" id="Snippet2":::

## <a name="checkpoint"></a>Checkpoint
 この段階で、 **[Web Part Gallery]** ノードに必要なすべてのコードがプロジェクト内に揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、**WebPartNodeExtension** プロジェクトをビルドして確認してください。

#### <a name="to-build-the-project"></a>プロジェクトをビルドするには

1. **ソリューション エクスプローラー** で、**WebPartNodeExtension** プロジェクトのショートカット メニューを開き、 **[ビルド]** を選択します。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>拡張機能を配置するための VSIX パッケージを作成する
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-the-vsix-package"></a>VSIX パッケージを構成するには

1. **ソリューション エクスプローラー** で、**WebPartNode** プロジェクトの **source.extension.vsixmanifest** ファイルをマニフェスト エディターで開きます。

     source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. **[製品名]** ボックスに、「**サーバー エクスプローラーの Web パーツ ギャラリー ノード**」と入力します。

3. **[作成者]** ボックスに、「**Contoso**」と入力します。

4. **[説明]** ボックスに「**サーバー エクスプローラーの [SharePoint 接続] ノードに、カスタムの [Web Part Gallery] ノードを追加します**」と入力します。

5. エディターの **[アセット]** タブで、 **[新規作成]** をクリックします。

6. **[新しいアセットを追加する]** ダイアログ ボックスの **[種類]** ボックスの一覧で、**Microsoft.VisualStudio.MefComponent** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. **[ソース]** ボックスの一覧で、 **[A project in current solution]\(現在のソリューション内のプロジェクト\)** を選択します。

8. **[プロジェクト]** ボックスの一覧で **[WebPartNodeExtension]** を選択し、 **[OK]** をクリックします。

9. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** を選択し、ソリューションがエラーなしでコンパイルされることを確認します。

10. WebPartNode プロジェクトのビルド出力フォルダーに、WebPartNode.vsix ファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-extension"></a>拡張機能をテストする
 これで、**サーバー エクスプローラー** の新しい **[Web Part Gallery]** ノードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで、拡張機能プロジェクトのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで、新しい **[Web Parts]** ノードを使用します。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、**WebPartNode** ソリューションを開きます。

2. WebPartNodeExtension プロジェクトで、**SiteNodeExtension** コード ファイルを開き、`NodeChildrenRequested` メソッドと `CreateWebPartNodes` メソッド内の最初のコード行にブレークポイントを追加します。

3. **F5** キーを押してデバッグを開始します。

     Visual Studio で、%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part Gallery Node Extension for Server Explorer\1.0 に拡張機能がインストールされ、Visual Studio の実験用インスタンスが起動します。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-extension"></a>拡張機能をテストするには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[表示]**  >  **[サーバー エクスプローラー]** を選択します。

2. テストに使用する SharePoint サイトが、**サーバー エクスプローラー** の **[SharePoint 接続]** ノードの下に表示されていることを確認します。 一覧に表示されていない場合は、次の手順を実行します。

    1. **[SharePoint 接続]** のショートカット メニューを開き、 **[接続の追加]** を選択します。

    2. **[SharePoint 接続の追加]** ダイアログ ボックスで、接続先の SharePoint サイトの URL を入力し、 **[OK]** をクリックします。

         開発用コンピューター上の SharePoint サイトを指定するには、「 **http://localhost** 」と入力します。

3. サイト接続ノード (サイトの URL が表示されます) を展開し、子サイト ノード (たとえば、 **[Team Site]** ) を展開します。

4. Visual Studio のもう一方のインスタンスのコードが、先ほど `NodeChildrenRequested` メソッドに設定したブレークポイントで停止していることを確認し、**F5** キーを押して、プロジェクトのデバッグを続行します。

5. Visual Studio の実験用インスタンスで、最上位のサイト ノードの下に表示される **[Web Part Gallery]** ノードを展開します。

6. Visual Studio のもう一方のインスタンスのコードが、先ほど `CreateWebPartNodes` メソッドに設定したブレークポイントで停止していることを確認し、**F5** キーを押して、プロジェクトのデバッグを続行します。

7. Visual Studio の実験用インスタンスで、接続されたサイトのすべての Web パーツが、**サーバー エクスプローラー** の **[Web Part Gallery]** ノードの下に表示されていることを確認します。

8. Web パーツのショートカット メニューを開き、 **[プロパティ]** を選択します。

9. **[プロパティ]** ウィンドウで、Web パーツの詳細が表示されていることを確認します。

10. **サーバー エクスプローラー** で、同じ Web パーツのショートカット メニューを開き、 **[Display Message]\(メッセージの表示\)** を選択します。

     表示されるメッセージ ボックスで、 **[OK]** をクリックします。

## <a name="uninstall-the-extension-from-visual-studio"></a>拡張機能を Visual Studio からアンインストールする
 拡張機能のテストが完了したら、Visual Studio からアンインストールします。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** を選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、 **[サーバー エクスプローラーの Web パーツ ギャラリー ノード]** を選択し、 **[アンインストール]** をクリックします。

3. 表示されるダイアログ ボックスで、 **[はい]** を選択します。

4. **[今すぐ再起動]** をクリックして、アンインストールを完了します。

     プロジェクト項目もアンインストールされます。

5. Visual Studio の両方のインスタンス (実験用インスタンスと、WebPartNode ソリューションが開かれたインスタンス) を閉じます。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [チュートリアル: サーバー エクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)
- [アイコンまたはその他のイメージの作成 &#40;アイコン用イメージ エディター&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)