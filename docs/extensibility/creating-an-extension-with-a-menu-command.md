---
title: メニューコマンドを使用して拡張機能を作成する |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7cb82a2a5e02b2e109bb5b27ec54d1a2cd965901
ms.sourcegitcommit: 90c3187d804ad7544367829d07ed4b47d3f8a72d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68821542"
---
# <a name="create-an-extension-with-a-menu-command"></a>メニューコマンドを使用して拡張機能を作成する

このチュートリアルでは、メモ帳を起動するメニューコマンドを使用して拡張機能を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 詳細については、"[Visual Studio SDK をインストール](../extensibility/installing-the-visual-studio-sdk.md)"を参照してください。

## <a name="create-a-menu-command"></a>メニューコマンドを作成する

1. **Firstmenucommand**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、 **[新しいプロジェクト]** ダイアログで見つけることができます。

2. プロジェクトが開いたら、 **Firstcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[**新しい項目**の**追加** > ] を選択します。 **[新しい項目の追加]** ダイアログで、 **[ C#ビジュアル**  > **機能拡張**] にアクセスし、 **[カスタムコマンド]** を選択します。 ウィンドウの下部にある **名前** フィールドで、コマンドファイル名 を*FirstCommand.cs*に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、[実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

::: moniker range="vs-2017"

4. 実験用インスタンスで、[**ツール** > ] **[拡張機能と更新プログラム]** ウィンドウを開きます。 **Firstmenucommand**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで**拡張機能と更新プログラム**を開いた場合、 **firstmenucommand**は表示されません)。

::: moniker-end

::: moniker range=">=vs-2019"

4. 実験用インスタンスで、[**拡張** > **機能の管理**] ウィンドウを開きます。 **Firstmenucommand**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで **[拡張機能の管理]** を開いた場合、 **firstmenucommand**は表示されません)。

::: moniker-end

次に、実験用インスタンスの **[ツール]** メニューにアクセスします。 **呼び出し FirstCommand**コマンドが表示できます。 この時点で、コマンドを実行すると、 **Firstcommandpackage 内に Firstcommandpackage**というメッセージボックスが表示されます。 次のセクションでは、このコマンドからメモ帳を実際に起動する方法について説明します。

## <a name="change-the-menu-command-handler"></a>メニューコマンドハンドラーの変更

次に、コマンドハンドラーを更新してメモ帳を起動してみましょう。

1. デバッグを停止し、Visual Studio の作業インスタンスに戻ります。 *FirstCommand.cs*ファイルを開き、次の using ステートメントを追加します。

    ```csharp
    using System.Diagnostics;
    ```

2. プライベート FirstCommand コンストラクターを検索します。 コマンドがコマンドサービスにフックされ、コマンドハンドラーが指定されている場合は、次のようになります。 次のように、コマンドハンドラーの名前を「StartNotepad」に変更します。

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

3. メソッドを削除し、 `StartNotepad`メソッドを追加します。これにより、メモ帳が開始されます。 `MenuItemCallback`

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. 試してみましょう。プロジェクトのデバッグを開始し、[**ツール** > ] **[firstcommand]** の順にクリックすると、メモ帳のインスタンスが表示されます。

    <xref:System.Diagnostics.Process>クラスのインスタンスを使用して、メモ帳だけでなく、任意の実行可能ファイルを実行できます。 たとえば、を`calc.exe`使用して試してみてください。

## <a name="clean-up-the-experimental-environment"></a>実験環境のクリーンアップ

複数の拡張機能を開発している場合、または異なるバージョンの拡張コードを使用して結果を調査している場合は、実験環境が動作しなくなる可能性があります。 この場合は、リセットスクリプトを実行する必要があります。 これは、 **Visual studio の実験的なインスタンスのリセット**と呼ばれ、VISUAL studio SDK の一部として出荷されます。 このスクリプトは、拡張機能へのすべての参照を実験環境から削除するので、最初から開始できます。

このスクリプトは、次の2つの方法のいずれかで取得できます。

1. デスクトップから、 **[Visual Studio の実験用インスタンスのリセット]** を探します。

2. コマンド ラインから次を実行します。

    ```xml
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>拡張機能をデプロイする

ツール拡張機能を希望どおりに実行できるようになったので、友人や同僚との共有について考えてみましょう。 これは、Visual Studio 2015 がインストールされている限り、簡単です。 作成した *.vsix*ファイルを送信するだけで済みます。 (リリースモードでビルドするようにしてください)。

この拡張機能の *.vsix*ファイルは、 *firstmenucommand* bin ディレクトリにあります。 具体的には、リリース構成をビルドしたことを前提として、次のようになります。

*\<コードディレクトリ > \FirstMenuCommand\FirstMenuCommand\bin\Release\ FirstMenuCommand .vsix*

拡張機能をインストールするには、フレンドが開いている Visual Studio のインスタンスをすべて閉じ、.vsix ファイルをダブルクリックする必要があり*ます*。これにより、 **vsix インストーラー**が表示されます。 ファイルは *%LocalAppData%\Microsoft\VisualStudio\<version > \ Extensions*ディレクトリにコピーされます。

友人が Visual Studio を再度起動すると、[**ツール** > ] **[拡張機能と更新プログラム]** に firstmenucommand 拡張機能が表示されます。 拡張機能**と更新プログラム**にアクセスして、拡張機能をアンインストールまたは無効にすることができます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio 拡張機能で実行できることのほんの一部のみを示しました。 Visual Studio 拡張機能で実行できるその他の (非常に簡単な) 項目を次に示します。

1. 単純なメニューコマンドを使用して、さらに多くのことを行うことができます。

   1. 独自のアイコンを追加します。[メニューコマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)

   2. メニューコマンドのテキストを変更します。[メニューコマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md)

   3. コマンドにメニューショートカットを追加します。[メニュー項目にキーボードショートカットをバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. さまざまな種類のコマンド、メニュー、およびツールバーを追加します。[メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)

3. ツールウィンドウを追加し、組み込みの Visual Studio ツールウィンドウを拡張します。[ツールウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)

4. IntelliSense、コード候補、およびその他の機能を既存のコードエディターに追加します。[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)

5. 拡張機能にオプションおよびプロパティページとユーザー設定を追加します。[プロパティとプロパティウィンドウを拡張](../extensibility/extending-properties-and-the-property-window.md)し、[ユーザー設定とオプションを拡張](../extensibility/extending-user-settings-and-options.md)する

   その他の種類の拡張機能には、新しい種類のプロジェクトの作成 (プロジェクトの[拡張](../extensibility/extending-projects.md))、新しい種類のエディターの作成 ([カスタムエディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md))、分離シェルでの拡張機能の実装など、さらに多くの作業が必要です。[Visual Studio 分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
