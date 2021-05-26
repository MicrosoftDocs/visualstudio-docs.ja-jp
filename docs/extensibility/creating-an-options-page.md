---
title: オプション ページの作成 | Microsoft Docs
description: プロパティ グリッドを使用してプロパティを確認および設定する簡単な [ツール] - [オプション] ページを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], creating
ms.assetid: 9f4e210c-4b47-4daa-91fa-1c301c4587f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eb94554b4ac1af30d8187a8ab75aa83f65dccc72
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055805"
---
# <a name="create-an-options-page"></a>オプション ページを作成する

このチュートリアルでは、プロパティ グリッドを使用してプロパティを確認および設定する簡単な [ツール] - [オプション] ページを作成します。

 これらのプロパティを設定ファイルに保存したり、設定ファイルから復元したりするには、以下の手順に従った後、「[設定カテゴリを作成する」](../extensibility/creating-a-settings-category.md)をご覧ください。

 MPF には、[ツール] - [オプション] ページの作成に役立つ 2 つのクラス (<xref:Microsoft.VisualStudio.Shell.Package> クラスと <xref:Microsoft.VisualStudio.Shell.DialogPage> クラス) が用意されています。 これらのページのコンテナーを提供する VSPackage を作成するには、`Package` クラスをサブクラス化します。 各 [ツール] - [オプション] ページを作成するには、`DialogPage` クラスから派生させます。

## <a name="prerequisites"></a>必須コンポーネント

 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-tools-options-grid-page"></a>[ツール] - [オプション] のグリッド ページを作成する

 このセクションでは、簡単な [ツール] - [オプション] のプロパティ グリッドを作成します。 このグリッドを使用すると、プロパティの値を表示および変更できます。

### <a name="to-create-the-vsix-project-and-add-a-vspackage"></a>VSIX プロジェクトを作成して VSPackage を追加するには

1. すべての Visual Studio 拡張機能は、拡張機能アセットを格納する VSIX デプロイ プロジェクトから始まります。 `MyToolsOptionsExtension` という名前の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. `MyToolsOptionsPackage` という名前の Visual Studio パッケージ項目テンプレートを追加して、VSPackage を追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C# の項目]**  >  **[機能拡張]** の順にアクセスし、 **[Visual Studio パッケージ]** を選択します。 ダイアログの下部にある **[名前]** フィールドで、ファイル名を `MyToolsOptionsPackage.cs` に変更します。 VSPackage の作成方法の詳細については、「[VSPackage を使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-vspackage.md)」をご覧ください。

### <a name="to-create-the-tools-options-property-grid"></a>[ツール] - [オプション] のプロパティ グリッドを作成するには

1. コード エディターで *MyToolsOptionsPackage* ファイルを開きます。

2. 次の using ステートメントを追加します。

   ```csharp
   using System.ComponentModel;
   ```

3. `OptionPageGrid` クラスを宣言し、<xref:Microsoft.VisualStudio.Shell.DialogPage> から派生させます。

   ```csharp
   public class OptionPageGrid : DialogPage
   {  }
   ```

4. <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> を `VSPackage` クラスに適用して、OptionPageGrid のオプションのカテゴリとオプション ページ名をそのクラスに割り当てます。 結果は以下のようになります。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

5. `OptionInteger` プロパティを `OptionPageGrid` クラスに追加します。

    - <xref:System.ComponentModel.CategoryAttribute?displayProperty=fullName> を適用して、そのプロパティにプロパティ グリッドカテゴリを割り当てます。

    - <xref:System.ComponentModel.DisplayNameAttribute?displayProperty=fullName> を適用して、そのプロパティに名前を割り当てます。

    - <xref:System.ComponentModel.DescriptionAttribute?displayProperty=fullName> を適用して、そのプロパティに説明を割り当てます。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;

        [Category("My Category")]
        [DisplayName("My Integer Option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
    }
    ```

    > [!NOTE]
    > <xref:Microsoft.VisualStudio.Shell.DialogPage> の既定の実装では、適切なコンバーターを持つプロパティ、または適切なコンバーターを持つプロパティに拡張できる構造体または配列であるプロパティがサポートされています。 コンバーターの一覧については、<xref:System.ComponentModel> 名前空間をご覧ください。

6. プロジェクトをビルドし、デバッグを開始します。

7. Visual Studio の実験用インスタンスで、 **[ツール]** メニューの **[オプション]** をクリックします。

     左側のペインに **[My Category]** が表示されます (オプションのカテゴリはアルファベット順に一覧表示されるため、一覧の中ほどにそれが表示されます)。 **[My Category]** を開いてから、 **[My Grid Page]** をクリックします。 右側のペインに、オプションのグリッドが表示されます。 プロパティのカテゴリは **My Options** で、プロパティ名は **My Integer Option** です。 ペインの下部に **My integer option** というプロパティの説明が表示されます。 値を初期値の 256 から別の値に変更します。 **[OK]** をクリックしてから、 **[My Grid Page]** をもう一度開きます。 新しい値が保持されていることがわかります。

     お客様のオプション ページは、Visual Studio の検索ボックスからも使用できます。 IDE の上部付近にある検索ボックスに「**My Category**」と入力すると、 **[My Category] -> [My Grid Page]** が結果に表示されます。

## <a name="create-a-tools-options-custom-page"></a>[ツール] - [オプション] のカスタム ページを作成する

 このセクションでは、カスタム UI を使用して [ツール] - [オプション] ページを作成します。 このページを使用すると、プロパティの値を表示および変更できます。

1. コード エディターで *MyToolsOptionsPackage* ファイルを開きます。

2. 次の using ステートメントを追加します。

    ```csharp
    using System.Windows.Forms;
    ```

3. `OptionPageCustom` クラスを `OptionPageGrid` クラスの直前に追加します。 `DialogPage` から新しいクラスを派生させます。

    ```csharp
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

4. GUID 属性を追加します。 OptionString プロパティを追加します。

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }
    }
    ```

5. 2 つ目の <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> を VSPackage クラスに適用します。 この属性によって、オプションのカテゴリとオプション ページ名がそのクラスに割り当てます。

    ```csharp
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
    [ProvideMenuResource("Menus.ctmenu", 1)]
    [Guid(GuidList.guidMyToolsOptionsPkgString)]
    [ProvideOptionPage(typeof(OptionPageGrid),
        "My Category", "My Grid Page", 0, 0, true)]
    [ProvideOptionPage(typeof(OptionPageCustom),
        "My Category", "My Custom Page", 0, 0, true)]
    public sealed class MyToolsOptionsPackage : Package
    ```

6. MyUserControl という名前の新しい **ユーザー コントロール** をプロジェクトに追加します。

7. **TextBox** コントロールをそのユーザー コントロールに追加します。

     **[プロパティ]** ウィンドウのツール バーで、 **[イベント]** ボタンをクリックしてから、**Leave** イベントをダブルクリックします。 新しいイベント ハンドラーが *MyUserControl.cs* コードに表示されます。

8. パブリックの `OptionsPage` フィールド (`Initialize` メソッド) をコントロール クラスに追加し、イベント ハンドラーを更新して、オプションの値をテキスト ボックスの内容に設定します。

    ```csharp
    public partial class MyUserControl : UserControl
    {
        public MyUserControl()
        {
            InitializeComponent();
        }

        internal OptionPageCustom optionsPage;

        public void Initialize()
        {
            textBox1.Text = optionsPage.OptionString;
        }

        private void textBox1_Leave(object sender, EventArgs e)
        {
            optionsPage.OptionString = textBox1.Text;
        }
    }
    ```

     `optionsPage` フィールドでは、親の `OptionPageCustom` インスタンスへの参照が保持されます。 `Initialize` メソッドによって `OptionString` が **TextBox** に表示されます。 フォーカスが **TextBox** から離れると、イベント ハンドラーによって **TextBox** の現在の値が `OptionString` に書き込まれます。

9. パッケージ コード ファイルで、`OptionPageCustom.Window` プロパティのオーバーライドを `OptionPageCustom` クラスに追加して、`MyUserControl` のインスタンスを作成、初期化して、返します。 このクラスは以下のようになります。

    ```csharp
    [Guid("00000000-0000-0000-0000-000000000000")]
    public class OptionPageCustom : DialogPage
    {
        private string optionValue = "alpha";

        public string OptionString
        {
            get { return optionValue; }
            set { optionValue = value; }
        }

        protected override IWin32Window Window
        {
            get
            {
                MyUserControl page = new MyUserControl();
                page.optionsPage = this;
                page.Initialize();
                return page;
            }
        }
    }
    ```

10. プロジェクトをビルドして実行します。

11. 実験用インスタンスで、 **[ツール]**  >  **[オプション]** の順にクリックします。

12. **[My Category]** 、 **[My Custom Page]** の順に検索します。

13. **OptionString** の値を変更します。 **[OK]** をクリックしてから、 **[My Custom Page]** をもう一度開きます。 新しい値が保持されていることがわかります。

## <a name="access-options"></a>アクセス オプション

 このセクションでは、関連付けられている [ツール] - [オプション] ページをホストする VSPackage からオプションの値を取得します。 同じ手法を使用して、パブリック プロパティの値を取得することもできます。

1. パッケージ コード ファイルで、**OptionInteger** というパブリック プロパティ を **MyToolsOptionsPackage** クラスに追加します。

    ```csharp
    public int OptionInteger
    {
        get
        {
            OptionPageGrid page = (OptionPageGrid)GetDialogPage(typeof(OptionPageGrid));
            return page.OptionInteger;
        }
    }

    ```

     このコードでは、<xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> を呼び出して `OptionPageGrid` インスタンスを作成または取得します。 `OptionPageGrid` では、<xref:Microsoft.VisualStudio.Shell.DialogPage.LoadSettingsFromStorage%2A> を呼び出して、パブリック プロパティであるそのオプションを読み込みます。

2. ここで、**MyToolsOptionsCommand** という名前のカスタム コマンド項目テンプレートを追加して、値を表示します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *MyToolsOptionsCommand.cs* に変更します。

3. *MyToolsOptionsCommand* ファイルで、コマンドの `ShowMessageBox` メソッドの本体を以下に置き換えます。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
        MyToolsOptionsPackage myToolsOptionsPackage = this.package as MyToolsOptionsPackage;
        System.Windows.Forms.MessageBox.Show(string.Format(CultureInfo.CurrentCulture, "OptionInteger: {0}", myToolsOptionsPackage.OptionInteger));
    }

    ```

4. プロジェクトをビルドし、デバッグを開始します。

5. 実験用インスタンスで、 **[ツール]** メニューの **[MyToolsOptionsCommand の呼び出し]** をクリックします。

     メッセージ ボックスに `OptionInteger` の現在の値が表示されます。

## <a name="see-also"></a>関連項目

- [オプションとオプション ページ](../extensibility/internals/options-and-options-pages.md)
