---
title: FAQ:アドインを VSPackage 拡張機能に変換する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3a01d333-6e31-423f-ae06-5091a4fcb7a9
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc6ed31f96fc2021d0d9e104692f0440cfb78a5e
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433739"
---
# <a name="faq-converting-add-ins-to-vspackage-extensions"></a>FAQ:アドインを VSPackage 拡張機能に変換します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

現在、アドインは非推奨とされます。 新しい Visual Studio 拡張機能をするためには、VSIX 拡張機能を作成する必要があります。 VSIX 拡張機能に Visual Studio アドインを変換する方法についてよく寄せられる質問に対する回答を示します。  
  
> [!WARNING]
> 以降、Visual Studio 2015 では c# および Visual Basic プロジェクトでは、VSIX プロジェクトを使用し、メニュー コマンド、ツール ウィンドウ、および Vspackage の項目テンプレートを追加できます。 詳細については、次を参照してください。 [、Visual Studio 2015 SDK の新](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md)します。  
  
> [!IMPORTANT]
> 多くの場合は、VSPackage プロジェクト項目で VSIX プロジェクトに単に、アドインのコードを転送できます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> メソッドで <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> を呼び出すことで、DTE オートメーション オブジェクトを取得できます。  
>   
> `DTE2 dte = (DTE2)GetService(typeof(DTE));`  
>   
> 詳細については、次を参照してください。 [VSPackage でアドイン コードを実行する方法でしょうか。](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_RunAddin)以下。  
  
## <a name="what-software-do-i-need-to-develop-vsix-extensions"></a>VSIX 拡張機能を開発する必要があるソフトウェアをでしょうか。  
 Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 より詳細な情報については 、[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md) に関する記事を参照してください。  
  
## <a name="wheres-the-extension-documentation"></a>拡張機能のドキュメントにはどこですか。  
 始まり[Visual Studio 拡張機能の開発を始める](../extensibility/starting-to-develop-visual-studio-extensions.md)します。 Msdn VSSDK 拡張機能の開発に関するその他の記事では、以下のいずれかです。  
  
## <a name="can-i-convert-my-add-in-project-to-a-vsix-project"></a>アドイン プロジェクトを VSIX プロジェクトは変換できますか。  
 アドイン プロジェクトは、VSIX プロジェクトで使用されるメカニズムは、アドイン プロジェクトで使用されているのと同じではないために、VSIX プロジェクトに直接変換できません。 VSIX プロジェクト テンプレート、および適切なプロジェクト項目テンプレートに含まれる多く比較的簡単に起動して VSIX 拡張機能として実行されるコード。  
  
## <a name="BKMK_StartDeveloping"></a> VSIX 拡張機能の開発を開始する方法  
 メニュー コマンドを含む VSIX を作成する方法を次に示します。  
  
#### <a name="to-make-a-vsix-extension-that-has-a-menu-command"></a>メニュー コマンドを含む VSIX 拡張機能を作成するには  
  
1. VSIX プロジェクトを作成する。 (**ファイル**、**新規**、**プロジェクト**、または型**プロジェクト**で、**クイック起動**ウィンドウ)。 **新しいプロジェクト** ダイアログ ボックスで、展開**Visual c#/機能拡張**または**Visual Basic/機能拡張**選択**VSIX プロジェクト**)。プロジェクトに名前を**TestExtension**場所を指定するとします。  
  
2. 追加、**カスタム コマンド**プロジェクト項目テンプレート。 (でプロジェクト ノードを右クリックし、**ソリューション エクスプ ローラー**選択**追加/新しい項目の**します。 **新しいプロジェクト**Visual c# または Visual Basic では、選択のいずれかのダイアログ、**拡張**ノード**カスタム コマンド**)。  
  
3. F5 キーを押して、プロジェクトをデバッグ モードでビルドおよび実行します。  
  
     Visual Studio の 2 番目のインスタンスが表示されます。 この 2 番目のインスタンスは実験用インスタンスと呼ばれます。コードの記述に使用する Visual Studio のインスタンスとは設定が異なることがあります。 実験用インスタンスを初めて実行するときには、VS Online にサインインしてテーマとプロファイルを指定するよう求められます。  
  
     **ツール** メニュー (に実験用インスタンス) という名前のボタンを表示する必要があります**マイ コマンド名**します。 このボタンを選択すると、メッセージが表示されます。**TestVSPackagePackage.MenuItemCallback() 内**します。  
  
## <a name="BKMK_RunAddin"></a> VSPackage でアドイン コードを実行する方法はありますか  
 通常、アドイン コードは次の 2 つの方法のどちらかで実行します。  
  
- メニュー コマンドによるトリガー (コードは `IDTCommandTarget.Exec` メソッド内にあります)  
  
- 起動時に自動的に実行 (コードは `OnConnection` イベント ハンドラー内にあります)。  
  
  VSPackage でも同じ操作を実行できます。 コールバック メソッドにアドイン コードを追加する方法を次に示します。  
  
#### <a name="to-implement-a-menu-command-in-a-vspackage"></a>VSPackage にメニュー コマンドを実装するには  
  
1. メニュー コマンドを含む VSPackage を作成します。 (詳細については、次を参照してください[メニュー コマンドを使用して拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)。)。  
  
2. VSPackage の定義が含まれているファイルを開きます。 (C# プロジェクトである<em>\<プロジェクト名 ></em>Package.cs です)。  
  
3. ファイルに次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. `MenuItemCallback` メソッドを見つけます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトを取得するため、<xref:EnvDTE80.DTE2> の呼び出しを追加します。  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. アドインのコードを `IDTCommandTarget.Exec` メソッドに追加します。 たとえばを新しいウィンドウを追加するいくつかのコードをここでは、**出力**ウィンドウと、新しいウィンドウに"Some Text"を出力します。  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));  
       OutputWindow outputWindow = dte.ToolWindows.OutputWindow;  
  
       OutputWindowPane outputWindowPane = outputWindow.OutputWindowPanes.Add("A New Pane");  
       outputWindowPane.OutputString("Some Text");  
   }  
  
   ```  
  
6. このプロジェクトをビルドして実行します。 F5 キーを押すか、選択**開始**上、**デバッグ**ツールバー。 Visual Studio の実験用インスタンスで、**ツール**という名前のボタンがメニューにあります**マイ コマンド名**します。 このボタンは、単語を選択すると**Some Text**に表示する必要があります、**出力**ウィンドウ ペイン。 (を開く必要があります、**出力**ウィンドウ)。  
  
   起動時にコードを実行することもできます。 ただし、VSPackage 拡張機能では通常、この方法はお勧めできません。 Visual Studio の起動時に読み込まれる拡張機能が多すぎると、起動にかかる時間がかなり長くなることがあります。 何らかの条件 (ソリューションが開いているなど) に一致した場合にのみ VSPackage を自動的に読み込むようにしておくことをお勧めします。  
  
   この手順では、ソリューションが開いているときに自動的に読み込まれる VSPackage のアドイン コードを実行する方法を示します。  
  
#### <a name="to-autoload-a-vspackage"></a>VSPackage を自動読み込みさせるには  
  
1. Visual Studio パッケージ プロジェクト項目には、VSIX プロジェクトを作成します。 (これを行う手順については、次を参照してください。 [VSIX 拡張機能の開発を開始する方法でしょうか。](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping)します。 追加するだけで、 **Visual Studio パッケージ**プロジェクト項目の代わりにします)。VSIX プロジェクトに名前を**TestAutoload**します。  
  
2. TestAutoloadPackage.cs を開きます。 パッケージ クラスが宣言されている行を見つけます。  
  
   ```csharp  
   public sealed class <name of your package>Package : Package  
   ```  
  
3. この行の上に、一連の属性が記述されています。 次の属性を追加します。  
  
   ```csharp  
   [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
   ```  
  
4. `Initialize()` メソッド内にブレークポイントを設定し、デバッグを開始します (F5)。  
  
5. この実験用インスタンスで、プロジェクトを開きます。 VSPackage が読み込まれ、ブレークポイントにヒットします。  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> のフィールドを使用して、VSPackage を読み込む他のコンテキストを指定できます。 詳細については、次を参照してください。 [Vspackage の読み込み](../extensibility/loading-vspackages.md)します。  
  
## <a name="how-can-i-get-the-dte-object"></a>DTE オブジェクトは入手するにはどうしたらよいですか?  
 アドインが UI (メニュー コマンド、ツールバー ボタン、ツール ウィンドウなど) を表示しない場合、VSPackage から DTE オートメーション オブジェクトを入手できる限り、コードを変更せずにそのまま使用できます。 次の手順に従います。  
  
#### <a name="to-get-the-dte-object-from-a-vspackage"></a>VSPackage から DTE オブジェクトを取得するには  
  
1. VSIX プロジェクトは Visual Studio パッケージ項目テンプレートを使用して、検索、 <em>\<プロジェクト名 ></em>Package.cs ファイルを検索します。 これは <xref:Microsoft.VisualStudio.Shell.Package> から派生するクラスで、Visual Studio の操作に役立ちます。 この場合、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> を使用して <xref:EnvDTE80.DTE2> オブジェクトを取得します。  
  
2. 次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
3. `Initialize` メソッドを見つけます。 このメソッドは、パッケージ ウィザードで指定したコマンドを処理します。 DTE オブジェクトを取得するため、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> の呼び出しを追加します。  
  
   ```csharp  
   DTE dte = (DTE)GetService(typeof(DTE));  
   ```  
  
   <xref:EnvDTE.DTE> オートメーション オブジェクトを取得したら、プロジェクトに残りのアドイン コードを追加できます。 <xref:EnvDTE80.DTE2> オブジェクトが必要な場合は、同じ操作を実行できます。  
  
## <a name="how-do-i-change-menu-commands-and-toolbar-buttons-in-my-add-in-to-the-vspackage-style"></a>アドインのメニュー コマンドとツールバー ボタンを VSPackage スタイルで変更するにはどうしたらよいですか?  
 VSPackage 拡張機能は、ほとんどのメニュー コマンド、ツールバー、ツールバー ボタン、その他の UI を作成するときに .vsct ファイルを使用します。 **カスタム コマンド**プロジェクト項目テンプレートを使用して、オプションのコマンドを作成する、**ツール**メニュー。 詳細については、次を参照してください。[メニュー コマンドを使用して拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)です。  
  
 .Vsct ファイルの詳細については、次を参照してください。[方法 VSPackages に追加のユーザー インターフェイス要素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)します。 .Vsct ファイルを使用して、メニューのツールバー、およびツールバーのボタンを追加する方法を示したチュートリアルでは、次を参照してください。[拡張メニューとコマンド](../extensibility/extending-menus-and-commands.md)します。  
  
## <a name="how-do-i-add-custom-tool-windows-in-the-vspackage-way"></a>VSPackage を使用してカスタム ツールウィンドウを追加するにはどうしたらよいですか?  
 カスタム ツール ウィンドウのプロジェクト項目テンプレートでは、ツール ウィンドウを作成するオプションを提供します。 このプロジェクト項目テンプレートの詳細については、次を参照してください。[ツール ウィンドウで、拡張機能を作成する](../extensibility/creating-an-extension-with-a-tool-window.md)します。 ツール ウィンドウについては、次を参照してください。[拡張とカスタマイズ ツール Windows](../extensibility/extending-and-customizing-tool-windows.md)と、その下にある情報の記事特に[ツール ウィンドウの追加](../extensibility/adding-a-tool-window.md)します。  
  
## <a name="how-do-i-manage-visual-studio-windows-in-the-vspackage-way"></a>VSPackage を使用して Visual Studio ウィンドウを管理するにはどうしたらよいですか?  
 Visual Studio ウィンドウを管理するアドインの場合、そのアドイン コードは VSPackage で機能します。 たとえば、この手順を管理するコードを追加する方法を示しています。、**タスク一覧**を、 `MenuItemCallback` 、VSPackage のメソッド。  
  
#### <a name="to-insert-window-management-code-from-an-add-in-into-a-vspackage"></a>アドインのウィンドウ管理コードを VSPackage に挿入するには  
  
1. メニュー コマンドを含む VSPackage を作成、 [VSIX 拡張機能の開発を開始する方法でしょうか。](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping)セクション。  
  
2. VSPackage の定義が含まれているファイルを開きます。 (C# プロジェクトである<em>\<プロジェクト名 ></em>Package.cs です)。  
  
3. 次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. `MenuItemCallback` メソッドを見つけます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトを取得するため、<xref:EnvDTE80.DTE2> の呼び出しを追加します。  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. アドインのコードを追加します。 たとえば、新しいタスクを追加するコードをここでは、**タスク一覧**タスクの数を示しから 1 つのタスクを削除します。  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)   
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       TaskList tl = (TaskList)dte.ToolWindows.TaskList;   
       askItem tlItem;   
  
       // Add a couple of tasks to the Task List.   
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 1.",    
           vsTaskPriority.vsTaskPriorityHigh, vsTaskIcon.vsTaskIconUser,   
           true, "", 10, true, true);  
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 2.",   
           vsTaskPriority.vsTaskPriorityLow, vsTaskIcon.vsTaskIconComment, true, "", 20, true,true);  
  
       // List the total number of task list items after adding the new task items.  
       System.Windows.Forms.MessageBox.Show("Task Item 1 description: "+tl.TaskItems.Item(2).Description);  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
  
       // Remove the second task item. The items list in reverse numeric order.   
       System.Windows.Forms.MessageBox.Show("Deleting the second task item");  
       tl.TaskItems.Item(2).Delete();  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
   }  
   ```  
  
## <a name="how-do-i-manage-projects-and-solutions-in-a-vspackage"></a>VSPackage でプロジェクトとソリューションを管理するにはどうしたらよいですか?  
 プロジェクトとソリューションを管理するアドインの場合、そのアドイン コードは VSPackage で機能します。 たとえば、スタートアップ プロジェクトを取得するコードを追加する手順を次に示します。  
  
1. メニュー コマンドを含む VSPackage を作成、 [VSIX 拡張機能の開発を開始する方法でしょうか。](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping)セクション。  
  
2. VSPackage の定義が含まれているファイルを開きます。 (C# プロジェクトである<em>\<プロジェクト名 ></em>Package.cs です)。  
  
3. 次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. `MenuItemCallback` メソッドを見つけます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトを取得するため、<xref:EnvDTE80.DTE2> の呼び出しを追加します。  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. アドインのコードを追加します。 たとえば、次のコードはソリューション内のスタートアップ プロジェクトの名前を取得します。 (このパッケージを実行するときには、マルチプロジェクト ソリューションが開いている必要があります。)  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       SolutionBuild2 sb = (SolutionBuild2)dte.Solution.SolutionBuild;   
       Project startupProj;   
       string msg = "";  
  
       foreach (String item in (Array)sb.StartupProjects)   
       {  
           msg += item;   
       }  
       System.Windows.Forms.MessageBox.Show("Solution startup Project: "+msg);   
       startupProj = dte.Solution.Item(msg);   
       System.Windows.Forms.MessageBox.Show("Full name of solution's startup project: "+"/n"+startupProj.FullName);   
   }  
   ```  
  
## <a name="how-do-i-set-keyboard-shortcuts-in-a-vspackage"></a>VSPackage でキーボード ショートカットを設定するにはどうしたらよいですか?  
 .vsct ファイルの `<KeyBindings>` 要素を使用します。 次の例では、`idCommand1` コマンドのキーボード ショートカットは Alt+A、`idCommand2` コマンドのキーボード ショートカットは Alt+Ctrl+A です。 キー名の構文に注意してください。  
  
```xml  
<KeyBindings>  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand1" editor="guidVSStd97" key1="A" mod1="ALT" />  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand2" editor="guidVSStd97" key1="A" mod1="CONTROL" mod2="ALT" />  
</KeyBindings>  
```  
  
## <a name="how-do-i-handle-automation-events-in-a-vspackage"></a>VSPackage でオートメーション イベントを処理するにはどうしたらよいですか?  
 VSPackage では、アドインと同様の方法でオートメーション イベントを処理します。 `OnItemRenamed` イベントを処理する方法を次のコードに示します。 (この例は、DTE オブジェクトを既に取得していることを前提としています。)  
  
```csharp  
Events2 dteEvents = (Events2)dte.Events;  
dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;   
. . .  
public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)   
{  
    string s = "[Event] Renamed " + oldName + " to " + Path.GetFileName(projItem.get_FileNames(1) + " in project " + projItem.ContainingProject.Name;   
}  
```
