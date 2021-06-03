---
title: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)
titleSuffix: ''
description: 項目テンプレートを使用して、SharePoint サイトにカスタム動作を作成するために SharePoint プロジェクトに追加できるプロジェクト項目を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 71e9d83cbe3459abb05e24b127e54651aade8ee5
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217958"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-1"></a>チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)
  Visual Studio の SharePoint プロジェクト システムは、プロジェクト項目の種類を独自に作成することによって拡張することができます。 このチュートリアルでは、SharePoint プロジェクトに追加できるプロジェクト項目を作成します。これは SharePoint サイトにカスタム動作を作成するためのプロジェクト項目です。 SharePoint サイトの **[サイトの操作]** メニューに対し、カスタム動作によってメニュー項目を追加します。

 このチュートリアルでは、次のタスクについて説明します。

- カスタム動作のための SharePoint プロジェクト項目の新しい種類を定義する Visual Studio 拡張機能の作成。 この新しいプロジェクト項目の種類では、次に示すいくつかのカスタム機能を実装します。

  - プロジェクト項目に関連したさまざまな追加タスク (Visual Studio でカスタム動作を作成するためのデザイナーを表示するなど) の開始点となるショートカット メニュー。

  - 開発者がプロジェクト項目やそれを含んでいるプロジェクトの特定のプロパティを変更したときに実行されるコード。

  - **ソリューション エクスプローラー** で、プロジェクト項目の横に表示されるカスタム アイコン。

- 対応するプロジェクト項目用の Visual Studio 項目テンプレートを作成する。

- プロジェクト項目テンプレートや拡張機能のアセンブリを配置するための Visual Studio Extension (VSIX) パッケージを構築する。

- プロジェクト項目のデバッグとテストを行う。

  これは、独立したチュートリアルです。 このチュートリアルを完了すると、項目テンプレートにウィザードを追加してプロジェクト項目を拡張できるようになります。 詳細については、「[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)」を参照してください。

> [!NOTE]
> ワークフローのカスタム アクティビティを作成する方法を示すサンプルを [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) からダウンロードできます。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows、SharePoint、および Visual Studio。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 このチュートリアルでは、プロジェクト項目を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint のカスタム動作。 詳細については、「[カスタム アクション](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14))」を参照してください。

- Visual Studio の項目テンプレート。 詳細については、「[Creating Project and Item Templates](../ide/creating-project-and-item-templates.md)」 (プロジェクトと項目テンプレートの作成) をご覧ください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを実行するには、3 つのプロジェクトを作成する必要があります。

- VSIX プロジェクト。 このプロジェクトは、SharePoint プロジェクト項目を配置するための VSIX パッケージを作成します。

- 項目テンプレート プロジェクト。 このプロジェクトは、SharePoint プロジェクト項目を SharePoint プロジェクトに追加するために使用できる項目テンプレートを作成します。

- クラス ライブラリ プロジェクト。 このプロジェクトは、SharePoint プロジェクト項目の動作を定義する Visual Studio 拡張機能を実装します。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスの上部にある一覧で **[.NET Framework 4.5]** が選択されていることを確認します。

4. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** ノードをクリックします。

    > [!NOTE]
    > **[機能拡張]** ノードは、Visual Studio SDK がインストールされている場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

5. **[VSIX プロジェクト]** テンプレートを選択します。

6. **[Name]** ボックスに「**CustomActionProjectItem**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の **ソリューション エクスプローラー** に **CustomActionProjectItem** プロジェクトが追加されます。

#### <a name="to-create-the-item-template-project"></a>項目テンプレート プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの上部にある一覧で **[.NET Framework 4.5]** が選択されていることを確認します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[機能拡張]** ノードをクリックします。

4. プロジェクト テンプレートの一覧で **[C# 項目テンプレート]** または **[Visual Basic 項目テンプレート]** テンプレートを選択します。

5. **[名前]** ボックスに「**ItemTemplate**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のソリューションに **ItemTemplate** プロジェクトが追加されます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの上部にある一覧で **[.NET Framework 4.5]** が選択されていることを確認します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開します。次に、 **[Windows]** ノード、 **[クラス ライブラリ]** プロジェクト テンプレートの順にクリックします。

4. **[名前]** ボックスに「**ProjectItemDefinition**」と入力し、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**ProjectItemDefinition** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-extension-project"></a>拡張機能プロジェクトを構成する
 SharePoint プロジェクト項目の種類を定義するためのコードを記述する前に、コード ファイルおよびアセンブリ参照を拡張機能プロジェクトに追加しておく必要があります。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. **ソリューション エクスプローラー** で **ProjectItemDefinition** プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順にクリックします。

2. プロジェクト項目の一覧で **[コード ファイル]** を選択します。

3. **[名前]** ボックスに **CustomAction** という名前と適切なファイル名拡張子を入力し、 **[追加]** をクリックします。

4. **ソリューション エクスプローラー** で、**ProjectItemDefinition** プロジェクトのショートカット メニューを開き、 **[参照の追加]** をクリックします。

5. **[参照マネージャー - ProjectItemDefinition]** ダイアログ ボックスで、 **[アセンブリ]** ノード、 **[フレームワーク]** ノードの順にクリックします。

6. 次の各アセンブリの横にあるチェック ボックスをオンにします。

    - System.ComponentModel.Composition

    - System.Windows.Forms

7. **[拡張機能]** ノードを選択し、Microsoft.VisualStudio.Sharepoint アセンブリの横にあるチェック ボックスをオンにして、 **[OK]** をクリックします。

## <a name="define-the-new-sharepoint-project-item-type"></a>新しい SharePoint プロジェクト項目の種類を定義する
 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスを実装するクラスを作成して、新しいプロジェクト項目の種類の動作を定義します。 このインターフェイスは、新しい種類のプロジェクト項目を定義するたびに必ず実装します。

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>新しい SharePoint プロジェクト項目の種類を定義するには

1. ProjectItemDefinition プロジェクトで、CustomAction コード ファイルを開きます。

2. このファイル内のコードを次のコードに置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/projectitemtypedefinition/customaction.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/projectitemdefinition/customaction.vb" id="Snippet1":::

## <a name="create-an-icon-for-the-project-item-in-solution-explorer"></a>ソリューション エクスプローラーに表示されるプロジェクト項目用アイコンを作成する
 カスタム SharePoint プロジェクト項目を作成した場合、そのプロジェクト項目にはイメージ (アイコンまたはビットマップ) を関連付けることができます。 **ソリューション エクスプローラー** には、このイメージがプロジェクト項目の横に表示されます。

 次の手順では、プロジェクト項目のアイコンを実際に作成し、拡張機能のアセンブリに埋め込みます。 このアイコンは、先ほど作成した <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute> クラスの `CustomActionProjectItemTypeProvider` から参照されます。

#### <a name="to-create-a-custom-icon-for-the-project-item"></a>プロジェクト項目のカスタム アイコンを作成するには

1. **ソリューション エクスプローラー** で **ProjectItemDefinition** プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目...]** の順にクリックします。

2. プロジェクト項目の一覧で **[アイコン ファイル]** 項目を選択します。

    > [!NOTE]
    > Visual Basic プロジェクトの場合、 **[アイコン ファイル]** 項目を表示するには、 **[全般]** ノードをクリックする必要があります。

3. **[名前]** ボックスに「**CustomAction_SolutionExplorer.ico**」と入力し、 **[追加]** をクリックします。

     **イメージ エディター** に新しいアイコンが表示されます。

4. 認識しやすいデザインとなるよう 16x16 版のアイコン ファイルを編集し、アイコン ファイルを保存します。

5. **ソリューション エクスプローラー** で **[CustomAction_SolutionExplorer.ico]** をクリックします。

6. **[プロパティ]** ウィンドウで、"**ビルド アクション**" プロパティの横にある矢印をクリックします。

7. 表示された一覧で **[埋め込まれたリソース]** を選択します。

## <a name="checkpoint"></a>Checkpoint
 この段階で、プロジェクト項目に必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、プロジェクトをビルドして確認してください。

#### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. **ProjectItemDefinition** プロジェクトのショートカット メニューを開き、 **[ビルド]** をクリックします。

## <a name="create-a-visual-studio-item-template"></a>Visual Studio 項目テンプレートを作成する
 自分が定義したプロジェクト項目を他の開発者が使用できるようにするには、プロジェクト テンプレートまたは項目テンプレートを作成します。 Visual Studio で新しいプロジェクトを作成する際または既存のプロジェクトに項目を追加する際、開発者は、そのテンプレートを使用して、プロジェクト項目のインスタンスを作成します。 このチュートリアルでは、ItemTemplate プロジェクトを使用してプロジェクト項目を構成します。

#### <a name="to-create-the-item-template"></a>項目テンプレートを作成するには

1. Class1 コード ファイルを ItemTemplate プロジェクトから削除します。

2. ItemTemplate プロジェクトで、*ItemTemplate.vstemplate* ファイルを開きます。

3. ファイルの内容を次の XML に置き換え、ファイルを保存して閉じます。

    > [!NOTE]
    > 次の XML は、Visual C# の項目テンプレート用です。 Visual Basic の項目テンプレートを作成する場合は、`ProjectType` 要素の値を `VisualBasic` に置き換えてください。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
      <TemplateData>
        <DefaultName>CustomAction</DefaultName>
        <Name>Custom Action</Name>
        <Description>SharePoint Custom Action by Contoso</Description>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>1000</SortOrder>
        <Icon>ItemTemplate.ico</Icon>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
      <TemplateContent>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\Elements.xml">Elements.xml</ProjectItem>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\SharePointProjectItem.spdata">CustomAction.spdata</ProjectItem>
      </TemplateContent>
    </VSTemplate>
    ```

     このファイルには、項目テンプレートの内容と動作が定義されています。 このファイルの内容の詳細については、「[Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)」を参照してください。

4. **ソリューション エクスプローラー** で **ItemTemplate** プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

5. **[新しい項目の追加]** ダイアログ ボックスで、 **[テキスト ファイル]** テンプレートを選択します。

6. **[名前]** ボックスに「**CustomAction.spdata**」と入力し、 **[追加]** をクリックします。

7. 次の XML を *CustomAction.spdata* ファイルに追加し、ファイルを保存して閉じます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ProjectItem Type="Contoso.CustomAction" DefaultFile="Elements.xml"
     xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
      <Files>
        <ProjectItemFile Source="Elements.xml" Target="$fileinputname$\" Type="ElementManifest" />
      </Files>
    </ProjectItem>
    ```

     このファイルには、プロジェクト項目に含まれている各ファイルに関する情報が格納されます。 `Type` 要素の `ProjectItem` 属性には、プロジェクト項目定義 (先ほど作成した <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> クラス) の `CustomActionProjectItemTypeProvider` に渡した文字列を設定します。 *.spdata* ファイルの内容の詳細については、[SharePoint プロジェクト項目スキーマのリファレンス](../sharepoint/sharepoint-project-item-schema-reference.md)に関するページを参照してください。

8. **ソリューション エクスプローラー** で **ItemTemplate** プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

9. **[新しい項目の追加]** ダイアログ ボックスで **[XML ファイル]** テンプレートを選択します。

10. **[名前]** ボックスに「**Elements.xml**」と入力し、 **[追加]** をクリックします。

11. *Elements.xml* ファイルの内容を次の XML に置き換え、ファイルを保存して閉じます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="Replace this with a GUID or some other unique string"
                    GroupId="SiteActions"
                    Location="Microsoft.SharePoint.StandardMenu"
                    Sequence="1000"
                    Title="Replace this with your title"
                    Description="Replace this with your description" >
        <UrlAction Url="~site/Lists/Tasks/AllItems.aspx"/>
      </CustomAction>
    </Elements>
    ```

     このファイルは、SharePoint サイトの **[サイトの操作]** メニューのメニュー項目を作成する既定のカスタム動作を定義します。 ユーザーがメニュー項目をクリックすると、`UrlAction` 要素に指定された URL が Web ブラウザーに表示されます。 カスタム動作の定義に使用できる XML 要素の詳細については、[カスタム動作の定義](/sharepoint/dev/schema/custom-action-definition-schema)に関するページを参照してください。

12. 必要に応じて、*ItemTemplate.ico* ファイルを開き、わかりやすいデザインに変更します。 **[新しい項目の追加]** ダイアログ ボックスで、対応するプロジェクト項目の横にこのアイコンが表示されます。

13. **ソリューション エクスプローラー** で、**ItemTemplate** プロジェクトのショートカット メニューを開き、 **[プロジェクトのアンロード]** をクリックします。

14. **ItemTemplate** プロジェクトのショートカット メニューを開き、 **[ItemTemplate.csproj の編集]** または **[ItemTemplate.vbproj の編集]** をクリックします。

15. プロジェクト ファイルで次の `VSTemplate` 要素を見つけます。

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
    ```

16. `VSTemplate` 要素を次の XML に置き換え、ファイルを保存して閉じます。

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath` 要素は、プロジェクトをビルドすると項目テンプレートが作成されるパス内の追加フォルダーを指定します。 ここで指定されたフォルダー内の項目テンプレートが使用可能になるのは、顧客が **[新しい項目の追加]** ダイアログ ボックスを開き、 **[SharePoint]** ノードを展開して、 **[2010]** ノードを選択したときのみです。

17. **ソリューション エクスプローラー** で、**ItemTemplate** プロジェクトのショートカット メニューを開き、 **[プロジェクトの再読み込み]** をクリックします。

## <a name="create-a-vsix-package-to-deploy-the-project-item"></a>プロジェクト項目を配置するための VSIX パッケージを作成する
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューション エクスプローラー** で、CustomActionProjectItem プロジェクトの **source.extension.vsixmanifest** ファイルのショートカット メニューを開き、 **[開く]** をクリックします。

     Visual Studio によってマニフェスト エディターでファイルが開きます。 source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「[VSIX 拡張機能スキーマ 1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. **[プロジェクト名]** ボックスに「**Custom Action Project Item**」と入力します。

3. **[作成者]** ボックスに、「**Contoso**」と入力します。

4. **[説明]** ボックスに、「**A SharePoint project item that represents a custom action**」(カスタム動作を表す SharePoint プロジェクト項目) と入力します。

5. **[アセット]** タブで **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

6. **[種類]** ボックスの一覧で **[Microsoft.VisualStudio.ItemTemplate]** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `ItemTemplate` 要素に対応します。 プロジェクト項目テンプレートが格納される VSIX パッケージ内のサブフォルダーは、この要素によって指定されます。 詳細については、[ItemTemplate 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\)) に関するページを参照してください。

7. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

8. **[プロジェクト]** ボックスの一覧で **[ItemTemplate]** を選択し、 **[OK]** をクリックします。

9. **[アセット]** タブで、もう一度 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

10. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.MefComponent]** を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「[MEFComponent 要素 (VSX スキーマ)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

11. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

12. **[プロジェクト]** ボックスの一覧で **[ProjectItemDefinition]** を選択します。

13. **[OK]** を選択します。

14. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックし、プロジェクトがエラーなしでコンパイルされたことを確認します。

15. CustomActionProjectItem プロジェクトのビルド出力フォルダーに CustomActionProjectItem.vsix ファイルが格納されていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、CustomActionProjectItem プロジェクトが格納されているフォルダーの下にあります。

## <a name="test-the-project-item"></a>プロジェクト項目をテストする
 これで、プロジェクト項目をテストする準備ができました。 まず、Visual Studio の実験用インスタンスで CustomActionProjectItem ソリューションのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで、SharePoint プロジェクトの **カスタム動作** プロジェクト項目をテストします。 最後に、SharePoint プロジェクトをビルドして実行し、カスタム動作が正常に機能することを確認します。

#### <a name="to-start-debugging-the-solution"></a>ソリューションのデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、CustomActionProjectItem ソリューションを開きます。

2. CustomAction コード ファイルを開き、`InitializeType` メソッドのコードの先頭行にブレークポイントを追加します。

3. **F5** キーを押してデバッグを開始します。

     Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Custom Action Project Item\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-project-item-in-visual-studio"></a>Visual Studio でプロジェクト項目をテストするには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

2. (項目テンプレートがサポートする言語に応じて) **[Visual C#]** または **[Visual Basic]** を展開し、 **[SharePoint]** を展開して、 **[2010]** ノードをクリックします。

3. プロジェクト テンプレートの一覧で **[SharePoint 2010 プロジェクト]** を選択します。

4. **[名前]** ボックスに「**CustomActionTest**」と入力し、 **[OK]** をクリックします。

5. **SharePoint カスタマイズ ウィザード** で、デバッグに使用するサイトの URL を入力し、 **[完了]** をクリックします。

6. **ソリューション エクスプローラー** でプロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

7. **[新しい項目の追加]** ダイアログ ボックスで、 **[SharePoint]** ノードの下の **[2010]** ノードをクリックします。

     **[カスタム動作]** 項目がプロジェクト項目の一覧に表示されることを確認します。

8. **[カスタム動作]** 項目を選択し、 **[追加]** をクリックします。

     Visual Studio によって、**CustomAction1** という名前の項目がプロジェクトに追加され、エディターに *Elements.xml* ファイルが表示されます。

9. Visual Studio のもう一方のインスタンスで、先ほど `InitializeType` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

10. **F5** キーを押して、プロジェクトのデバッグを続行します。

11. Visual Studio の実験用インスタンスで、**ソリューション エクスプローラー** を開き、 **[CustomAction1]** ノードのショートカット メニューを開いて、 **[カスタム動作デザイナーの表示]** をクリックします。

12. メッセージ ボックスが表示されることを確認して、 **[OK]** をクリックします。

     このショートカット メニューを使用して、追加のオプションやコマンド (カスタム動作のデザイナーを表示するなど) を開発者に提供することができます。

13. メニュー バーで **[表示]**  >  **[出力]** の順に選択します。

     **[出力]** ウィンドウが開きます。

14. **ソリューション エクスプローラー** で、 **[CustomAction1]** 項目のショートカット メニューを開き、その名前を「**MyCustomAction**」に変更します。

     **[出力]** ウィンドウに確認メッセージが表示されます。 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemNameChanged> クラスに定義した `CustomActionProjectItemTypeProvider` イベント ハンドラーによってメッセージが出力されます。 このイベントを初めとする、プロジェクト項目の各種イベントを処理することにより、プロジェクト項目に対して開発者が変更を加えたときのカスタム動作を実装することができます。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>SharePoint のカスタム動作をテストするには

1. Visual Studio の実験用インスタンスで、 **[MyCustomAction]** プロジェクト項目の子である *Elements.xml* ファイルを開きます。

2. *Elements.xml* ファイルで、次の変更を行い、ファイルを保存します。

    - `CustomAction` 要素で、次の例に示すように、`Id` 属性を GUID などの一意の文字列に設定します。

        ```xml
        Id="cd85f6a7-af2e-44ab-885a-0c795b52121a"
        ```

    - `CustomAction` 要素で、次の例に示すように、`Title` 属性を設定します。

        ```xml
        Title="SharePoint Developer Center"
        ```

    - `CustomAction` 要素で、次の例に示すように、`Description` 属性を設定します。

        ```xml
        Description="Opens the SharePoint Developer Center Web site."
        ```

    - `UrlAction` 要素で、次の例に示すように、`Url` 属性を設定します。

        ```xml
        Url="https://docs.microsoft.com/sharepoint/dev/"
        ```

3. **F5** キーを押します。

     カスタム動作がパッケージ化され、プロジェクトの "**サイト URL**" プロパティで指定された SharePoint サイトに配置されます。 Web ブラウザーには、このサイトの既定のページが表示されます。

    > [!NOTE]
    > **[スクリプト デバッグが無効]** ダイアログ ボックスが表示された場合は、 **[はい]** をクリックしてプロジェクトをデバッグします。

4. **[サイトの操作]** メニューで、 **[SharePoint デベロッパー センター]** を選択し、ブラウザーで https://docs.microsoft.com/sharepoint/dev/ の Web サイトが開かれていることを確認してから、Web ブラウザーを閉じます。

## <a name="clean-up-the-development-computer"></a>開発コンピューターをクリーンアップする
 プロジェクト項目のテストが終わったら、プロジェクト項目テンプレートを Visual Studio の実験用インスタンスから削除します。

#### <a name="to-clean-up-the-development-computer"></a>開発コンピューターをクリーンアップするには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で **[カスタム動作プロジェクト項目]** を選択し、 **[アンインストール]** をクリックします。

3. 表示されたダイアログ ボックスで、 **[はい]** をクリックして、拡張機能をアンインストールすることを確認します。

4. **[今すぐ再起動]** をクリックして、アンインストールを完了します。

5. Visual Studio の実験用インスタンスと、CustomActionProjectItem ソリューションが開いているインスタンスの両方を閉じます。

## <a name="next-steps"></a>次のステップ
 このチュートリアルを完了すると、項目テンプレートにウィザードを追加できるようになります。 ユーザーがカスタム動作プロジェクト項目を SharePoint プロジェクトに追加するときに、このウィザードは動作についての情報 (その動作が選択されたときに移動するための場所と URL など) を収集し、*Elements.xml* ファイルの新しいプロジェクト項目にこの情報を追加します。 詳細については、「[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [SharePoint プロジェクト サービスを使用する](../sharepoint/using-the-sharepoint-project-service.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [アイコン用イメージ エディター](/cpp/windows/image-editor-for-icons)
- [アイコンまたはその他のイメージの作成 &#40;アイコン用イメージ エディター&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)