---
title: メニュー コマンドを持つ拡張機能を作成する | Microsoft Docs
description: メモ帳を起動するメニュー コマンドを持つ拡張機能を作成する方法について説明します。 メニュー コマンドを作成してから、メニュー コマンドのハンドラーを変更します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: de79662494a3228dd301e8d08480c6aa0a0192a2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089213"
---
# <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを持つ拡張機能を作成する

このチュートリアルでは、メモ帳を起動するメニュー コマンドを持つ拡張機能を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-menu-command"></a>メニュー コマンドを作成する

1. **FirstMenuCommand** という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

::: moniker range="vs-2017"

2. プロジェクトが開いたら、**FirstCommand** という名前のカスタム コマンド項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *FirstCommand.cs* に変更します。

::: moniker-end

::: moniker range=">=vs-2019"

2. プロジェクトが開いたら、**FirstCommand** という名前のカスタム コマンド項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[拡張性]** に移動し、 **[コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *FirstCommand.cs* に変更します。

::: moniker-end

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、「[実験用インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

::: moniker range="vs-2017"

4. 実験用インスタンスで、 **[ツール]**  >  **[拡張機能と更新プログラム]** ウィンドウを開きます。 **FirstMenuCommand** 拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで **[拡張機能と更新プログラム]** を開いた場合、**FirstMenuCommand** は表示されません)。

::: moniker-end

::: moniker range=">=vs-2019"

4. 実験用インスタンスで、 **[拡張]**  >  **[拡張機能の管理]** ウィンドウを開きます。 **FirstMenuCommand** 拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで **[拡張機能の管理]** を開いた場合、**FirstMenuCommand** は表示されません)。

::: moniker-end

次に、実験用インスタンスの **[ツール]** メニューに移動します。 **Invoke FirstCommand** コマンドが表示されます。 この時点でコマンドを実行すると、「**FirstCommand Inside FirstMenuCommand.FirstCommand.MenuItemCallback()** 」という内容のメッセージ ボックスが表示されます。 次のセクションでは、このコマンドからメモ帳を実際に起動する方法について説明します。

## <a name="change-the-menu-command-handler"></a>メニュー コマンドのハンドラーを変更する

次に、メモ帳が起動されるようにコマンド ハンドラーを更新してみましょう。

1. デバッグを停止し、Visual Studio の作業インスタンスに戻ります。 *FirstCommand.cs* ファイルを開いて、次の using ステートメントを追加します。

    ```csharp
    using System.Diagnostics;
    ```

2. プライベートの FirstCommand コンストラクターを見つけます。 これは、コマンドがコマンド サービスにフックされ、コマンド ハンドラーが指定される場所です。 次のように、コマンド ハンドラーの名前を「StartNotepad」に変更します。

    ```csharp
    private FirstCommand(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        CommandID menuCommandID = new CommandID(CommandSet, CommandId);
        // Change to StartNotepad handler.
        MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

3. `Execute` メソッドを削除し、メモ帳を起動するだけの `StartNotepad` メソッドを追加します。

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();

        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. では、試してみましょう。プロジェクトのデバッグを開始し、 **[ツール]**  >  **[Invoke FirstCommand]** の順にクリックすると、メモ帳のインスタンスが起動されます。

    <xref:System.Diagnostics.Process> クラスのインスタンスを使用すると、メモ帳だけでなく、任意の実行可能ファイルを実行できます。 たとえば、`calc.exe` で試してみてください。

## <a name="clean-up-the-experimental-environment"></a>実験環境をクリーンアップする

複数の拡張機能を開発している場合、または異なるバージョンの拡張機能コードの結果を調べている場合は、実験環境が想定どおりに動作しなくなる可能性があります。 この場合は、リセット スクリプトを実行する必要があります。 これは、**Visual studio の実験用インスタンスのリセット** と呼ばれ、Visual Studio SDK の一部として出荷されています。 このスクリプトでは、拡張機能へのすべての参照が実験環境から削除されるので、ゼロから開始できます。

このスクリプトは、次の 2 つの方法のいずれかで取得できます。

1. デスクトップから、 **[Visual Studio の実験用インスタンスのリセット]** を見つけます。

2. コマンド ラインから次を実行します。

    ```cmd
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>拡張機能をデプロイする

ツール拡張機能を期待どおりに実行できるようになったので、友人や同僚とそれを共有することについて考えてみましょう。 Visual Studio 2015 がインストールされていれば、これは簡単です。 行う必要があるのは、作成した *.vsix* ファイルを彼らに送信することだけです。 (リリース モードでビルドしてください。)

この拡張機能の *.vsix* ファイルは、*FirstMenuCommand* の bin ディレクトリにあります。 リリース構成をビルドしたことを想定すると、具体的には次の場所にあります。

*\<code directory>\FirstMenuCommand\FirstMenuCommand\bin\Release\FirstMenuCommand.vsix*

拡張機能をインストールするには、友人は開いている Visual Studio のインスタンスをすべて閉じて、 *.vsix* ファイルをダブルクリックする必要があります。これにより、**VSIX インストーラー** が起動されます。 ファイルは *%LocalAppData%\Microsoft\VisualStudio\<version>\Extensions* ディレクトリにコピーされます。

友人が Visual Studio を再度起動すると、 **[ツール]**  >  **[拡張機能と更新プログラム]** に FirstMenuCommand 拡張機能が表示されます。 拡張機能をアンインストールまたは無効にするには、 **[拡張機能と更新プログラム]** に移動します。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、Visual Studio の拡張機能で実行できることのごく一部のみを示しました。 Visual Studio の拡張機能で実行できるその他の (適度に簡単な) ことを次に示します。

1. 単純なメニュー コマンドを使用して、さらに多くのことを行うことができます。

   1. 独自のアイコンを追加する: [メニュー コマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)

   2. メニュー コマンドのテキストを変更する:[メニュー コマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md)

   3. コマンドにメニュー ショートカットを追加する: [キーボード ショートカットをメニュー項目にバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. さまざまな種類のコマンド、メニュー、ツールバーを追加する: [メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)

3. ツール ウィンドウの追加と組み込みの Visual Studio ツール ウィンドウの拡張: [ツール ウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)

4. IntelliSense、コード候補、その他の機能を既存のコード エディターに追加する: [エディターと言語サービスを拡張する](../extensibility/extending-the-editor-and-language-services.md)

5. 拡張機能に [オプション] および [プロパティ] ページと、ユーザー設定を追加する: [プロパティとプロパティ ウィンドウを拡張する](../extensibility/extending-properties-and-the-property-window.md)、[ユーザー設定とオプションを拡張する](../extensibility/extending-user-settings-and-options.md)

   その他の種類の拡張機能では、新しい種類のプロジェクトの作成 (「[プロジェクトの拡張](../extensibility/extending-projects.md)」)、新しい種類のエディターの作成 (「[カスタム エディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md)」)、Isolated Shell での拡張機能の実装 (「[Visual Studio Isolated Shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)」) など、さらに多くの作業が必要となります
