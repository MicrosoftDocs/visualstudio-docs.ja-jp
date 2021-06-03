---
title: プロジェクト テンプレートを使用してサイト列プロジェクト項目を作成する (パート 2)
titleSuffix: ''
description: サイト列プロジェクト テンプレートにウィザードを追加して、ユーザーがテンプレートを使用してプロジェクト項目を含む SharePoint プロジェクトを作成するときに、ユーザーからデータを収集します。
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
ms.openlocfilehash: 13a2f2c147bbf175a7601cd465dc8acbba9b5388
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217750"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>チュートリアル: プロジェクト テンプレートを使用してサイト列プロジェクト項目を作成する (パート 2)
  SharePoint プロジェクト項目のカスタム種類を定義し、Visual Studio でその種類をプロジェクト テンプレートと関連付けてから、テンプレート用のウィザードを用意することもできます。 ウィザードを使用すると、ユーザーがテンプレートを使用してプロジェクト項目を含む新しいプロジェクトを作成するときに、ユーザーから情報を収集できます。 収集した情報を使用して、プロジェクト項目を初期化できます。

 このチュートリアルでは、「[チュートリアル: プロジェクト テンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」で説明されている [サイト列] プロジェクト テンプレートにウィザードを追加します。 ユーザーが Site Column プロジェクトを作成するときに、ウィザードは、サイト内の列に関する情報 (その基本型やグループなど) を収集し、この情報を新しいプロジェクトの *Elements.xml* ファイルに追加します。

 このチュートリアルでは、次のタスクについて説明します。

- プロジェクト テンプレートに関連付けるカスタム SharePoint プロジェクト項目の種類に対するウィザードを作成します。

- Visual Studio の SharePoint プロジェクト用の組み込みウィザードと似たカスタム ウィザードの UI を定義します。

- ウィザードの実行中にローカル SharePoint サイトへの呼び出しを行うために使用される 2 つの "*SharePoint コマンド*" を作成します。 SharePoint コマンドは、SharePoint サーバー オブジェクト モデルの API を呼び出すために Visual Studio 拡張機能で使用できるメソッドです。 詳細については、[SharePoint オブジェクト モデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)に関するページを参照してください。

- 置き換え可能パラメーターを使用して、ウィザードで収集したデータで SharePoint プロジェクト ファイルを初期化します。

- 新しい各 Site Column プロジェクト インスタンスで新しい .snk ファイルを作成します。 このファイルを使用してプロジェクトの出力に署名し、SharePoint ソリューション アセンブリをグローバル アセンブリ キャッシュに配置できるようにします。

- ウィザードをデバッグおよびテストします。

> [!NOTE]
> 一連のサンプル ワークフローについては、「[SharePoint ワークフローのサンプル](/sharepoint/dev/general-development/sharepoint-workflow-samples)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、まず「[チュートリアル: プロジェクト テンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」を完了して、SiteColumnProjectItem ソリューションを作成する必要があります。

 また、このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、プロジェクト項目を配置するための VSIX パッケージを、SDK の **VSIX プロジェクト** テンプレートを使用して作成します。 詳細については、「[Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- Visual Studio のプロジェクトおよび項目テンプレート用のウィザード。 詳細については、「[方法: プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)」と <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを参照してください。

- SharePoint のサイト内の列。 詳細については、「[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))」を参照してください。

## <a name="understand-the-wizard-components"></a>ウィザードのコンポーネントについて
 このチュートリアルで説明されているウィザードには、いくつかのコンポーネントが含まれています。 次の表は、これらのコンポーネントについての説明です。

|コンポーネント|説明|
|---------------|-----------------|
|ウィザード実装|これは `SiteColumnProjectWizard` という名前のクラスであり、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装します。 このインターフェイスは、ウィザードの起動および終了時と、ウィザードの実行中の特定のタイミングで Visual Studio によって呼び出されるメソッドを定義します。|
|ウィザード UI|これは、`WizardWindow` という名前の WPF ベースのウィンドウです。 このウィンドウには、`Page1` および `Page2` という名前の 2 つのユーザー コントロールが含まれます。 これらのユーザー コントロールは、ウィザードの 2 つのページを表します。<br /><br /> このチュートリアルでは、ウィザード実装の <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドによって、ウィザード UI が表示されます。|
|ウィザード データ モデル|これは、`SiteColumnWizardModel` という名前の中間クラスであり、ウィザード UI とウィザード実装の間のレイヤーを提供します。 このサンプルでは、このクラスを使用して、ウィザード実装とウィザード UI を互いに抽象化できるようにします。このクラスは、すべてのウィザードで必須コンポーネントとなるわけではありません。<br /><br /> このチュートリアルでは、ウィザード UI が表示されるときに、ウィザード実装によって、ウィザード ウィンドウに `SiteColumnWizardModel` オブジェクトが渡されます。 ウィザード UI は、このオブジェクトのメソッドを使用して UI にコントロールの値を保存し、入力されたサイト URL が有効であることの確認などのタスクを実行します。 ユーザーがウィザードを終了すると、ウィザード実装は `SiteColumnWizardModel` オブジェクトを使用して、UI の最終的な状態を判断します。|
|プロジェクト署名マネージャー|これは、`ProjectSigningManager` という名前のヘルパー クラスであり、新しい各プロジェクト インスタンスで新しい key.snk ファイルを作成するためにウィザード実装によって使用されます。|
|SharePoint コマンド|これらは、ウィザードの実行中にローカル SharePoint サイトへの呼び出しを行うためにウィザード データ モデルによって使用されるメソッドです。 SharePoint コマンドは .NET Framework 3.5 をターゲットとする必要があるため、これらのコマンドは他のウィザード コードとは異なるアセンブリに実装されます。|

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、「[チュートリアル: プロジェクト テンプレートを使用してサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」で作成した SiteColumnProjectItem ソリューションに複数のプロジェクトを追加する必要があります。

- WPF プロジェクト。 このプロジェクトで、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装し、ウィザードの UI を定義します。

- SharePoint コマンドを定義するクラス ライブラリ プロジェクト。 このプロジェクトは .NET Framework 3.5 を対象にする必要があります。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-wpf-project"></a>WPF プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、SiteColumnProjectItem ソリューションを開きます。

2. **ソリューション エクスプローラー** で **[SiteColumnProjectItem]** ソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。

3. **[新しいプロジェクトの追加]** ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で、 **[.NET Framework 4.5]** が選択されていることを確認します。

4. **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードをクリックします。

5. プロジェクト テンプレートの一覧で **[WPF ユーザー コントロール ライブラリ]** を選択し、プロジェクトに **ProjectTemplateWizard** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**ProjectTemplateWizard** プロジェクトがソリューションに追加され、既定の UserControl1.xaml ファイルが開きます。

6. UserControl1.xaml ファイルをプロジェクトから削除します。

#### <a name="to-create-the-sharepoint-commands-project"></a>SharePoint コマンド プロジェクトを作成するには

1. **ソリューション エクスプローラー** で [SiteColumnProjectItem] ソリューション ノードのショートカット メニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順にクリックします。

2. **[新しいプロジェクトの追加]** ダイアログ ボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 3.5]** を選択します。

3. **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードをクリックします。

4. **[クラス ライブラリ]** プロジェクト テンプレートを選択し、プロジェクトに **SharePointCommands** という名前を付けて、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**SharePointCommands** プロジェクトがソリューションに追加され、既定の Class1 コード ファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-projects"></a>プロジェクトを構成する
 ウィザードを作成する前に、いくつかのコード ファイルとアセンブリ参照をプロジェクトに追加する必要があります。

#### <a name="to-configure-the-wizard-project"></a>ウィザード プロジェクトを構成するには

1. **ソリューション エクスプローラー** で、 **[ProjectTemplateWizard]** プロジェクト ノードのショートカット メニューを開き、 **[プロパティ]** をクリックします。

2. **プロジェクト デザイナー** で、Visual C# プロジェクトの場合は **[アプリケーション]** タブを選択し、Visual Basic プロジェクトの場合は **[コンパイル]** タブを選択します。

3. ターゲット フレームワークが .NET Framework 4.5 Client Profile ではなく .NET Framework 4.5 に設定されていることを確認します。

     詳細については、「[方法: .NET Framework のバージョンをターゲットにする](../ide/visual-studio-multi-targeting-overview.md)」を参照してください。

4. **ProjectTemplateWizard** プロジェクトのショートカット メニューを開き、 **[追加]** をクリックし、 **[新しい項目]** を選択します。

5. **[ウィンドウ (WPF)]** 項目を選択し、項目に **WizardWindow** という名前を付けて、 **[追加]** をクリックします。

6. 2 つの **[ユーザー コントロール (WPF)]** 項目をプロジェクトに追加し、それらの項目に **Page1** と **Page2** という名前を付けます。

7. 次の名前で 4 つのコード ファイルをプロジェクトに追加します。

    - SiteColumnProjectWizard

    - SiteColumnWizardModel

    - ProjectSigningManager

    - CommandIds

8. **[ProjectTemplateWizard]** プロジェクト ノードのショートカット メニューを開き、 **[参照の追加]** をクリックします。

9. **[アセンブリ]** ノードを展開し、 **[拡張機能]** ノードをクリックして、次のアセンブリの横にあるチェック ボックスをオンにします。

    - EnvDTE

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.Shell.Interop.10.0

    - Microsoft.VisualStudio.Shell.Interop.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

10. **[OK]** をクリックして、アセンブリをプロジェクトに追加します。

11. **ソリューション エクスプローラー** で、**ProjectTemplateWizard** プロジェクトの **[参照設定]** フォルダーの下の **[EnvDTE]** をクリックします。

12. **[プロパティ]** ウィンドウで、"**相互運用型の埋め込み**" プロパティの値を **False** に変更します。

13. Visual Basic プロジェクトを開発している場合は、**プロジェクト デザイナー** を使用して ProjectTemplateWizard 名前空間をプロジェクトにインポートします。

     詳細については、「[方法: インポートした名前空間を追加または削除する (Visual Basic)](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)」を参照してください。

#### <a name="to-configure-the-sharepointcommands-project"></a>SharePointcommands プロジェクトを構成するには

1. **ソリューション エクスプローラー** で、 **[SharePointCommands]** プロジェクト ノードをクリックします。

2. メニュー バーで **[プロジェクト]** 、 **[既存項目の追加]** の順にクリックします。

3. **[既存項目の追加]** ダイアログ ボックスで、ProjectTemplateWizard プロジェクトのコード ファイルが格納されているフォルダーを参照し、**CommandIds** コード ファイルを選択します。

4. **[追加]** ボタンの横にある矢印をクリックし、表示されるメニューの **[リンクとして追加]** オプションをクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、**SharePointCommands** プロジェクトにリンクとしてコード ファイルが追加されます。 コード ファイルそのものは **ProjectTemplateWizard** プロジェクトに存在しますが、そのファイル内のコードは **SharePointCommands** プロジェクトでもコンパイルされます。

5. **SharePointCommands** プロジェクトに、Commands という別のコード ファイルを追加します。

6. SharePointCommands プロジェクトを選択し、メニュー バーで **[プロジェクト]**  >  **[参照の追加]** の順にクリックします。

7. **[アセンブリ]** ノードを展開し、 **[拡張機能]** ノードをクリックして、次のアセンブリの横にあるチェック ボックスをオンにします。

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

8. **[OK]** をクリックして、アセンブリをプロジェクトに追加します。

## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>ウィザード モデル、署名マネージャー、SharePoint コマンド ID を作成する
 ProjectTemplateWizard プロジェクトにコードを追加して、サンプルの次のコンポーネントを実装します。

- SharePoint コマンド ID。 これらは、ウィザードによって使用される SharePoint コマンドを識別する文字列です。 このチュートリアルの後半で、SharePointCommands プロジェクトにコードを追加してコマンドを実装します。

- ウィザード データ モデル。

- プロジェクト署名マネージャー。

  これらのコンポーネントの詳細については、「[ウィザードのコンポーネントについて](#understand-the-wizard-components)」を参照してください。

#### <a name="to-define-the-sharepoint-command-ids"></a>SharePoint コマンド ID を定義するには

1. ProjectTemplateWizard プロジェクトで、CommandIds コード ファイルを開き、このファイルの内容全体を次のコードに置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs" id="Snippet5":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb" id="Snippet5":::

#### <a name="to-create-the-wizard-model"></a>ウィザード モデルを作成するには

1. SiteColumnWizardModel コード ファイルを開き、このファイルの内容全体を次のコードに置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb" id="Snippet6":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs" id="Snippet6":::

#### <a name="to-create-the-project-signing-manager"></a>プロジェクト署名マネージャーを作成するには

1. ProjectSigningManager コード ファイルを開き、このファイルの内容全体を次のコードに置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb" id="Snippet8":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs" id="Snippet8":::

## <a name="create-the-wizard-ui"></a>ウィザード UI を作成する
 ウィザード ウィンドウの UI と、ウィザード ページの UI を提供する 2 つのユーザー コントロールを定義する XAML を追加し、ウィンドウとユーザー コントロールの動作を定義するコードを追加します。 作成するウィザードは、Visual Studio の SharePoint プロジェクト用の組み込みウィザードに似ています。

> [!NOTE]
> 以降の手順では、プロジェクトに XAML またはコードを追加した後で、いくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

#### <a name="to-create-the-wizard-window-ui"></a>ウィザード ウィンドウの UI を作成するには

1. ProjectTemplateWizard プロジェクトで、WizardWindow.xaml ファイルのショートカット メニューを開き、 **[開く]** をクリックしてウィンドウをデザイナーで開きます。

2. デザイナーの XAML ビューで、現在の XAML を次の XAML に置き換えます。 この XAML は、見出しを含む UI、ウィザード ページが含まれる <xref:System.Windows.Controls.Grid>、およびウィンドウの下部に示されるナビゲーション ボタンを定義します。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml" id="Snippet10":::

    > [!NOTE]
    > この XAML で作成するウィンドウは <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基底クラスから派生します。 カスタムの WPF ダイアログ ボックスを Visual Studio に追加する場合は、ダイアログ ボックスをこのクラスから派生し、スタイルを他の Visual Studio ダイアログ ボックスと一貫させ、発生する可能性のあるモーダル ダイアログの問題を回避することをお勧めします。 詳細については、「[モーダル ダイアログ ボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

3. Visual Basic プロジェクトを開発している場合は、`Window` 要素の `x:Class` 属性の `WizardWindow` クラス名から `ProjectTemplateWizard` 名前空間を削除します。 この要素は XAML の 1 行目にあります。 変更後の 1 行目は次の例のようになります。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. WizardWindow.xaml ファイルの分離コード ファイルを開きます。

5. このファイルの内容を、ファイルの先頭の `using` 宣言を除いて、次のコードに置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb" id="Snippet4":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs" id="Snippet4":::

#### <a name="to-create-the-first-wizard-page-ui"></a>1 つ目のウィザード ページの UI を作成するには

1. ProjectTemplateWizard プロジェクトで、Page1.xaml ファイルのショートカット メニューを開き、 **[開く]** をクリックしてユーザー コントロールをデザイナーで開きます。

2. デザイナーの XAML ビューで、現在の XAML を次の XAML に置き換えます。 この XAML で定義している UI には、ユーザーがデバッグに使用するローカル サイトの URL を入力できるテキスト ボックスが含まれます。 この UI には、ユーザーがプロジェクトをサンドボックス化するかどうかを指定できるオプション ボタンも含まれます。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml" id="Snippet11":::

3. Visual Basic プロジェクトを開発している場合は、`ProjectTemplateWizard` 要素の `Page1` 属性の `x:Class` クラス名から `UserControl` 名前空間を削除します。 これは XAML の 1 行目にあります。 変更後の 1 行目は次のようになります。

    ```xml
    <UserControl x:Class="Page1"
    ```

4. Page1.xaml ファイルの内容を、ファイルの先頭にある `using` 宣言を除いて、次のコードに置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs" id="Snippet2":::

#### <a name="to-create-the-second-wizard-page-ui"></a>2 つ目のウィザード ページの UI を作成するには

1. ProjectTemplateWizard プロジェクトで、Page2.xaml ファイルのショートカット メニューを開き、 **[開く]** をクリックします。

     ユーザー コントロールがデザイナーで開きます。

2. XAML ビューで、現在の XAML を次の XAML に置き換えます。 この XAML は、サイト内の列の基本型を選択するためのドロップダウン リスト、ギャラリーでサイト内の列を表示する組み込みまたはカスタムのグループを指定するためのコンボ ボックス、およびサイト内の列の名前を指定するためのボックスが含まれる UI を定義します。

     :::code language="xml" source="../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml" id="Snippet12":::

3. Visual Basic プロジェクトを開発している場合は、`ProjectTemplateWizard` 要素の `Page2` 属性の `x:Class` クラス名から `UserControl` 名前空間を削除します。 これは XAML の 1 行目にあります。 変更後の 1 行目は次のようになります。

    ```xml
    <UserControl x:Class="Page2"
    ```

4. Page2.xaml ファイルの分離コード ファイルの内容を、ファイルの先頭にある `using` 宣言を除いて、次のコードに置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs" id="Snippet3":::

## <a name="implement-the-wizard"></a>ウィザードを実装する
 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装することで、ウィザードの主要機能を定義します。 このインターフェイスは、ウィザードの起動および終了時と、ウィザードの実行中の特定のタイミングで Visual Studio によって呼び出されるメソッドを定義します。

#### <a name="to-implement-the-wizard"></a>ウィザードを実装するには

1. ProjectTemplateWizard プロジェクトで、SiteColumnProjectWizard コード ファイルを開きます。

2. このファイルの内容全体を次のコードで置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb" id="Snippet7":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs" id="Snippet7":::

## <a name="create-the-sharepoint-commands"></a>SharePoint コマンドを作成する
 SharePoint サーバー オブジェクト モデルを呼び出す 2 つのカスタム コマンドを作成します。 一方のコマンドは、ウィザードでユーザーが入力するサイトの URL が有効かどうかを判断します。 もう一方のコマンドは、指定した SharePoint サイトからすべてのフィールドの型を取得して、ユーザーが新しいサイト内の列の基本として使用するフィールドの型を選択できるようにします。

#### <a name="to-define-the-sharepoint-commands"></a>SharePoint コマンドを定義するには

1. **SharePointCommands** プロジェクトの Commands コード ファイルを開きます。

2. このファイルの内容全体を次のコードで置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb" id="Snippet9":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs" id="Snippet9":::

## <a name="checkpoint"></a>Checkpoint
 この段階で、ウィザードに必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、プロジェクトをビルドして確認してください。

#### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="removing-the-keysnk-file-from-the-project-template"></a>プロジェクト テンプレートからの key.snk ファイルの削除
 [「チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (パート 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md))」では、作成したプロジェクトテンプレートに、各サイト列プロジェクトインスタンスの署名に使用されるキー .snk ファイルが含まれています。 ウィザードでプロジェクトごとに新しい key.snk ファイルが生成されるようになったため、この key.snk ファイルはもう必要ありません。 プロジェクト テンプレートから key.snk ファイルを削除し、このファイルへの参照を削除します。

#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>プロジェクト テンプレートから key.snk ファイルを削除するには

1. **ソリューション エクスプローラー** で、 **[SiteColumnProjectTemplate]** ノードの下の **key.snk** ファイルのショートカット メニューを開き、 **[削除]** をクリックします。

2. 表示される確認のダイアログ ボックスで、**[OK]** をクリックします。

3. **[SiteColumnProjectTemplate]** ノードの下の SiteColumnProjectTemplate.vstemplate ファイルを開き、そのファイルから次の要素を削除します。

    ```xml
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
    ```

4. ファイルを保存して閉じます。

5. **[SiteColumnProjectTemplate]** ノードの下の ProjectTemplate.csproj または ProjectTemplate.vbproj ファイルを開き、そのファイルから次の `PropertyGroup` 要素を削除します。

    ```xml
    <PropertyGroup>
      <SignAssembly>true</SignAssembly>
      <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
    </PropertyGroup>
    ```

6. 次の `None` 要素を削除します。

    ```xml
    <None Include="key.snk" />
    ```

7. ファイルを保存して閉じます。

## <a name="associating-the-wizard-with-the-project-template"></a>ウィザードとプロジェクト テンプレートの関連付け
 ウィザードの実装が済んだので、ウィザードと **Site Column** プロジェクト テンプレートを関連付ける必要があります。 これを行うために必要となる手順は次の 3 つです。

1. ウィザード アセンブリに厳密な名前で署名します。

2. ウィザード アセンブリの公開キー トークンを取得します。

3. **Site Column** プロジェクト テンプレートの .vstemplate ファイルに、ウィザード アセンブリへの参照を追加します。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>ウィザード アセンブリに厳密な名前で署名するには

1. **ソリューション エクスプローラー** で、**ProjectTemplateWizard** プロジェクトのショートカット メニューを開き、 **[プロパティ]** をクリックします。

2. **[署名]** タブの **[アセンブリの署名]** チェック ボックスをオンにします。

3. **[厳密な名前のキー ファイルを選択してください]** ボックスの一覧で **\<New...>** を選択します。

4. **[厳密な名前キーの作成]** ダイアログ ボックスで、新しいキー ファイルの名前を入力し、 **[キー ファイルをパスワードで保護する]** チェック ボックスをオフにして、 **[OK]** をクリックします。

5. **ProjectTemplateWizard** プロジェクトのショートカット メニューを開き、 **[ビルド]** をクリックして ProjectTemplateWizard.dll ファイルを作成します。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>ウィザード アセンブリの公開キー トークンを取得するには

1. **[スタート]** メニューで **[すべてのプログラム]** 、 **[Microsoft Visual Studio]** 、 **[Visual Studio Tools]** の順にポイントし、 **[開発者コマンド プロンプト]** をクリックします。

     Visual Studio コマンド プロンプト ウィンドウが開きます。

2. 次のコマンドを実行します。*PathToWizardAssembly* は、開発コンピューター上で ProjectTemplateWizard プロジェクト用にビルドされた ProjectTemplateWizard.dll アセンブリへの完全パスで置き換えます。

    ```cmd
    sn.exe -T PathToWizardAssembly
    ```

     ProjectTemplateWizard.dll アセンブリに対する公開キー トークンが Visual Studio コマンド プロンプト ウィンドウに記述されます。

3. Visual Studio コマンド プロンプト ウィンドウは開いたままにします。 次の手順の間に、公開キー トークンが必要になります。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>.vstemplate ファイルにウィザード アセンブリへの参照を追加するには

1. **ソリューション エクスプローラー** で、 **[SiteColumnProjectTemplate]** プロジェクト ノードを展開し、SiteColumnProjectTemplate.vstemplate ファイルを開きます。

2. ファイルの末尾の近くで、次の `WizardExtension` 要素を `</TemplateContent>` タグと `</VSTemplate>` タグの間に追加します。 `PublicKeyToken` 属性の "*トークン*" の値は、前の手順で取得した公開キー トークンで置き換えます。

    ```xml
    <WizardExtension>
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>
    </WizardExtension>
    ```

     `WizardExtension` 要素の詳細については、[WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md) に関するページを参照してください。

3. ファイルを保存して閉じます。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>プロジェクト テンプレートの Elements.xml ファイルに置き換え可能パラメーターを追加する
 複数の置き換え可能パラメーターを、SiteColumnProjectTemplate プロジェクトの *Elements.xml* ファイルに追加します。 これらのパラメーターは、前に定義した `RunStarted` クラスの `SiteColumnProjectWizard` メソッドで初期化されます。 ユーザーが Site Column プロジェクトを作成すると、Visual Studio によって自動的に、新しいプロジェクト項目の *Elements.xml* ファイル内のこれらのパラメーターが、ウィザードでユーザーが指定した値に置き換えられます。

 置き換え可能パラメーターはトークンであり、先頭と末尾にはドル記号 ($) が付いています。 独自の置き換え可能パラメーターを定義するだけでなく、SharePoint プロジェクト システムによって定義されて初期化される組み込みパラメーターを使用することもできます。 詳細については、「[置き換え可能パラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>置き換え可能パラメーターを Elements.xml ファイルに追加するには

1. SiteColumnProjectTemplate プロジェクトで、*Elements.xml* ファイルの内容を次の XML に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
             Name="$fieldname$"
             DisplayName="$fieldname$"
             Type="$selectedfieldtype$"
             Group="$selectedgrouptype$">
      </Field>
    </Elements>
    ```

     新しい XML では、`Name`、`DisplayName`、`Type`、`Group` の各属性の値がカスタムの置き換え可能パラメーターに変更されます。

2. ファイルを保存して閉じます。

## <a name="add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加する
 Site Column プロジェクト テンプレートが含まれる VSIX パッケージと共にウィザードを配置するには、ウィザード プロジェクトと SharePoint コマンド プロジェクトへの参照を VSIX プロジェクトの source.extension.vsixmanifest ファイルに追加します。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加するには

1. **ソリューション エクスプローラー** に表示されている **SiteColumnProjectItem** プロジェクトで、**source.extension.vsixmanifest** ファイルのショートカット メニューを開き、 **[開く]** をクリックします。

     Visual Studio によってマニフェスト エディターでファイルが開きます。

2. エディターの **[アセット]** タブで、 **[新規作成]** をクリックします。

     **[新しいアセットの追加]** ダイアログ ボックスが開きます。

3. **[種類]** ボックスの一覧で、 **[Microsoft.VisualStudio.Assembly]** を選択します。

4. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

5. **[プロジェクト]** ボックスの一覧で、 **[ProjectTemplateWizard]** を選択し、 **[OK]** をクリックします。

6. エディターの **[アセット]** タブで、もう一度 **[新規作成]** をクリックします。

     **[新しいアセットの追加]** ダイアログ ボックスが開きます。

7. **[種類]** ボックスの一覧に「**SharePoint.Commands.v4**」と入力します。

8. **[ソース]** ボックスの一覧で、 **[現在のソリューション内のプロジェクト]** を選択します。

9. **[プロジェクト]** ボックスの一覧で **SharePointCommands** プロジェクトを選択し、 **[OK]** をクリックします。

10. メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** の順に選択し、ソリューションがエラーなしでビルドされることを確認します。

## <a name="test-the-wizard"></a>ウィザードをテストする
 これで、ウィザードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで SiteColumnProjectItem ソリューションのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで、Site Column プロジェクトのウィザードをテストします。 最後に、プロジェクトをビルドして実行し、サイト内の列が正常に機能することを確認します。

#### <a name="to-start-debugging-the-solution"></a>ソリューションのデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、SiteColumnProjectItem ソリューションを開きます。

2. ProjectTemplateWizard プロジェクトで、SiteColumnProjectWizard コード ファイルを開き、`RunStarted` メソッド内のコードの 1 行目にブレークポイントを追加します。

3. メニュー バーで **[デバッグ]**  >  **[例外]** の順に選択します。

4. **[例外]** ダイアログ ボックスで、 **[Common Language Runtime Exceptions]** の **[スローされるとき]** チェック ボックスと **[ユーザーにハンドルされていないとき]** チェック ボックスがオフになっていることを確認して、 **[OK]** をクリックします。

5. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[デバッグ開始]** の順に選択して、デバッグを開始します。

     Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-wizard-in-visual-studio"></a>Visual Studio でウィザードをテストするには

1. Visual Studio の実験用インスタンスのメニュー バーで **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

2. (プロジェクト テンプレートがサポートする言語に応じて) **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[SharePoint]** ノードを展開して、 **[2010]** ノードをクリックします。

3. プロジェクト テンプレートの一覧で **[サイト列]** を選択し、プロジェクトに **SiteColumnWizardTest** という名前を付けて、 **[OK]** をクリックします。

4. Visual Studio のもう一方のインスタンスで、先ほど `RunStarted` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

5. **F5** キーを押すかメニュー バーで **[デバッグ]**  >  **[続行]** の順にクリックして、プロジェクトのデバッグを続行します。

6. **SharePoint カスタマイズ ウィザード** で、デバッグに使用するサイトの URL を入力し、 **[次へ]** をクリックします。

7. **SharePoint カスタマイズ ウィザード** の 2 つ目のページで、次のように選択します。

   - **[種類]** ボックスの一覧で **[ブール型]** を選択します。

   - **[グループ]** ボックスの一覧で **[Custom Yes/No Columns]** を選択します。

   - **[名前]** ボックスに「**My Yes/No Column**」と入力し、 **[完了]** をクリックします。

     **ソリューション エクスプローラー** に、新しいプロジェクトが開き、そのプロジェクトに含まれる **Field1** というプロジェクト項目が表示されます。また、Visual Studio エディターに、プロジェクトの *Elements.xml* ファイルが開きます。

8. *Elements.xml* にウィザードで指定した値が含まれることを確認します。

#### <a name="to-test-the-site-column-in-sharepoint"></a>SharePoint でサイト内の列をテストするには

1. Visual Studio の実験用インスタンスで、**F5** キーを押します。

     サイト列がパッケージ化され、プロジェクトの "**サイト URL**" プロパティで指定された SharePoint サイトに配置されます。 Web ブラウザーには、このサイトの既定のページが表示されます。

    > [!NOTE]
    > **[スクリプト デバッグが無効]** ダイアログ ボックスが表示された場合は、 **[はい]** をクリックしてプロジェクトをデバッグします。

2. **[サイトの操作]** メニューの **[サイトの設定]** をクリックします。

3. [サイトの設定] ページの **[ギャラリー]** で **[サイト列]** リンクをクリックします。

4. サイト列の一覧で、 **[Custom Yes/No Columns]** グループに **[My Yes/No Column]** という列が含まれることを確認して、Web ブラウザーを閉じます。

## <a name="clean-up-the-development-computer"></a>開発コンピューターをクリーンアップする
 プロジェクト項目のテストが終わったら、プロジェクト テンプレートを Visual Studio の実験用インスタンスから削除します。

#### <a name="to-clean-up-the-development-computer"></a>開発コンピューターをクリーンアップするには

1. Visual Studio の実験用インスタンスのメニュー バーで、 **[ツール]**  >  **[拡張機能と更新プログラム]** の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で **[サイト列]** を選択し、 **[アンインストール]** をクリックします。

3. 表示されるダイアログ ボックスで、 **[はい]** をクリックして拡張機能のアンインストールを確定し、 **[今すぐ再起動]** をクリックしてアンインストールを完了します。

4. Visual Studio の実験用インスタンスと、CustomActionProjectItem ソリューションが開いているインスタンスの両方を閉じます。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能を配置する方法の詳細については、「[Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [チュートリアル: プロジェクト テンプレートを使用してサイト列プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [カスタムの SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートの作成](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
