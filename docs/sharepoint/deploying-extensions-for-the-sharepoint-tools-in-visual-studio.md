---
title: Visual Studio での SharePoint ツールの拡張機能の配置 | Microsoft Docs
description: Visual Studio で SharePoint ツールの拡張機能を配置します。 Visual Studio 拡張機能 (VSIX) プロジェクトを使用して VSIX パッケージを作成します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying extensions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6a899bcc132b9229c1046dee5793278f79ea9e5d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948896"
---
# <a name="deploy-extensions-for-the-sharepoint-tools-in-visual-studio"></a>Visual Studio での SharePoint ツールの拡張機能の配置

SharePoint ツールの拡張機能を配置するには、拡張アセンブリと拡張機能と共に配布するその他のファイルを含む [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能 (VSIX) パッケージを作成します。 VSIX パッケージは、Open パッケージング規約 (OPC) 標準に従った圧縮ファイルです。 VSIX パッケージには、 *.vsix* という拡張子が付きます。

VSIX パッケージが作成されると、他のユーザーがその .vsix ファイルを実行して拡張機能をインストールできます。 ユーザーが拡張機能をインストールすると、すべてのファイルが %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions フォルダーにインストールされます。 拡張機能を配置するために、VSIX パッケージを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトにアップロードできます。または、ネットワーク共有や他の Web サイトでパッケージをホストするなどの方法で顧客にパッケージを配布できます。

VSIX パッケージの作成と [Visual Studio Marketplace](https://marketplace.visualstudio.com/) への配置の詳細については、「[Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 VSIX パッケージは、Visual Studio で **VSIX プロジェクト** テンプレートを使用するか、手動で作成できます。

## <a name="use-vsix-projects-to-create-vsix-packages"></a>VSIX プロジェクトを使用して VSIX パッケージを作成する

Visual Studio SDK に用意されている **VSIX プロジェクト** テンプレートを使用して、SharePoint ツールの拡張機能用の VSIX パッケージを作成できます。 VSIX プロジェクトを使用すると、手動で VSIX パッケージを作成するよりも多くのメリットが得られます。

- プロジェクトをビルドすると、Visual Studio によって VSIX パッケージが自動的に生成されます。 パッケージへの配置ファイルの追加や、パッケージの [Content_Types].xml ファイルの作成などのタスクが自動的に実行されます。

- 拡張機能プロジェクトのビルド出力とプロジェクト テンプレートや項目テンプレートなどの他のファイルを VSIX パッケージに含めるように VSIX プロジェクトを構成できます。

VSIX プロジェクトの使用方法の詳細については、「[VSIX プロジェクト テンプレート](../extensibility/vsix-project-template.md)」を参照してください。

### <a name="organize-your-projects"></a>プロジェクトを整理する

既定では、VSIX プロジェクトでは、アセンブリではなく VSIX パッケージのみが生成されます。 そのため、通常は、VSIX プロジェクトに SharePoint ツールの拡張機能を実装しません。 通常は、少なくとも 2 つのプロジェクトを使用します。

- VSIX プロジェクト。

- 拡張機能を実装するクラス ライブラリ プロジェクト。

特定の種類の拡張機能の追加プロジェクトを使用することもできます。

- 拡張機能によって使用される任意の SharePoint コマンドを実装するクラス ライブラリ プロジェクト。 このシナリオを示すチュートリアルについては、「[チュートリアル: Web パーツを表示するようにサーバー エクスプローラーを拡張する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

- 項目テンプレートまたはプロジェクト テンプレートを作成する項目テンプレートまたはプロジェクト テンプレート プロジェクト (拡張機能で新しい種類の SharePoint プロジェクト項目を定義する場合)。 このシナリオを示すチュートリアルについては、「[チュートリアル: 項目テンプレートを使用してカスタム アクション プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」を参照してください。

- 項目テンプレートまたはプロジェクト テンプレート用のカスタム ウィザードを実装するクラス ライブラリ プロジェクト (拡張機能にテンプレートが含まれる場合)。 このシナリオを示すチュートリアルについては、「[チュートリアル: 項目テンプレートを使用してカスタム アクションプロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)」を参照してください。

すべてのプロジェクトを同じ Visual Studio ソリューションに含める場合は、クラス ライブラリ プロジェクトのビルド出力が含まれるように VSIX プロジェクトの source.extension.vsixmanifest ファイルを変更できます。

### <a name="edit-the-vsix-manifest"></a>VSIX マニフェストを編集する

VSIX プロジェクトの source.extension.vsixmanifest ファイルを、拡張機能に含めるすべての項目のエントリを含むように編集する必要があります。 ショートカット メニューから source.extension.vsixmanifest ファイルを開くと、ファイル内の XML を編集するための UI を示すファイルがデザイナーに表示されます。 詳細については、「[VSIX マニフェスト デザイナー](../extensibility/vsix-manifest-designer.md)」を参照してください。

次の項目について、source.extension.vsixmanifest ファイルにエントリを追加する必要があります。

- 拡張アセンブリ。

- 拡張機能によって使用される任意の SharePoint コマンドを実装するアセンブリ。

- 拡張機能に関連付けられているプロジェクト テンプレートまたは項目テンプレート。

- 拡張機能に関連付けられているテンプレートのカスタム ウィザード。

次の手順では、.vsixmanifest ファイルのこれらの各項目にエントリを追加する方法について説明します。

#### <a name="to-include-the-extension-assembly"></a>拡張アセンブリを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** を選択します。

     デザイナーでファイルが開きます。

2. エディターの **[アセット]** タブで、 **[新規]** ボタンを選択します。

     **[Add New Asset]\(新しいアセットの追加\)** ダイアログ ボックスが開きます。

3. **[種類]** の一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

4. **[ソース]** の一覧で、次のいずれかの操作を実行します。

    - 拡張アセンブリが VSIX プロジェクトと同じソリューション内のプロジェクトからビルドされる場合は、 **[現在のソリューション内のプロジェクト]** を選択します。 **[プロジェクト]** の一覧で、プロジェクトの名前を選択します。

    - 拡張アセンブリがファイルとしてプロジェクトに含まれる場合は、 **[ファイルシステム上のファイル]** を選択します。 **[パス]** の一覧で、拡張アセンブリ ファイルの完全なパスを入力するか、 **[参照]** ボタンを使用してアセンブリ ファイルを探して選択します。

5. **[OK]** を選択します。

#### <a name="to-include-a-sharepoint-command-assembly"></a>SharePoint コマンド アセンブリを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** ボタンを選択します。

     デザイナーでファイルが開きます。

2. エディターの **[アセット]** セクションで、 **[新規]** ボタンを選択します。

     **[Add New Asset]\(新しいアセットの追加\)** ダイアログ ボックスが開きます。

3. **[種類]** ボックスに「**SharePoint.Commands.v4**」と入力します。

4. **[ソース]** の一覧で、次のいずれかの操作を実行します。

    - コマンド アセンブリが VSIX プロジェクトと同じソリューション内のプロジェクトからビルドされる場合は、 **[現在のソリューション内のプロジェクト]** を選択します。 **[プロジェクト]** の一覧で、プロジェクトの名前を選択します。

    - コマンド アセンブリがファイルとしてプロジェクトに含まれる場合は、 **[ファイルシステム上のファイル]** を選択します。 **[パス]** の一覧で、拡張アセンブリ ファイルの完全なパスを入力するか、 **[参照]** ボタンを使用してアセンブリ ファイルを探して選択します。

5. **[OK]** を選択します。

#### <a name="to-include-a-template-that-you-create"></a>作成するテンプレートを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** ボタンを選択します。

     デザイナーでファイルが開きます。

2. エディターの **[アセット]** セクションで、 **[新規]** ボタンを選択します。

     **[Add New Asset]\(新しいアセットの追加\)** ダイアログ ボックスが開きます。

3. **[種類]** の一覧で、 **[Microsoft.VisualStudio.ProjectTemplate]** または **[Microsoft.VisualStudio.ItemTemplate]** を選択します。

4. **[ソース]** の一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

5. **[プロジェクト]** の一覧で、プロジェクトの名前を選択し、 **[OK]** をクリックします。

6. **ソリューション エクスプローラー** で、プロジェクト テンプレートまたは項目テンプレート プロジェクトのショートカット メニューを開き、 **[プロジェクトのアンロード]** をクリックします。

7. プロジェクト ノードのショートカット メニューをもう一度開き、 **[** _YourTemplateProjectName_ **.csproj の編集]** または **[** _YourTemplateProjectName_ **.vbproj の編集]** を選択します。

8. プロジェクト ファイルで次の `VSTemplate` 要素を見つけます。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
    ```

9. この要素を次の XML に置き換えます。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath` 要素は、プロジェクトをビルドするとプロジェクト テンプレートが作成されるパス内の追加フォルダーを指定します。 顧客が **[新しいプロジェクトの追加]** ダイアログ ボックスを開き、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択したときのみ、ここで指定したフォルダー内の項目テンプレートが使用可能になります。

10. ファイルを保存して閉じます。

11. **ソリューション エクスプローラー** で、プロジェクト テンプレートまたは項目テンプレート プロジェクトのショートカット メニューを開き、 **[プロジェクトの再ロード]** を選択します。

#### <a name="to-include-a-template-that-you-create-manually"></a>手動で作成するテンプレートを含めるには

1. VSIX プロジェクトで、テンプレートを格納する新しいフォルダーをプロジェクトに追加します。

2. この新しいフォルダーの下に次のサブフォルダーを作成し、テンプレート (.zip) ファイルを "*ロケール ID*" フォルダーに追加します。

     *YourTemplateFolder*

     **SharePoint**

     **SharePoint14**

     *ロケール ID*

     *YourTemplateName*.zip

     たとえば、英語 (米国) ロケールをサポートする ContosoCustomAction.zip という名前の項目テンプレートがある場合、完全なパスは *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip* のようになります。

3. **ソリューション エクスプローラー** で、テンプレート ファイル (*YourTemplateName*.zip) を選択します。

4. **[プロパティ]** ウィンドウで、 **[ビルド アクション]** プロパティを **[コンテンツ]** に設定します。

5. source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** を選択します。

     デザイナーでファイルが開きます。

6. エディターの **[アセット]** セクションで、 **[新規]** ボタンを選択します。

     **[Add New Asset]\(新しいアセットの追加\)** ダイアログ ボックスが開きます。

7. **[種類]** の一覧で、 **[Microsoft.VisualStudio.ItemTemplate]** または **[Microsoft.VisualStudio.ProjectTemplate]** を選択します。

8. **[ソース]** の一覧で、 **[ファイルシステム上のファイル]** を選択します。

9. **[パス]** フィールドに、アセンブリの完全なパス (たとえば *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*) を入力するか、 **[参照]** ボタンを使用してアセンブリを探して選択し、 **[OK]** ボタンをクリックします。

#### <a name="to-include-a-wizard-for-a-project-template-or-item-template"></a>プロジェクト テンプレートまたは項目テンプレート用のウィザードを含めるには

1. VSIX プロジェクトで、source.extension.vsixmanifest ファイルのショートカット メニューを開き、 **[開く]** を選択します。

     デザイナーでファイルが開きます。

2. エディターの **[アセット]** セクションで、 **[新規]** ボタンを選択します。

     **[Add New Asset]\(新しいアセットの追加\)** ダイアログ ボックスが開きます。

3. **[種類]** の一覧で、 **[Microsoft.VisualStudio.Assembly]** を選択します。

4. **[ソース]** の一覧で、次のいずれかの操作を実行します。

    - ウィザード アセンブリが VSIX プロジェクトと同じソリューション内のプロジェクトからビルドされる場合は、 **[現在のソリューション内のプロジェクト]** を選択します。 **[プロジェクト]** の一覧で、プロジェクトの名前を選択します。

    - ウィザード アセンブリがファイルとしてプロジェクトに含まれる場合は、 **[ファイルシステム上のファイル]** を選択します。 **[パス]** フィールドに、アセンブリ ファイルの完全なパスを入力するか、 **[参照]** ボタンを使用してアセンブリを探して選択します。

5. **[OK]** を選択します。

### <a name="related-walkthroughs"></a>関連するチュートリアル

次の表に、VSIX プロジェクトを使用してさまざまな種類の SharePoint ツールの拡張機能を配置する方法を示すチュートリアルを示します。

|拡張機能の種類|関連するチュートリアル|
|--------------------|--------------------------|
|拡張アセンブリのみを含む拡張機能|[チュートリアル: SharePoint プロジェクト項目の種類を拡張する](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)<br /><br /> [チュートリアル: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)<br /><br /> [チュートリアル: サーバー エクスプローラー拡張機能で SharePoint クライアント オブジェクト モデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)|
|SharePoint コマンドを含む拡張機能|[チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成する](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)<br /><br /> [チュートリアル: Web パーツを表示するようにサーバー エクスプローラーを拡張する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)<br /><br /> [チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|
|Visual Studio テンプレートを含む拡張機能|[チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)<br /><br /> [チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)|
|テンプレート ウィザードを含む拡張機能|[チュートリアル: 項目テンプレートを使ってカスタム アクション プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)<br /><br /> [チュートリアル: プロジェクト テンプレートを使ってサイト列プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|

## <a name="create-vsix-packages-manually"></a>VSIX パッケージを手動で作成する

SharePoint ツールの拡張機能の VSIX パッケージを手動で作成する場合は、次の手順を実行します。

1. 新しいフォルダー内に extension.vsixmanifest ファイルと [Content_Types].xml ファイルを作成します。 詳細については、「[VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)」を参照してください。

2. エクスプローラーで、2 つの XML ファイルが含まれるフォルダーを右クリックし、[送る]、[圧縮 (zip 形式) フォルダー] の順にクリックします。 結果として得られる .zip ファイルの名前を Filename.vsix に変更します。ここで Filename には、パッケージをインストールする再頒布可能なファイルの名前を指定します。

3. 拡張アセンブリを VSIX パッケージに追加します。 拡張機能に SharePoint コマンドが含まれる場合は、SharePoint コマンドを実装するアセンブリも VSIX パッケージに追加します。

4. extension.vsixmanifest ファイルを変更します。

    - `Assets` 要素の下に `Microsoft.VisualStudio.MefComponent` 要素を追加し、新しい要素の値を、VSIX パッケージ内の拡張機能を実装するアセンブリの相対パスに設定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

    - 拡張機能に SharePoint のサーバー オブジェクト モデルを呼び出す SharePoint コマンドが含まれる場合は、`Assets` 要素の下に `Microsoft.VisualStudio.Assembly` 要素を追加します。 新しい要素の値を、VSIX パッケージ内の SharePoint コマンドを実装するアセンブリの相対パスに設定します。 詳細については、「[Asset 要素 (VSX スキーマ)](/previous-versions/dd393737(v=vs.110))」を参照してください。

    - 拡張機能にプロジェクト テンプレートまたは項目テンプレートが含まれる場合は、`Assets` 要素の下に `ProjectTemplate` または `ItemTemplate` 要素を追加します。 新しい要素の値を、VSIX パッケージ内のテンプレートが格納されるフォルダーの相対パスに設定します。 詳細については、「[ProjectTemplate 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\))」と「[ItemTemplate 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))」を参照してください。

    - 拡張機能にプロジェクト テンプレートまたは項目テンプレートのカスタム ウィザードが含まれる場合は、`Assets` 要素の下に `Assembly` 要素を追加します。 新しい要素の値を、VSIX パッケージ内のアセンブリの相対パスに設定し、`AssemblyName` 属性を (バージョン、カルチャ、および公開キートークンを含む) 完全なアセンブリ名に設定します。 詳細については、「[Dependency 要素 (VSX スキーマ)](/previous-versions/dd393682(v=vs.110))」を参照してください。

### <a name="example"></a>例

次の例は、SharePoint ツールの拡張機能用の extension.vsixmanifest ファイルの内容を示しています。 この拡張機能は、Contoso.ProjectExtension.dll という名前のアセンブリに実装されます。 拡張機能には、Contoso.ExtensionCommands.dll という名前の SharePoint コマンド アセンブリと、VSIX パッケージの **ItemTemplates** という名前のフォルダーの下の項目テンプレートが含まれています。 この例では、両方のアセンブリが VSIX パッケージの extension.vsixmanifest ファイルと同じフォルダーにあることを前提としています。

```xml
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <Identity Id="CustomActionProjectItem.Microsoft.b99efe4d-cef3-4afd-b9af-034ca0c52743" Version="1.0" Language="en-US" Publisher="Microsoft" />
    <DisplayName>CustomActionProjectItem</DisplayName>
    <Description>Empty VSIX Project.</Description>
  </Metadata>
  <Installation>
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="11.0" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" Version="4.5" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.ItemTemplate" Path="ItemTemplates" />
    <Asset Type="Microsoft.VisualStudio.MefComponent" Path="ProjectItemDefinition.dll" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>こちらもご覧ください

- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [SharePoint オブジェクト モデルを呼び出す](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Visual Studio での SharePoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)