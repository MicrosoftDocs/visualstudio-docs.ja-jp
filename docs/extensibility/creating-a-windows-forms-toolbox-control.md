---
title: Windows フォーム ツールボックス コントロールの作成 | Microsoft Docs
description: このチュートリアルでは、Visual Studio SDK を使用して、Windows フォーム ツールボックス コントロール テンプレートを使用した簡単なカウンター コントロールを作成する方法について説明します。
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- winforms
- toolbox
- windows forms
ms.assetid: 0be6ffc1-8afd-4d02-9a5d-e27dde05fde6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 42dcf30e7c31880357bb95e3858a2c70aa59f174
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089330"
---
# <a name="create-a-windows-forms-toolbox-control"></a>Windows フォーム ツールボックス コントロールの作成

Visual Studio Extensibility Tools (VS SDK) に含まれている Windows フォーム ツールボックス コントロール項目テンプレートを使用すると、拡張機能のインストール時に自動的に追加される **ツールボックス** コントロールを作成できます。 このチュートリアルでは、他のユーザーに配布できる簡単なカウンター コントロールを、テンプレートを使用して作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-the-toolbox-control"></a>ツールボックス コントロールを作成する

Windows フォーム ツールボックス コントロール テンプレートでは、未定義のユーザー コントロールを作成できます。また、**ツールボックス** にコントロールを追加するために必要な機能がすべて用意されています。

### <a name="create-an-extension-with-a-windows-forms-toolbox-control"></a>Windows フォーム ツールボックス コントロールを使用して拡張機能を作成する

1. `MyWinFormsControl` という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. プロジェクトが開いたら、`Counter` という名前の **Windows フォーム ツールボックス コントロール** 項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[Windows フォーム ツールボックス コントロール]** を選択します。

3. これにより、ユーザー コントロール、**ツールボックス** にコントロールを配置するための `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>、展開用の VSIX マニフェストの **Microsoft.VisualStudio.ToolboxControl** アセット エントリが追加されます。

### <a name="build-a-user-interface-for-the-control"></a>コントロールのユーザー インターフェイスを構築する

`Counter` コントロールには、現在のカウントを表示するための <xref:System.Windows.Forms.Label> と、カウントを 0 にリセットするための <xref:System.Windows.Forms.Button> の 2 つの子コントロールが必要です。 呼び出し元がプログラムでカウンターをインクリメントするため、これら以外の子コントロールは必要ありません。

#### <a name="to-build-the-user-interface"></a>ユーザー インターフェイスを作成するには

1. **ソリューション エクスプローラー** で *Counter.cs* をダブルクリックして、デザイナーで開きます。

2. **[ここをクリック]** ボタンを削除します。これは、Windows フォーム ツールボックス コントロール項目テンプレートを追加するときに既定で含まれます。

3. **ツールボックス** から、`Label` コントロールと、その下にある `Button` コントロールをデザイン サーフェイスにドラッグします。

4. ユーザー コントロール全体のサイズを 150, 50 ピクセルに変更し、ボタン コントロールのサイズを 50, 20 ピクセルに変更します。

5. **[プロパティ]** ウィンドウで、デザイン サーフェイス上のコントロールに対して次の値を設定します。

    |コントロール|プロパティ|値|
    |-------------|--------------|-----------|
    |`Label1`|**[テキスト]**|""|
    |`Button1`|**名前**|btnReset|
    |`Button1`|**[テキスト]**|Reset|

### <a name="code-the-user-control"></a>ユーザー コントロールのコーディング

`Counter` コントロールは、カウンターをインクリメントするメソッド、カウンターがインクリメントされると発生するイベント、および **[Reset]** ボタンを公開します。また、現在のカウント、表示テキスト、および **[Reset]** ボタンの表示または非表示の状態を格納するための、3 つのプロパティも公開します。 `ProvideToolboxControl` 属性は、 **[ツールボックス]** のどの場所に `Counter` コントロールが表示されるかを判断します。

#### <a name="to-code-the-user-control"></a>ユーザー コントロールのコーディングを行うには

1. フォームをダブルクリックすると、その読み込みイベント ハンドラーがコード ウィンドウに表示されます。

2. イベント ハンドラー メソッドの上にあるコントロール クラスで、次の例に示すように、カウンター値を格納する整数と表示テキストを格納する文字列を作成します。

    ```csharp
    int currentValue;
    string displayText;
    ```

3. 次のパブリック プロパティ宣言を作成します。

    ```csharp
    public int Value {
        get { return currentValue; }
    }

    public string Message {
        get { return displayText; }
        set { displayText = value; }
    }

    public bool ShowReset {
        get { return btnReset.Visible; }
        set { btnReset.Visible = value; }
    }

    ```

    呼び出し元では、これらのプロパティにアクセスして、カウンターの表示テキストを取得および設定したり、 **[Reset]** ボタンの表示と非表示を切り替えたりすることができます。 呼び出し元では、読み取り専用の `Value` プロパティの現在の値を取得できますが、値を直接設定することはできません。

4. コントロールの `Load` イベントに次のコードを追加します。

    ```csharp
    private void Counter_Load(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = Message + Value;
    }

    ```

    <xref:System.Windows.Forms.UserControl.Load> イベントの **ラベル** テキストを設定すると、対象のプロパティの値が適用される前に読み込むことができます。 コンストラクターで **ラベル** テキストを設定すると、空の **ラベル** が生成されます。

5. 次のように、カウンターをインクリメントするパブリック メソッドを作成します。

    ```csharp
    public void Increment()
    {
        currentValue++;
        label1.Text = displayText + Value;
        Incremented(this, EventArgs.Empty);
    }

    ```

6. `Incremented` イベントの宣言をコントロール クラスに追加します。

    ```csharp
    public event EventHandler Incremented;
    ```

    呼び出し元では、このイベントにハンドラーを追加して、カウンターの値の変更に応答することができます。

7. デザイン ビューに戻り、 **[Reset]** ボタンをダブルクリックして `btnReset_Click` イベント ハンドラーを生成します。 次に、以下の例に示すように入力します。

    ```csharp
    private void btnReset_Click(object sender, EventArgs e)
    {
        currentValue = 0;
        label1.Text = displayText + Value;
    }

    ```

8. すぐに、クラス定義の上、 `ProvideToolboxControl` 属性の宣言内で、最初のパラメーターの値を `"MyWinFormsControl.Counter"` から `"General"`に変更します。 これにより、 **[ツールボックス]** のコントロールをホストする項目グループの名前が設定されます。

    次の例では、 `ProvideToolboxControl` の属性と、調整されたクラス定義を示しています。

    ```csharp
    [ProvideToolboxControl("General", false)]
    public partial class Counter : UserControl
    ```

### <a name="test-the-control"></a>コントロールをテストする

 **ツールボックス** コントロールをテストする場合は、まず開発環境でテストし、その後で、コンパイルされたアプリケーションでテストします。

#### <a name="to-test-the-control"></a>コントロールをテストするには

1. **F5** キーを押して **デバッグを開始** します。

    このコマンドを使用するとプロジェクトが構築され、コントロールがインストールされた Visual Studio の 2 つ目の実験用インスタンスが開きます。

2. Visual Studio の実験用インスタンスで、**Windows フォーム アプリケーション** プロジェクトを作成します。

3. **ソリューション エクスプローラー** で *Form1.cs* をダブルクリックして、デザイナーで開きます (まだ開いていない場合)。

4. **ツールボックス** では、`Counter` コントロールが **[全般]** セクションに表示されます。

5. `Counter` コントロールをフォームにドラッグして選択します。 `Value`、`Message`、`ShowReset` の各プロパティが、<xref:System.Windows.Forms.UserControl> から継承されたプロパティと一緒に、 **[プロパティ]** ウィンドウに表示されます。

6. `Message` プロパティを `Count:` に設定します。

7. <xref:System.Windows.Forms.Button> コントロールをフォームにドラッグし、ボタンの名前プロパティとテキスト プロパティを `Test` に設定します。

8. ボタンをダブルクリックしてコード ビューで *Form1.cs* を開き、クリック ハンドラーを作成します。

9. クリック ハンドラーで、`counter1.Increment()` を呼び出します。

10. コンストラクター関数で、`InitializeComponent` の呼び出しの後に「`counter1``.``Incremented +=`」と入力し、**Tab** キーを 2 回押します。

    Visual Studio によって、`counter1.Incremented` イベントのフォーム レベルのハンドラーが生成されます。

11. イベント ハンドラーで `Throw` ステートメントを強調表示し、「`mbox`」と入力します。**Tab** キーを 2 回押すと、mbox コード スニペットからメッセージ ボックスが生成されます。

12. 次の行で、以下の `if`/`else` ブロックを追加して、 **[Reset]** ボタンの表示を設定します。

    ```csharp
    if (counter1.Value < 5) counter1.ShowReset = false;
    else counter1.ShowReset = true;
    ```

13. **F5** キーを押します。

    フォームが開きます。 `Counter` コントロールに次のテキストが表示されます。

    **Count: 0**

14. **[Test]** を選択します。

    カウンターの値が増加し、Visual Studio によってメッセージ ボックスが表示されます。

15. メッセージ ボックスを閉じます。

    **[Reset]** ボタンが消えます。

16. カウンターが **5** に到達するまで **[Test]** を選択し、毎回メッセージ ボックスを閉じます。

    **[Reset]** ボタンが再び表示されます。

17. **[リセット]** を選択します。

    カウンターが **0** にリセットされます。

## <a name="next-steps"></a>次のステップ

**ツールボックス** コントロールを構築すると、Visual Studio によって、プロジェクトの \bin\debug\ フォルダーに *ProjectName.vsix* という名前のファイルが作成されます。 コントロールは、 *.vsix* ファイルをネットワークや Web サイトにアップロードすることで展開できます。 この *.vsix* ファイルをユーザーが開くと、コントロールがユーザーのコンピューターにインストールされ、Visual Studio の **ツールボックス** に追加されます。 または、 *.vsix* ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) にアップロードして、ユーザーが **[ツール]**  >  **[拡張機能と更新プログラム]** ダイアログで検索できるようにすることもできます。

## <a name="see-also"></a>関連項目

- [Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)
- [WPF ツールボックス コントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)
- [Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)
- [Windows フォーム コントロール開発の基本概念](/dotnet/framework/winforms/controls/windows-forms-control-development-basics)
