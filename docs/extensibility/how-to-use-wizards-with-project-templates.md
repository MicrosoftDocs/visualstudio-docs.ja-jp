---
title: '方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する'
description: Visual Studio SDK で IWizard インターフェイスを使用する方法について説明します。これにより、ユーザーがテンプレートからプロジェクトを作成するときに、カスタム コードを実行できるようになります。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- project templates [Visual Studio], wizards
- Visual Studio templates, wizards
- wizards [Visual Studio], project templates
- templates [Visual Studio], wizards
- IWizard interface
ms.assetid: 47ee26cf-67b7-4ff1-8a9d-ab11a725405c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 41290f946c198ed854cad9a7eb2af088f6fe228a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082284"
---
# <a name="how-to-use-wizards-with-project-templates"></a>方法: プロジェクト テンプレートを組み合わせたウィザードを使用する

Visual Studio には、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスが用意されています。このインターフェイスを実装すると、ユーザーがテンプレートからプロジェクトを作成する際にカスタム コードを実行できるようになります。

プロジェクト テンプレートのカスタマイズを使用すると、ユーザー入力を収集してテンプレートをカスタマイズしたり、テンプレートにファイルを追加したり、プロジェクトで許可されているその他のアクションを実行したりするカスタム UI を表示できます。

<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイス メソッドは、プロジェクトの作成中にさまざまな時点で呼び出されます。プロジェクトの作成は、ユーザーが **[新しいプロジェクト]** ダイアログ ボックスの **[OK]** をクリックすると同時に開始されます。 インターフェイスの各メソッドには、そのメソッドが呼び出される時点を表す名前が付けられます。 たとえば、プロジェクトの作成の開始直後に、Visual Studio によって <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> が呼び出されます。この時点が、ユーザー入力を収集するためのカスタム コードの記述に適した場所になります。

## <a name="create-a-project-template-project-with-a-vsix-project"></a>VSIX プロジェクトを使用してプロジェクト テンプレート プロジェクトを作成する

カスタム テンプレートの作成は、Visual Studio SDK の一部であるプロジェクト テンプレート プロジェクトから始めます。 この手順では、C# プロジェクト テンプレート プロジェクトを使用しますが、Visual Basic プロジェクト テンプレート プロジェクトもあります。 次に、プロジェクト テンプレート プロジェクトを含むソリューションに VSIX プロジェクトを追加します。

1. C# プロジェクト テンプレート プロジェクトを作成します (Visual Studio で、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** を選択し、「プロジェクト テンプレート」を検索します)。 **MyProjectTemplate** と名前を付けます。

   > [!NOTE]
   > Visual Studio SDK のインストールを求められる場合があります。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

2. プロジェクト テンプレート プロジェクトと同じソリューションに新しい VSIX プロジェクトを追加します (**ソリューション エクスプローラー** で、ソリューション ノードを選択し、右クリックして、 **[追加]**  >  **[新しいプロジェクト]** を選択し、「vsix」を検索します)。 **MyProjectWizard** と名前を付けます。

3. VSIX プロジェクトをスタートアップ プロジェクトとして設定します。 **ソリューション エクスプローラー** で VSIX プロジェクト ノードを選択し、右クリックして、 **[スタートアップ プロジェクトに設定]** を選択します。

4. テンプレート プロジェクトを VSIX プロジェクトのアセットとして追加します。 **ソリューション エクスプローラー** の VSIX プロジェクト ノードで、*source.extension.vsixmanifest* ファイルを見つけます。 それをダブルクリックしてマニフェスト エディターで開きます。

5. マニフェスト エディターで、ウィンドウの左側にある **[アセット]** タブを選択します。

6. **[アセット]** タブで、 **[新規]** を選択します。 **[新しい資産の追加]** ウィンドウの [種類] フィールドで **[Microsoft.VisualStudio.ProjectTemplate]** を選択します。 **[ソース]** フィールドで、 **[現在のソリューション内のプロジェクト]** を選択します。 **[プロジェクト]** フィールドで、 **[MyProjectTemplate]** を選択します。 次に、 **[OK]** をクリックします

7. ソリューションをビルドし、デバッグを開始します。 Visual Studio の 2 番目のインスタンスが表示されます。 (これには数分かかることがあります)。

8. Visual Studio の 2 番目のインスタンスで、新しいテンプレートを使用して新しいプロジェクトを作成してみてください ( **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** を選択し、「myproject」を検索します)。 **Class1** という名前のクラスがある新しいプロジェクトが表示されます。 これでカスタム プロジェクト テンプレートの作成は完了です。 すぐにデバッグを停止してください。

## <a name="create-a-custom-template-wizard"></a>カスタム テンプレート ウィザードを作成する

この手順では、プロジェクトを作成する前に Windows フォームを開くカスタム ウィザードを作成する方法について説明します。 このフォームを使用すると、ユーザーは、プロジェクトの作成時にソース コードに追加されるカスタム パラメーター値を追加できます。

1. アセンブリを作成できるように VSIX プロジェクトを設定します。

2. **ソリューション エクスプローラー** で VSIX プロジェクト ノードを選択します。 **ソリューション エクスプローラー** の下に **プロパティ** ウィンドウが表示されます。 そうでない場合は、 **[表示]**  >  **[プロパティ ウィンドウ]** を選択するか、**F4** キーを押します。 **プロパティ** ウィンドウでは、次のフィールドに `true` を選択します。

   - **[Include Assembly In VSIX Container]\(VSIX コンテナーにアセンブリを含める\)**

   - **[Include Debug Symbols In VSIX Container]\(VSIX コンテナーにデバッグ シンボルを含める\)**

   - **[Include Debug Symbols In Local VSIX Deployment]\(ローカルの VSIX 配置にデバッグ シンボルを含める\)**

3. アセンブリをアセットとして VSIX プロジェクトに追加します。 *source.extension.vsixmanifest* ファイルを開き、 **[資産]** タブを選択します。 **[新しい資産の追加]** ウィンドウで、 **[種類]** に **[Microsoft.VisualStudio.Assembly]** を選択し、 **[ソース]** に **[現在のソリューション内のプロジェクト]** を選択し、 **[プロジェクト]** に **[MyProjectWizard]** を選択します。

4. 以下の参照を VSIX プロジェクトに追加します (**ソリューション エクスプローラー** の VSIX プロジェクト ノードで、 **[参照]** を選択し、右クリックして、 **[参照の追加]** を選択します)。 **[参照の追加]** ダイアログの **[フレームワーク]** タブで、**System.Windows Forms** アセンブリを見つけて選択します。 また、**System** と **System.Drawing** の各アセンブリを見つけて選択します。 次に、 **[拡張機能]** タブを選択します。**EnvDTE** アセンブリを見つけて選択します。 また、**Microsoft.VisualStudio.TemplateWizardInterface** アセンブリを見つけて選択します。 **[OK]** をクリックします。

5. ウィザード実装のクラスを VSIX プロジェクトに追加します (**ソリューション エクスプローラー** で、VSIX プロジェクト ノードを右クリックし、 **[追加]** 、 **[新しい項目]** 、 **[クラス]** の順に選択します)。クラスに **WizardImplementation** と名前を付けます。

6. *WizardImplementationClass.cs* ファイルのコードを次のコードに置き換えます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.TemplateWizard;
   using System.Windows.Forms;
   using EnvDTE;

   namespace MyProjectWizard
   {
       public class WizardImplementation:IWizard
       {
           private UserInputForm inputForm;
           private string customMessage;

           // This method is called before opening any item that
           // has the OpenInEditor attribute.
           public void BeforeOpeningFile(ProjectItem projectItem)
           {
           }

           public void ProjectFinishedGenerating(Project project)
           {
           }

           // This method is only called for item templates,
           // not for project templates.
           public void ProjectItemFinishedGenerating(ProjectItem
               projectItem)
           {
           }

           // This method is called after the project is created.
           public void RunFinished()
           {
           }

           public void RunStarted(object automationObject,
               Dictionary<string, string> replacementsDictionary,
               WizardRunKind runKind, object[] customParams)
           {
               try
               {
                   // Display a form to the user. The form collects
                   // input for the custom message.
                   inputForm = new UserInputForm();
                   inputForm.ShowDialog();

                   customMessage = UserInputForm.CustomMessage;

                   // Add custom parameters.
                   replacementsDictionary.Add("$custommessage$",
                       customMessage);
               }
               catch (Exception ex)
               {
                   MessageBox.Show(ex.ToString());
               }
           }

           // This method is only called for item templates,
           // not for project templates.
           public bool ShouldAddProjectItem(string filePath)
           {
               return true;
           }
       }
   }
   ```

    このコードで参照されている **UserInputForm** は、後で実装されます。

    `WizardImplementation` クラスには、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> のすべてのメンバーに対するメソッドの実装が含まれています。 この例では、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドだけがタスクを実行します。 他のすべてのメソッドは、何もしないか、`true` を返します。

    <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドは、次の 4 つのパラメーターを受け取ります。

   - <xref:System.Object> パラメーター。プロジェクトをカスタマイズできるように、ルートの <xref:EnvDTE._DTE> オブジェクトにキャストできます。

   - <xref:System.Collections.Generic.Dictionary%602> パラメーター。テンプレートで定義済みのすべてのパラメーターのコレクションが含まれます。 テンプレート パラメーターの詳細については、「[テンプレート パラメーター](../ide/template-parameters.md)」を参照してください。

   - <xref:Microsoft.VisualStudio.TemplateWizard.WizardRunKind> パラメーター。使用されているテンプレートの種類に関する情報が含まれます。

   - <xref:System.Object> 配列。Visual Studio によってウィザードに渡される一連のパラメーターが格納されます。

     この例では、ユーザー入力フォームから <xref:System.Collections.Generic.Dictionary%602> パラメーターにパラメーター値を追加します。 プロジェクト内の `$custommessage$` パラメーターのすべてのインスタンスは、ユーザーが入力したテキストと置き換えられます。

7. 次に、**UserInputForm** を作成します。 *WizardImplementation.cs* ファイルで、`WizardImplementation` クラスの末尾の後に次のコードを追加します。

   ```csharp
   public partial class UserInputForm : Form
       {
           private static string customMessage;
           private TextBox textBox1;
           private Button button1;

           public UserInputForm()
           {
               this.Size = new System.Drawing.Size(155, 265);

               button1 = new Button();
               button1.Location = new System.Drawing.Point(90, 25);
               button1.Size = new System.Drawing.Size(50, 25);
               button1.Click += button1_Click;
               this.Controls.Add(button1);

               textBox1 = new TextBox();
               textBox1.Location = new System.Drawing.Point(10, 25);
               textBox1.Size = new System.Drawing.Size(70, 20);
               this.Controls.Add(textBox1);
           }
           public static string CustomMessage
           {
               get
               {
                   return customMessage;
               }
               set
               {
                   customMessage = value;
               }
           }
           private void button1_Click(object sender, EventArgs e)
           {
               customMessage = textBox1.Text;
               this.Close();
           }
       }
   ```

    ユーザー入力フォームには、カスタム パラメーターを入力するための簡単なフォームが用意されています。 このフォームには、`textBox1` という名前のテキスト ボックスおよび `button1` という名前のボタンがあります。 このボタンをクリックすると、テキスト ボックスのテキストが `customMessage` パラメーターに格納されます。

## <a name="connect-the-wizard-to-the-custom-template"></a>ウィザードをカスタム テンプレートに接続する

カスタム プロジェクト テンプレートでカスタム ウィザードを使用するには、ウィザード アセンブリに署名し、カスタム プロジェクト テンプレートにいくつかの行を追加して、新しいプロジェクトが作成されたときにウィザードの実装がどこにあるかを把握できるようにする必要があります。

1. アセンブリに署名します。 **ソリューション エクスプローラー** で、VSIX プロジェクトを選択し、右クリックして、 **[プロジェクトのプロパティ]** を選択します。

2. **[プロジェクトのプロパティ]** ウィンドウで、 **[署名]** タブを選択します。 **[署名]** タブで、 **[アセンブリの署名]** を確認します。 **[厳密な名前のキー ファイルを選択してください]** フィールドで **[\<New>]** を選択します。 **[厳密な名前キーの作成]** ウィンドウの **[キー ファイル名]** フィールドに「**key.snk**」と入力します。 **[キーファイルをパスワードで保護する]** フィールドをオフにします。

3. **ソリューション エクスプローラー** で、VSIX プロジェクトを選択し、 **[プロパティ]** ウィンドウを見つけます。

4. **[Copy Build Output to Output Directory]\(ビルド出力を出力ディレクトリにコピーする\)** フィールドを **[true]** に設定します。 これにより、ソリューションのリビルド時にアセンブリが出力ディレクトリにコピーされるようになります。 これはまだ `.vsix` ファイルに含まれています。 署名キーを調べるには、アセンブリを確認する必要があります。

5. ソリューションをリビルドします。

6. これで、MyProjectWizard プロジェクト ディレクトリ ( *\<your disk location>\MyProjectTemplate\MyProjectWizard\key.snk*) 内の key.snk ファイルを見つけられます。 *key.snk* ファイルをコピーします。

7. 出力ディレクトリに移動し、アセンブリ ( *\<your disk location>\MyProjectTemplate/MyProjectWizard\bin\Debug\MyProjectWizard.dll*) を見つけます。 *key.snk* ファイルをここに貼り付けます (これは絶対に必要というわけではありませんが、次の手順が簡単になります)。

8. コマンド ウィンドウを開き、アセンブリが作成されたディレクトリに移動します。

9. *sn.exe* 署名ツールを見つけます。 たとえば、Windows 10 64 ビット オペレーティング システムでは、一般的なパスは次のようになります。

     *C:\Program Files (x86)\Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.6.1 Tools*

     ツールが見つからない場合は、コマンド ウィンドウで **where /R . sn.exe** を実行してみてください。 パスをメモします。

10. *key.snk* ファイルから公開キーを抽出します。 コマンド ウィンドウで、次のように入力します

     **\<location of sn.exe>\sn.exe -p key.snk outfile.key.**

     ディレクトリ名にスペースがある場合は、*sn.exe* のパスを必ず引用符で囲んでください。

11. 出力ファイルから公開キー トークンを取得します。

     **\<location of sn.exe>\sn.exe -t outfile.key.**

     繰り返しになりますが、引用符を忘れないでください。 次のような行が出力に表示されます。

     **公開キー トークンは \<token> です**

     この値を書き留めておきます。

12. カスタム ウィザードへの参照をプロジェクト テンプレートの *.vstemplate* ファイルに追加します。 **ソリューション エクスプローラー** で、*MyProjectTemplate.vstemplate* という名前のファイルを見つけて開きます。 \<TemplateContent> セクションの末尾の後に、次のセクションを追加します。

    ```xml
    <WizardExtension>
        <Assembly>MyProjectWizard, Version=1.0.0.0, Culture=Neutral, PublicKeyToken=token</Assembly>
        <FullClassName>MyProjectWizard.WizardImplementation</FullClassName>
    </WizardExtension>
    ```

     この **MyProjectWizard** はアセンブリの名前であり、**token** は前の手順でコピーしたトークンです。

13. プロジェクト内のすべてのファイルを保存してリビルドします。

## <a name="add-the-custom-parameter-to-the-template"></a>テンプレートにカスタム パラメーターを追加する

この例で、テンプレートとして使用されるプロジェクトには、カスタム ウィザードのユーザー入力フォームに指定されたメッセージが表示されます。

1. **ソリューション エクスプローラー** で、**MyProjectTemplate** プロジェクトに移動し、*Class1.cs* を開きます。

2. アプリケーションの `Main` メソッドに次のコード行を追加します。

   ```csharp
   Console.WriteLine("$custommessage$");
   ```

    `$custommessage$` パラメーターは、プロジェクトをテンプレートから作成する際にユーザー入力フォームに入力したテキストで置き換えられます。

テンプレートにエクスポートされる前の完全なコード ファイルを次に示します。

```csharp
using System;
using System.Collections.Generic;
$if$ ($targetframeworkversion$ >= 3.5)using System.Linq;
$endif$using System.Text;

namespace $safeprojectname$
{
    public class Class1
    {
          static void Main(string[] args)
          {
               Console.WriteLine("$custommessage$");
          }
    }
}
```

## <a name="use-the-custom-wizard"></a>カスタム ウィザードを使用する

これで、テンプレートからプロジェクトを作成し、カスタム ウィザードを使用できるようになりました。

1. ソリューションをリビルドし、デバッグを開始します。 Visual Studio の 2 番目のインスタンスが表示されます。

2. 新しい MyProjectTemplate プロジェクトを作成します ( **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** )。

3. **[新しいプロジェクト]** ダイアログ ボックスで「myproject」を検索してテンプレートを見つけ、名前を入力し、 **[OK]** をクリックします。

     ウィザードのユーザー入力フォームが開きます。

4. カスタム パラメーターの値を入力し、ボタンをクリックします。

     ウィザードのユーザー入力フォームが終了し、プロジェクトがテンプレートから作成されます。

5. **ソリューション エクスプローラー** で、ソース コード ファイルを右クリックし、 **[コードの表示]** をクリックします。

     `$custommessage$` は、ウィザードのユーザー入力フォームに入力されたテキストで置き換えられています。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TemplateWizard.IWizard>
- [テンプレートのカスタマイズ](../ide/customizing-project-and-item-templates.md)
- [WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md)
- [Visual Studio テンプレートの NuGet パッケージ](/nuget/visual-studio-extensibility/visual-studio-templates)
