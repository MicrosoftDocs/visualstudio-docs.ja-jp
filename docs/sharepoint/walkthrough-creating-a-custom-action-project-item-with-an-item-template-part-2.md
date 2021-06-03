---
title: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)
titleSuffix: ''
description: このチュートリアルでは、項目テンプレートを使用して SharePoint サイトでカスタム動作プロジェクト項目を追加するときに、ユーザーから情報を収集するウィザードを追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], creating template wizards
- SharePoint project items, creating template wizards
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4b6fad27342c086e551320977cdf712f816b383c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217945"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)
  SharePoint プロジェクト項目のカスタム種類を定義し、Visual Studio でその種類を項目テンプレートと関連付けてから、テンプレート用のウィザードを用意することもできます。 ウィザードを使用すると、ユーザーがテンプレートを使用してプロジェクト項目の新しいインスタンスをプロジェクトに追加するときに、ユーザーから情報を収集できます。 収集した情報を使用して、プロジェクト項目を初期化できます。

 このチュートリアルでは、「[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」で説明されているカスタム動作プロジェクト項目にウィザードを追加します。 ユーザーがカスタム動作プロジェクト項目を SharePoint プロジェクトに追加するときに、このウィザードはカスタム動作についての情報 (エンド ユーザーがその動作を選択したときに移動するための場所や URL など) を収集し、*Elements.xml* ファイルの新しいプロジェクト項目にこの情報を追加します。

 このチュートリアルでは、次のタスクについて説明します。

- 項目テンプレートに関連付けるカスタム SharePoint プロジェクト項目の種類に対するウィザードを作成します。

- Visual Studio の SharePoint プロジェクト項目用の組み込みウィザードと似たカスタム ウィザードの UI を定義します。

- 置き換え可能パラメーターを使用して、ウィザードで収集したデータで SharePoint プロジェクト ファイルを初期化します。

- ウィザードをデバッグおよびテストします。

> [!NOTE]
> ワークフローのカスタム アクティビティを作成する方法を示すサンプルを [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) からダウンロードできます。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、まず「[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」を完了して、CustomActionProjectItem ソリューションを作成する必要があります。

 また、このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、プロジェクト項目を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- Visual Studio のプロジェクトおよび項目テンプレート用のウィザード。 詳細については、「[方法: プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)」と <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを参照してください。

- SharePoint のカスタム動作。 詳細については、「[カスタム アクション](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14))」を参照してください。

## <a name="create-the-wizard-project"></a>ウィザード プロジェクトを作成する
 このチュートリアルを完了するには、「[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」で作成した CustomActionProjectItem ソリューションにプロジェクトを追加する必要があります。 このプロジェクトで、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装し、ウィザードの UI を定義します。

#### <a name="to-create-the-wizard-project"></a>ウィザード プロジェクトを作成するには

1. Visual Studio で、CustomActionProjectItem ソリューションを開きます

2. **ソリューション エクスプローラー** でソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードをクリックします。

4. **[新しいプロジェクト]** ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で、 **[.NET Framework 4.5]** が選択されていることを確認します。

5. **[WPF ユーザー コントロール ライブラリ]** プロジェクト テンプレートを選択し、プロジェクトに **ItemTemplateWizard** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、ソリューションに **ItemTemplateWizard** プロジェクトが追加されます。

6. [UserControl1] 項目をプロジェクトから削除します。

## <a name="configure-the-wizard-project"></a>ウィザード プロジェクトを構成する
 ウィザードを作成する前に、Windows Presentation Foundation (WPF) ウィンドウ、コード ファイル、およびアセンブリ参照をプロジェクトに追加する必要があります。

#### <a name="to-configure-the-wizard-project"></a>ウィザード プロジェクトを構成するには

1. **ソリューション エクスプローラー** で、 **[ItemTemplateWizard]** プロジェクト ノードのショートカット メニューを開き、 **[プロパティ]** をクリックします。

2. **プロジェクト デザイナー** で、ターゲット フレームワークが .NET Framework 4.5 に設定されていることを確認します。

     Visual C# プロジェクトの場合は、 **[アプリケーション]** タブでこの値を設定できます。Visual Basic プロジェクトの場合は、 **[コンパイル]** タブでこの値を設定できます。詳細については、「[方法: .NET Framework のバージョンをターゲットにする](../ide/visual-studio-multi-targeting-overview.md)」を参照してください。

3. **ItemTemplateWizard** プロジェクトで、 **[ウィンドウ (WPF)]** 項目をプロジェクトに追加し、その項目に **WizardWindow** という名前を付けます。

4. CustomActionWizard と String という名前の 2 つのコード ファイルを追加します。

5. **ItemTemplateWizard** プロジェクトのショートカット メニューを開き、 **[参照の追加]** をクリックします。

6. **[参照マネージャー - ItemTemplateWizard]** ダイアログ ボックスの **[アセンブリ]** ノードの下で、 **[拡張機能]** ノードを選択します。

7. 次のアセンブリの横にあるチェック ボックスをオンにして、 **[OK]** をクリックします。

    - EnvDTE

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

8. **ソリューション エクスプローラー** の ItemTemplateWizard プロジェクトの **[参照]** フォルダーで、**EnvDTE** 参照を選択します。

9. **[プロパティ]** ウィンドウで、"**相互運用型の埋め込み**" プロパティの値を **False** に変更します。

## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>カスタム動作の既定の場所および ID 文字列を定義する
 すべてのカスタム動作には、*Elements.xml* ファイルの `CustomAction` 要素の `GroupID` および `Location` 属性で指定された場所と ID があります。 この手順では、ItemTemplateWizard プロジェクトでのこれらの属性の有効な値の一部を定義します。 このチュートリアルを完了すると、ユーザーがウィザードで場所と ID を指定したときに、これらの文字列がカスタム動作プロジェクト項目の *Elements.xml* ファイルに書き込まれます。

 わかりやすくするために、このサンプルでは、使用可能な既定の場所と ID のサブセットのみをサポートしています。 完全な一覧については、「[カスタム アクションの既定の場所および ID](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))」を参照してください。

#### <a name="to-define-the-default-location-and-id-strings"></a>既定の場所と ID 文字列を定義するには

1. 開きます。

2. **ItemTemplateWizard** プロジェクトで、文字列コード ファイル内のコードを次のコードに置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs" id="Snippet6":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb" id="Snippet6":::

## <a name="create-the-wizard-ui"></a>ウィザード UI を作成する
 XAML を追加してウィザードの UI を定義し、いくつかのコードを追加してウィザードの一部のコントロールを ID 文字列にバインドします。 作成するウィザードは、Visual Studio の SharePoint プロジェクト用の組み込みウィザードに似ています。

#### <a name="to-create-the-wizard-ui"></a>ウィザード UI を作成するには

1. **ItemTemplateWizard** プロジェクトで、**WizardWindow.xaml** ファイルのショートカット メニューを開き、 **[開く]** をクリックしてウィンドウをデザイナーで開きます。

2. XAML ビューで、現在の XAML を次の XAML に置き換えます。 XAML は、見出し、カスタム動作の振る舞いを指定するコントロール、ウィンドウの下部にあるナビゲーション ボタンを含む UI を定義します。

    > [!NOTE]
    > このコードを追加した後で、プロジェクトでいくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml" id="Snippet9":::

    > [!NOTE]
    > この XAML で作成するウィンドウは <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基底クラスから派生します。 カスタムの WPF ダイアログ ボックスを Visual Studio に追加する場合は、ダイアログ ボックスをこのクラスから派生し、スタイルを Visual Studio の他のダイアログ ボックスと一貫させて、そうしなければモーダル ダイアログ ボックスで発生する可能性のある問題を回避することをお勧めします。 詳細については、「[モーダル ダイアログ ボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

3. Visual Basic プロジェクトを開発している場合は、`Window` 要素の `x:Class` 属性の `WizardWindow` クラス名から `ItemTemplateWizard` 名前空間を削除します。 この要素は XAML の 1 行目にあります。 完了すると、最初の行は次のコードのようになります。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. WizardWindow.xaml ファイルの分離コード ファイルで、現在のコードを次のコードに置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs" id="Snippet7":::

## <a name="implement-the-wizard"></a>ウィザードを実装する
 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装して、ウィザードの機能を定義します。

#### <a name="to-implement-the-wizard"></a>ウィザードを実装するには

1. **ItemTemplateWizard** プロジェクトで、**CustomActionWizard** コード ファイルを開き、このファイルの現在のコードを次のコードに置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs" id="Snippet8":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb" id="Snippet8":::

## <a name="checkpoint"></a>Checkpoint
 この段階で、ウィザードに必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、プロジェクトをビルドして確認してください。

#### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="associate-the-wizard-with-the-item-template"></a>ウィザードを項目テンプレートに関連付ける
 ウィザードの実装が完了したので、次の 3 つの主要な手順を実行して、このウィザードを **[カスタム動作]** 項目テンプレートに関連付ける必要があります。

1. ウィザード アセンブリに厳密な名前で署名します。

2. ウィザード アセンブリの公開キー トークンを取得します。

3. **[カスタム動作]** 項目テンプレートの .vstemplate ファイルに、ウィザード アセンブリへの参照を追加します。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>ウィザード アセンブリに厳密な名前で署名するには

1. **ソリューション エクスプローラー** で、 **[ItemTemplateWizard]** プロジェクト ノードのショートカット メニューを開き、 **[プロパティ]** をクリックします。

2. **[署名]** タブの **[アセンブリの署名]** チェック ボックスをオンにします。

3. **[厳密な名前のキー ファイルを選択してください]** ボックスの一覧で **\<New...>** を選択します。

4. **[厳密な名前キーの作成]** ダイアログ ボックスで名前を入力し、 **[キー ファイルをパスワードで保護する]** チェック ボックスをオフにして、 **[OK]** をクリックします。

5. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>ウィザード アセンブリの公開キー トークンを取得するには

1. Visual Studio のコマンド プロンプト ウィンドウで、*PathToWizardAssembly* を、開発用コンピューターの ItemTemplateWizard プロジェクトのビルドされた ItemTemplateWizard.dll アセンブリへの完全パスに置き換えて、次のコマンドを実行します。

    ```xml
    sn.exe -T PathToWizardAssembly
    ```

     *ItemTemplateWizard.dll* アセンブリに対する公開キー トークンが Visual Studio コマンド プロンプト ウィンドウに記述されます。

2. Visual Studio コマンド プロンプト ウィンドウは開いたままにします。 次の手順を完了するには、公開キー トークンが必要です。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>.vstemplate ファイルにウィザード アセンブリへの参照を追加するには

1. **ソリューション エクスプローラー** で、 **[ItemTemplate]** プロジェクト ノードを展開し、*ItemTemplate.vstemplate* ファイルを開きます。

2. ファイルの末尾の近くで、次の `WizardExtension` 要素を `</TemplateContent>` タグと `</VSTemplate>` タグの間に追加します。 `PublicKeyToken` 属性の *YourToken* の値は、前の手順で取得した公開キー トークンで置き換えます。

    ```xml
    <WizardExtension>
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>
    </WizardExtension>
    ```

     `WizardExtension` 要素の詳細については、[WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md) に関するページを参照してください。

3. ファイルを保存して閉じます。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>項目テンプレートの *Elements.xml* ファイルに置き換え可能パラメーターを追加する
 複数の置き換え可能パラメーターを、ItemTemplate プロジェクトの *Elements.xml* ファイルに追加します。 これらのパラメーターは、前に定義した `PopulateReplacementDictionary` クラスの `CustomActionWizard` メソッドで初期化されます。 ユーザーがカスタム動作プロジェクト項目をプロジェクトに追加すると、Visual Studio によって自動的に、新しいプロジェクト項目の *Elements.xml* ファイル内のこれらのパラメーターが、ウィザードでユーザーが指定した値に置き換えられます。

 置き換え可能パラメーターはトークンであり、先頭と末尾にはドル記号 ($) が付いています。 独自の置き換え可能パラメーターを定義するだけでなく、SharePoint プロジェクト システムで定義および初期化される組み込みパラメーターを使用することもできます。 詳細については、「[置き換え可能パラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>置き換え可能パラメーターを *Elements.xml* ファイルに追加するには

1. ItemTemplate プロジェクトで、*Elements.xml* ファイルの内容を次の XML に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="$IdValue$"
                    GroupId="$GroupIdValue$"
                    Location="$LocationValue$"
                    Sequence="1000"
                    Title="$TitleValue$"
                    Description="$DescriptionValue$" >
        <UrlAction Url="$UrlValue$"/>
      </CustomAction>
    </Elements>
    ```

     新しい XML では、`Id`、`GroupId`、`Location`、`Description`、`Url` の各属性の値が置き換え可能パラメーターに変更されます。

2. ファイルを保存して閉じます。

## <a name="add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加する
 VSIX プロジェクトの source.extension.vsixmanifest ファイルで、プロジェクト項目が含まれている VSIX パッケージと共に配置されるように、ウィザード プロジェクトへの参照を追加します。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加するには

1. **ソリューション エクスプローラー** で、CustomActionProjectItem プロジェクトの **source.extension.vsixmanifest** ファイルのショートカット メニューを開き、 **[開く]** をクリックしてマニフェスト エディターでファイルを開きます。

2. マニフェスト エディターで、 **[アセット]** タブを選択し、 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログ ボックスが表示されます。

3. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.Assembly]** を選択します。

4. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

5. **[プロジェクト]** ボックスの一覧で **[ItemTemplateWizard]** を選択し、 **[OK]** をクリックします。

6. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順に選択し、ソリューションがエラーなしでコンパイルされることを確認します。

## <a name="test-the-wizard"></a>ウィザードをテストする
 これで、ウィザードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで CustomActionProjectItem ソリューションのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで、SharePoint プロジェクトのカスタム動作プロジェクト項目のウィザードをテストします。 最後に、SharePoint プロジェクトをビルドして実行し、カスタム動作が正常に機能することを確認します。

#### <a name="to-start-to-debug-the-solution"></a>ソリューションのデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、CustomActionProjectItem ソリューションを開きます。

2. ItemTemplateWizard プロジェクトで、CustomActionWizard コード ファイルを開き、`RunStarted` メソッド内のコードの 1 行目にブレークポイントを追加します。

3. メニュー バーで **[デバッグ]**  >  **[例外]** の順に選択します。

4. **[例外]** ダイアログ ボックスで、 **[Common Language Runtime Exceptions]** の **[スローされるとき]** チェック ボックスと **[ユーザーにハンドルされていないとき]** チェック ボックスがオフになっていることを確認して、 **[OK]** をクリックします。

5. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順にクリックして、デバッグを開始します。

     Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Action Project Item\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-wizard-in-visual-studio"></a>Visual Studio でウィザードをテストするには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

2. (項目テンプレートがサポートする言語に応じて) **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[SharePoint]** ノードを展開して、 **[2010]** ノードをクリックします。

3. プロジェクト テンプレートの一覧で **[SharePoint 2010 プロジェクト]** を選択し、プロジェクトに **CustomActionWizardTest** という名前を付けて、 **[OK]** をクリックします。

4. **SharePoint カスタマイズ ウィザード** で、デバッグに使用するサイトの URL を入力し、 **[完了]** をクリックします。

5. **ソリューション エクスプローラー** でプロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

6. **[新しい項目の追加 - CustomItemWizardTest]** ダイアログ ボックスで、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを展開します。

7. プロジェクト項目の一覧で、 **[カスタム動作]** 項目を選択し、 **[追加]** をクリックします。

8. Visual Studio のもう一方のインスタンスで、先ほど `RunStarted` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

9. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[続行]** の順にクリックして、プロジェクトのデバッグを続行します。

     SharePoint カスタマイズ ウィザードが表示されます。

10. **[場所]** で、 **[リストの編集]** オプション ボタンをクリックします。

11. **[グループ ID]** ボックスの一覧で、 **[通信]** を選択します。

12. **[タイトル]** ボックスに「**SharePoint Developer Center**」(SharePoint デベロッパー センター) と入力します。

13. **[説明]** ボックスに「**Opens the SharePoint Developer Center website**」(SharePoint デベロッパー センター Web サイトを開く) と入力します。

14. **[URL]** ボックスに **https://docs.microsoft.com/sharepoint/dev/** と入力し、 **[完了]** をクリックします。

     Visual Studio によって、**CustomAction1** という名前の項目がプロジェクトに追加され、エディターに *Elements.xml* ファイルが表示されます。 *Elements.xml* にウィザードで指定した値が含まれることを確認します。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>SharePoint のカスタム動作をテストするには

1. Visual Studio の実験用インスタンスで、**F5** キーを押すか、メニュー バーで **[デバッグ]**  >  **[デバッグの開始]** の順に選択します。

     カスタム動作がパッケージ化され、プロジェクトの "**サイト URL**" プロパティで指定された SharePoint サイトに配置されます。Web ブラウザーが開き、このサイトの既定のページが表示されます。

    > [!NOTE]
    > **[スクリプト デバッグが無効]** ダイアログ ボックスが表示されたら、 **[はい]** をクリックします。

2. SharePoint サイトの [リスト] 領域で、 **[タスク]** リンクを選択します。

     **[タスク - すべてのタスク]** ページが表示されます。

3. リボンの **[リスト ツール]** タブで、 **[リスト]** タブを選択し、 **[設定]** グループで **[リストの設定]** を設定します。

     **[リストの設定]** ページが表示されます。

4. ページの上部近くにある **[通信]** の見出しの下で、 **[SharePoint デベロッパー センター]** リンクを選択し、ブラウザーで https://docs.microsoft.com/sharepoint/dev/ の Web サイトが開いていることを確認してからブラウザーを閉じます。

## <a name="cleaning-up-the-development-computer"></a>開発コンピューターのクリーンアップ
 プロジェクト項目のテストが終わったら、プロジェクト項目テンプレートを Visual Studio の実験用インスタンスから削除します。

#### <a name="to-clean-up-the-development-computer"></a>開発コンピューターをクリーンアップするには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で **[カスタム動作プロジェクト項目]** 拡張機能を選択し、 **[アンインストール]** をクリックします。

3. 表示されるダイアログ ボックスで、 **[はい]** をクリックして拡張機能のアンインストールを確定し、 **[今すぐ再起動]** をクリックしてアンインストールを完了します。

4. Visual Studio の両方のインスタンス (実験用インスタンスと CustomActionProjectItem ソリューションを開いたインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
- [カスタム アクションの既定の場所と ID](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))
