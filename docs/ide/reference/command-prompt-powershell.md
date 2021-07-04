---
title: 開発者向けのコマンドライン シェルとプロンプト
description: '[ツール]、[コマンド ライン] メニューから開始します。 .NET および C++ ツールは、Visual Studio 開発者コマンド プロンプト、開発者用 PowerShell およびターミナルからより簡単に使用できます。'
author: TerryGLee
ms.author: tglee
ms.date: 06/11/2021
ms.topic: reference
ms.custom: contperf-fy21q4
helpviewer_keywords:
- Visual Studio command prompt
- command prompt, Visual Studio
- Developer Command Prompt
- Developer PowerShell
- Visual Studio terminal
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
no-loc: cmdlet
ms.openlocfilehash: 858845ca5629f64e282e3864daa0201935316062
ms.sourcegitcommit: b4cc3dee59421f7089112becf128a369acadaf61
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2021
ms.locfileid: "112990520"
---
# <a name="visual-studio-developer-command-prompt-and-developer-powershell"></a>Visual Studio 開発者コマンド プロンプトと開発者用 PowerShell

Visual Studio 2019 には、開発者向けの 2 つのコマンドライン シェルが含まれています。

- **Visual Studio 開発者コマンド プロンプト** - 開発者用コマンドライン ツールを簡単に使用できるように特定の環境変数が設定されている標準コマンド プロンプトです。 Visual Studio 2015 以降で使用できます。

- **Visual Studio Developer PowerShell** - コマンド プロンプトよりも、さらに高機能です。 たとえば、1 つのコマンド ( *cmdlet* と呼ばれる) の出力を別のcmdletに渡すことができます。 このシェルには、開発者コマンド プロンプトと同じ環境変数が設定されています。 Visual Studio 2019 以降で使用できます。


:::image type="content" source="media/developer-command-prompt-for-vs/command-prompt.png" alt-text="clrver ツールが表示された Visual Studio の開発者コマンド プロンプト":::

Visual Studio 2019 バージョン 16.5 以降、Visual Studio には、これらのシェル (開発者コマンド プロンプトと開発者用 PowerShell) のどちらもホストできる統合 **ターミナル** が組み込まれています。 各シェルの複数のタブを開くこともできます。 Visual Studio ターミナルは、[Windows ターミナル](/windows/terminal/)を基に構築されています。 Visual Studio でターミナルを開くには、 **[表示]**  >  **[ターミナル]** を選択します。

:::image type="content" source="media/developer-command-prompt-for-vs/vs-terminal.png" alt-text="複数のタブが表示された Visual Studio ターミナル":::

いずれかの開発者シェルを Visual Studio から別のアプリとして、またはターミナル ウィンドウで開くと、現在のソリューションのディレクトリが表示されます (ソリューションを読み込み済みの場合)。 この動作により、ソリューションまたはそのプロジェクトに対してコマンドを実行するのが容易になります。

どちらのシェルにも、開発者用コマンドライン ツールをより簡単に使用できるように特定の環境変数が設定されています。 これらのシェルのいずれかを開いたら、さまざまなユーティリティのコマンドを入力できます。それらがどこにあるのかを知っている必要はありません。 

|よく使うコマンド|説明|
|--|--|
|[`MSBuild`](../../msbuild/msbuild-command-line-reference.md)|プロジェクトまたはソリューションをビルドする|
|[`clrver`](/dotnet/framework/tools/clrver-exe-clr-version-tool)| clr 用の [.NET Framework ツール](/dotnet/framework/tools/index)|
|[`ildasm`](/dotnet/framework/tools/ildasm-exe-il-disassembler)|逆アセンブラー用の [.NET Framework ツール](/dotnet/framework/tools/index)|
|[`dotnet`](/dotnet/core/tools/dotnet)|[.NET CLI コマンド](/dotnet/core/tools/index)|
|[`dotnet run`](/dotnet/core/tools/dotnet-run)|[.NET CLI コマンド](/dotnet/core/tools/index)|
|[`CL`](/cpp/build/reference/compiler-command-line-syntax)|C/C++ コンパイル ツール|
|[`NMAKE`](/cpp/build/reference/running-nmake)|C/C++ コンパイル ツール|
|[`LIB`](/cpp/build/reference/lib-reference)| C/C++ ビルド ツール|
|[`DUMPBIN`](/cpp/build/reference/dumpbin-reference)| C/C++ ビルド ツール|


## <a name="start-in-visual-studio"></a>Visual Studio で開始する

Visual Studio 内から開発者コマンド プロンプトまたは開発者用 PowerShell を開くには、次の手順に従います。

1. Visual Studio を開きます。

1. メニュー バーの **[ツール]**  >  **[コマンド ライン]**  >  **[開発者コマンド プロンプト]** または **[開発者用 PowerShell]** を選択します。

   ![Visual Studio でのコマンド プロンプト メニュー項目](./media/developer-command-prompt-for-vs/vs-menu.png)

## <a name="start-from-windows-menu"></a>Windows メニューから開始する

シェルを起動するもう 1 つの方法は、[スタート] メニューからです。 Visual Studio のバージョンと、インストールした追加の SDK およびワークロードに応じて、複数のコマンド プロンプトがある場合があります。 

### <a name="windows-10"></a>Windows 10

1. **スタート** ![キーボードの Windows ロゴ キー](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png)を選択し、 文字 **V** までスクロールします。

1. **[Visual Studio 2019]** フォルダーを展開します。

1. **[開発者コマンド プロンプト for VS 2019]** または **[Developer PowerShell for VS 2019]\(開発者用 PowerShell for VS 2019\)** を選択します。

   または、最初にタスク バーの [検索] ボックスにシェルの名前を入力することもできます。一致する検索結果が結果一覧に表示され始めたら、必要なものを選択します。

   ![Windows 10 での検索動作を示すアニメーション GIF](./media/developer-command-prompt-for-vs/windows-10-search.gif)

### <a name="windows-81"></a>Windows 8.1

1. キーボードの Windows ロゴ キー ![キーボードの Windows ロゴ キー](./media/developer-command-prompt-for-vs/windows-logo-key-graphic.png) を押すなどして、 **[スタート]** 画面に 移動します。

1. **[スタート]** 画面で、**Ctrl**+**Tab** キーを押して **[アプリ]** の一覧を開き、**V** を押します。インストールされているすべての Visual Studio コマンド プロンプトが含まれた一覧が表示されます。

1. **[開発者コマンド プロンプト for VS 2019]** または **[Developer PowerShell for VS 2019]\(開発者用 PowerShell for VS 2019\)** を選択します。

### <a name="windows-7"></a>Windows 7

1. **[スタート]** を選択し、 **[すべてのプログラム]** を展開します。

1. **[Visual Studio 2019]**  >  **[Visual Studio Tools]**  >  **[開発者コマンド プロンプト for VS 2019]** または **[Developer PowerShell for VS 2019]\(開発者用 PowerShell for VS 2019\)** を選択します。

   ![コマンド プロンプトが強調表示されている Windows 7 の [スタート] メニュー](./media/developer-command-prompt-for-vs/windows-7-menu.png)

[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) や[それ以前のバージョン](https://developer.microsoft.com/windows/downloads/sdk-archive)など、他の SDK がインストールされている場合は、コマンド プロンプトがさらに表示されることがあります。 各ツールのドキュメントを参照して、どのバージョンのコマンド プロンプトを使用する必要があるかを確認してください。

## <a name="start-from-file-browser"></a>ファイル ブラウザーから開始する 

インストール済みのシェルのショートカットは、通常、 **[スタート] メニュー** の Visual Studio フォルダー内 ( *%ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2019\Visual Studio Tools* 内など) にあります。 ただし、コマンド プロンプトを探しても期待した結果が得られない場合は、コンピューター上でファイルを手動で探すことができます。

### <a name="developer-command-prompt"></a>開発者コマンド プロンプト

コマンド プロンプト ファイルの名前 (*VsDevCmd.bat*) を検索するか、Visual Studio の Tools フォルダー ( *%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools* など) に移動します (パスは、使用している Visual Studio のバージョン、エディション、およびインストール場所に応じて変わります)。

コマンド プロンプト ファイルが見つかったら、通常のコマンド プロンプト ウィンドウで次のコマンドを入力して、それを開きます。

```cmd
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

または、Windows の **[ファイル名を指定して実行]** ダイアログ ボックスに次のコマンドを入力します。

```cmd
%comspec% /k "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\VsDevCmd.bat"
```

> [!TIP]
> パスは、実際の Visual Studio のインストールに合わせて編集する必要があります。

### <a name="developer-powershell"></a>開発者用 PowerShell

*Launch-VsDevShell.ps1* という名前の PowerShell スクリプト ファイルを検索するか、Visual Studio の Tools フォルダー ( *%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\Tools* など) に移動します (使用している Visual Studio のバージョン、エディション、インストール場所に応じてパスを変更します)。PowerShell ファイルが見つかったら、Windows PowerShell または PowerShell 6 のプロンプトで次のコマンドを入力して、それを開きます。

```powershell
& 'C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\Tools\Launch-VsDevShell.ps1'
```

既定では、起動される Developer PowerShell は、*Launch-VsDevShell.ps1* ファイルが配置されているインストール パスを持つ Visual Studio インストール用に構成されています。

> [!TIP]
> cmdletを実行するには、[実行ポリシー](/powershell/module/microsoft.powershell.core/about/about_execution_policies)が設定されている必要があります。

## <a name="see-also"></a>こちらもご覧ください

- [開発者用 PowerShell](https://devblogs.microsoft.com/visualstudio/the-powershell-you-know-and-love-now-with-a-side-of-visual-studio/)
- [新しい Visual Studio ターミナルの紹介](https://devblogs.microsoft.com/visualstudio/say-hello-to-the-new-visual-studio-terminal/)
- [Windows ターミナル](/windows/terminal/)
- [.NET Framework ツール](/dotnet/framework/tools/index)
- [外部ツールの管理](../managing-external-tools.md)
- [コマンド ラインから Microsoft C++ ツールセットを使用する](/cpp/build/building-on-the-command-line)
