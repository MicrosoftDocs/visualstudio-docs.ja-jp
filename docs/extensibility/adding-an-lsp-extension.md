---
title: 言語サーバー プロトコルの拡張機能の追加 | Microsoft Docs
description: 言語サーバー プロトコル (LSP) に基づいて言語サーバーを統合する Visual Studio 拡張機能を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: accf054cbf0b58066568124a3f35e064ce3cba78
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094992"
---
# <a name="add-a-language-server-protocol-extension"></a>言語サーバー プロトコルの拡張機能の追加

言語サーバー プロトコル (LSP) は、JSON RPC v2.0 形式の共通プロトコルであり、さまざまなコード エディターに言語サービス機能を提供するために使用されます。 開発者は、このプロトコルを使用して、1 つの言語サーバーを作成して、その LSP をサポートするさまざまなコード エディターに IntelliSense、エラー診断、すべての参照の検索などの言語サービス機能を提供できます。 従来、Visual Studio の言語サービスを追加するには、構文の強調表示などの基本的な機能を提供するために TextMate 文法ファイルを使用するか、より豊富なデータを提供するために Visual Studio 機能拡張 API の完全なセットを使用するカスタム言語サービスを記述する必要がありました。 Visual Studio による LSP のサポートでは、3 番目のオプションがあります。

![Visual Studio での言語サーバー プロトコル サービス](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>言語サーバー プロトコル

![言語サーバー プロトロルの実装](media/lsp-implementation.png)

この記事では、LSP ベースの言語サーバーを使用する Visual Studio 拡張機能を作成する方法について説明します。 LSP ベースの言語サーバーを既に開発しており、それを Visual Studio に統合する必要だけがあることを前提としています。

Visual Studio 内でのサポートのために、言語サーバーは、たとえば次のようなストリームベースの転送機構を使用してクライアント (Visual Studio) と通信できます。

* 標準入力/出力ストリーム
* 名前付きパイプ
* ソケット (TCP のみ)

Visual Studio での LSP とそのサポートの目的は、Visual Studio 製品に含まれていない言語サービスをオンボードすることです。 Visual Studio で既存の言語サービス (C# など) を拡張することを目的としているわけではありません。 既存の言語を拡張するには、言語サービスの拡張ガイド (たとえば ["Roslyn" .NET Compiler Platform](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)) を参照するか、[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)に関するページをご覧ください。

プロトコル自体の詳細については、[こちら](https://github.com/Microsoft/language-server-protocol)のドキュメントを参照してください。

サンプル言語サーバーを作成する方法、または既存の言語サーバーを Visual Studio Code に統合する方法の詳細については、[こちら](https://code.visualstudio.com/docs/extensions/example-language-server)のドキュメントを参照してください。

## <a name="language-server-protocol-supported-features"></a>言語サーバー プロトコルでサポートされる機能

次の表には、Visual Studio でサポートされている LSP 機能が示されています。

メッセージ | Visual Studio での IIS サポート
--- | ---
initialize | ○
初期化済み | ○
shutdown | ○
exit | ○
$/cancelRequest | ○
window/showMessage | ○
window/showMessageRequest | ○
window/logMessage | ○
telemetry/event |
client/registerCapability |
client/unregisterCapability |
workspace/didChangeConfiguration | ○
workspace/didChangeWatchedFiles | ○
workspace/symbol | ○
workspace/executeCommand | ○
workspace/applyEdit | ○
textDocument/publishDiagnostics | ○
textDocument/didOpen | ○
textDocument/didChange | ○
textDocument/willSave |
textDocument/willSaveWaitUntil |
textDocument/didSave | ○
textDocument/didClose | ○
textDocument/completion | ○
completion/resolve | ○
textDocument/hover | ○
textDocument/signatureHelp | ○
textDocument/references | ○
textDocument/documentHighlight | ○
textDocument/documentSymbol | ○
textDocument/formatting | ○
textDocument/rangeFormatting | ○
textDocument/onTypeFormatting |
textDocument/definition | ○
textDocument/codeAction | ○
textDocument/codeLens |
codeLens/resolve |
textDocument/documentLink |
documentLink/resolve |
textDocument/rename | ○

## <a name="get-started"></a>はじめに

> [!NOTE]
> Visual Studio 2017 バージョン 15.8 以降では、共通言語サーバー プロトコルのサポートが Visual Studio に組み込まれています。 [Language Server Client VSIX](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview) のプレビュー バージョンを使用して LSP 拡張機能をビルドしている場合は、バージョン 15.8 以上にアップグレードすると、その拡張機能は動作しなくなります。 LSP 拡張機能を再び動作させるには、次の手順を実行する必要があります。
>
> 1. Microsoft Visual Studio Language Server Protocol Preview VSIX をアンインストールします。
>
>    バージョン 15.8 以降は、Visual Studio のアップグレードを実行するたびに、VSIX のプレビューが自動的に検出され削除されます。
>
> 2. Nuget 参照を、[LSP パッケージ](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)のプレビュー版以外の最新バージョンに更新します。
>
> 3. VSIX マニフェスト内の Microsoft Visual Studio Language Server Protocol Preview VSIX への依存関係を削除します。
>
> 4. VSIX で、インストール ターゲットの下限として Visual Studio 2017 バージョン 15.8 Preview 3 が指定されていることを確認します。
>
> 5. リビルドして再デプロイします。

### <a name="create-a-vsix-project"></a>VSIX プロジェクトを作成する

LSP ベースの言語サーバーを使用して言語サービス拡張機能を作成するには、まず、VS のインスタンス用に **Visual Studio 拡張機能の開発** ワークロードがインストールされていることを確認します。

次に、 **[ファイル]**  >  **[新しいプロジェクト]**  >  **[Visual C#]**  >  **[拡張性]**  >  **[VSIX プロジェクト]** の順に選択して、新しい VSIX プロジェクトを作成します。

![VSIX プロジェクトを作成する](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>言語サーバーとランタイムのインストール

既定では、Visual Studio で LSP ベースの言語サーバーをサポートするために作成される拡張機能には、言語サーバー自体や、それらを実行するために必要なランタイムは含まれていません。 拡張機能の開発者が、必要な言語サーバーとランタイムの配布を担当します。 それにはいくつかの方法があります。

* 言語サーバーは、VSIX にコンテンツ ファイルとして埋め込むことができます。
* MSI を作成して、言語サーバーまたは必要なランタイムをインストールします。
* ランタイムおよび言語サーバーを取得する方法をユーザーに伝える、Marketplace での手順を指定します。

### <a name="textmate-grammar-files"></a>TextMate 文法ファイル

LSP には、言語にテキストの色付けを与える方法に関する仕様は含まれていません。 Visual Studio で言語にカスタムの色付けを行うために、拡張機能の開発者は、TextMate 文法ファイルを使用できます。 カスタムの TextMate 文法またはテーマ ファイルを追加するには、次の手順に従います。

1. "Grammars" という名前のフォルダーを拡張機能内に作成します (または選択した任意の名前にできます)。

2. *Grammars* フォルダー内に、カスタムの色付けを与えるすべての *\*.tmlanguage*、 *\*.plist*、 *\*.tmtheme*、または *\*.json* ファイルを含めます。

   > [!TIP]
   > *.tmtheme* ファイルでは、スコープがどのように Visual Studio の分類 (名前付き色キー) にマップするかを定義します。 詳細については、 *%ProgramFiles(x86)%\Microsoft Visual Studio\\\<version>\\\<SKU>\Common7\IDE\CommonExtensions\Microsoft\TextMate\Starterkit\Themesg* ディレクトリにあるグローバル *.tmtheme* ファイルを参照できます。

3. *.pkgdef* ファイルを作成し、 次のような行を追加します。

    ```
    [$RootKey$\TextMate\Repositories]
    "MyLang"="$PackageFolder$\Grammars"
    ```

4. ファイルを右クリックして、 **[プロパティ]** を選択します。 **[ビルド]** アクションを **[コンテンツ]** に変更し、 **[VSIX に含める]** プロパティを **[true]** に変更します。

前の手順を完了した後、*Grammars* フォルダーが、'MyLang' ('MyLang' は) という名前のリポジトリ ソースとして、パッケージのインストール ディレクトリに追加されます。 このディレクトリ内の文法ファイル ( *.tmlanguage* ファイル) とテーマ ファイル ( *.tmtheme* ファイル) のすべてが候補として選択され、TextMate で与えられた組み込みの文法に取って代わります。 文法ファイルの宣言された拡張子が、開かれているファイルの拡張子に一致した場合、TextMate はステップインします。

## <a name="create-a-simple-language-client"></a>単純な言語クライアントを作成する

### <a name="main-interface---ilanguageclient"></a>メイン インターフェイス - [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true)

VSIX プロジェクトの作成後、次の NuGet パッケージをプロジェクトに追加します。

* [Microsoft.VisualStudio.LanguageServer.Client](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> 前の手順を終えた後に NuGet パッケージに依存すると、Newtonsoft.Json および StreamJsonRpc パッケージもプロジェクトに追加されます。 **拡張機能が対象とする Visual Studio のバージョンに、これらの新しいバージョンがインストールされることが確実でない限りは、これらのパッケージを更新しないでください**。 アセンブリは、VSIX に含まれません。代わりに、Visual Studio インストール ディレクトリから選択されます。 ユーザーのマシンにインストールされているバージョンより新しいバージョンのアセンブリを参照している場合、拡張機能は機能しません。

この場合、LSP ベースの言語サーバーに接続する言語クライアントに必要なメイン インターフェイスである、[ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true) インターフェイスを実装する新しいクラスを作成できます。

サンプルを次に示します。

```csharp
namespace MockLanguageExtension
{
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
        public string Name => "Bar Language Extension";

        public IEnumerable<string> ConfigurationSections => null;

        public object InitializationOptions => null;

        public IEnumerable<string> FilesToWatch => null;

        public event AsyncEventHandler<EventArgs> StartAsync;
        public event AsyncEventHandler<EventArgs> StopAsync;

        public async Task<Connection> ActivateAsync(CancellationToken token)
        {
            await Task.Yield();

            ProcessStartInfo info = new ProcessStartInfo();
            info.FileName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location), "Server", @"MockLanguageServer.exe");
            info.Arguments = "bar";
            info.RedirectStandardInput = true;
            info.RedirectStandardOutput = true;
            info.UseShellExecute = false;
            info.CreateNoWindow = true;

            Process process = new Process();
            process.StartInfo = info;

            if (process.Start())
            {
                return new Connection(process.StandardOutput.BaseStream, process.StandardInput.BaseStream);
            }

            return null;
        }

        public async Task OnLoadedAsync()
        {
            await StartAsync.InvokeAsync(this, EventArgs.Empty);
        }

        public Task OnServerInitializeFailedAsync(Exception e)
        {
            return Task.CompletedTask;
        }

        public Task OnServerInitializedAsync()
        {
            return Task.CompletedTask;
        }
    }
}
```

実装する必要のある主なメソッドは、[OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017&preserve-view=true) と [ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017&preserve-view=true) です。 [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017&preserve-view=true) は、Visual Studio に拡張機能が読み込まれ、言語サーバーを起動する準備が整ったときに呼び出されます。 このメソッドでは、[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) デリゲートをすぐに呼び出して、言語サーバーを起動する必要があることを通知することも、追加のロジックを実行して後から [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) を呼び出すこともできます。 **言語サーバーをアクティブ化するには、ある時点で StartAsync を呼び出す必要があります。**

[ActivateAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017&preserve-view=true) は、[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017&preserve-view=true) デリゲートを呼び出すと、最終的に呼び出されるメソッドです。 これには、言語サーバーを起動し、そこへの接続を確立するロジックが含まれています。 サーバーへの書き込みとサーバーからの読み取りのストリームを含んだ接続オブジェクトを返す必要があります。 ここでスローされた例外はキャッチされ、Visual Studio の InfoBar メッセージを介してユーザーに表示されます。

### <a name="activation"></a>アクティブ化

言語クライアント クラスを実装した後、そのクラスを Visual Studio に読み込み、アクティブ化する方法を定義するための 2 つの属性を定義する必要があります。

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

Visual Studio では [MEF](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (Managed Extensibility Framework) を使用して、その拡張ポイントを管理します。 [Export](/dotnet/api/system.componentmodel.composition.exportattribute) 属性は、このクラスを拡張ポイントとして選択し、適切な時点で読み込む必要があることを、Visual Studio に示します。

MEF を使用するには、VSIX マニフェストで MEF をアセットとして定義する必要もあります。

VSIX マニフェスト デザイナーを開き、 **[アセット]** タブに移動します。

![MEF アセットを追加する](media/lsp-add-asset.png)

**[新規]** をクリックして、新しいアセットを追加します。

![MEF アセットを定義する](media/lsp-define-asset.png)

* **[種類]** : Microsoft.VisualStudio.MefComponent
* **[ソース]** : 現在のソリューションのプロジェクト
* **[プロジェクト]** : [お使いのプロジェクト]

### <a name="content-type-definition"></a>コンテンツ タイプの定義

現在、LSP ベースの言語サーバー拡張機能を読み込む唯一の方法は、ファイル コンテンツ タイプによるものです。 つまり、言語クライアント クラス ([ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017&preserve-view=true) を実装) を定義するときに、ファイルの種類を定義する必要があり、このファイルを開くと拡張機能が読み込まれます。 定義されているコンテンツ タイプに一致するファイルが開かれていない場合、拡張機能は読み込まれません。

これを行うには、1 つ以上の `ContentTypeDefinition` クラスを定義します。

```csharp
namespace MockLanguageExtension
{
    public class BarContentDefinition
    {
        [Export]
        [Name("bar")]
        [BaseDefinition(CodeRemoteContentDefinition.CodeRemoteContentTypeName)]
        internal static ContentTypeDefinition BarContentTypeDefinition;

        [Export]
        [FileExtension(".bar")]
        [ContentType("bar")]
        internal static FileExtensionToContentTypeDefinition BarFileExtensionDefinition;
    }
}
```

前の例で、 *.bar* ファイル拡張子で終わるファイルに対して、コンテンツ タイプ定義が作成されています。 コンテンツ タイプ定義には "bar" という名前が付けられ、[CodeRemoteContentTypeName](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017&preserve-view=true) から派生している必要があります。

コンテンツ タイプ定義を追加した後、言語クライアントの拡張機能を言語クライアントクラスに読み込むタイミングを定義できます。

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

LSP 言語サーバーのサポートの追加には、Visual Studio に自身のプロジェクト システムを実装する必要はありません。 お客様は、Visual Studio で 1 つのファイルまたはフォルダーを開いて、言語サービスの使用を開始できます。 実際、LSP 言語サーバーのサポートは、開いているフォルダーやファイルのシナリオでのみ機能するように設計されています。 カスタム プロジェクト システムが実装されている場合、一部の機能 (設定など) は機能しません。

## <a name="advanced-features"></a>高度な機能

### <a name="settings"></a>設定

カスタム言語サーバー固有の設定のサポートは利用できますが、まだ改善しているところです。 設定は、言語サーバーのサポート対象に固有であり、通常は言語サーバーがデータを生成する方法を制御します。 たとえば、言語サーバーには、報告されるエラーの最大数の設定が含まれている場合があります。 拡張機能の作成者が既定値を定義しますが、特定のプロジェクトについてはユーザーがこれを変更できます。

下の手順に従って、設定のサポートを LSP 言語サービス拡張機能に追加します。

1. 設定とその既定値を含む JSON ファイル (たとえば、*MockLanguageExtensionSettings.json*) をプロジェクトに追加します。 次に例を示します。

    ```json
    {
        "foo.maxNumberOfProblems": -1
    }
    ```

2. JSON ファイルを右クリックして、 **[プロパティ]** を選択します。 **[ビルド]** アクションを "Content" に、"VSIX に含める" プロパティを **true** に変更します。

3. ConfigurationSections を実装し、JSON ファイルで定義されている設定のプレフィックスの一覧を返します (Visual Studio Code では、これは package.js の構成セクション名にマップされています)。

    ```csharp
    public IEnumerable<string> ConfigurationSections
    {
        get
        {
            yield return "foo";
        }
    }
    ```

4. .pkgdef ファイルをプロジェクトに追加します (新しいテキスト ファイルを追加し、ファイル拡張子を .pkgdef に変更します)。 pkgdef ファイルには次の情報が含まれている必要があります。

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
    ```

    サンプル:

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\MockLanguageExtension]
    @="$PackageFolder$\MockLanguageExtensionSettings.json"
    ```

5. .pkgdef ファイルを右クリックし、 **[プロパティ]** を選択します。 **[ビルド]** アクションを **Content** に、 **[VSIX に含める]** プロパティを **true** に変更します。

6. *source.extension.vsixmanifest* ファイルを開いて、 **[アセット]** タブでアセットを追加します。

   ![vspackage アセットを編集する](media/lsp-add-vspackage-asset.png)

   * **[種類]** : Microsoft.VisualStudio.VsPackage
   * **[ソース]** : ファイルシステム上のファイル
   * **[パス]** : [ *.pkgdef* ファイルへのパス]

### <a name="user-editing-of-settings-for-a-workspace"></a>ユーザーによるワークスペース設定の編集

1. ユーザーは、サーバーが所有するファイルを含んだワークスペースを開きます。
2. ユーザーは、*VSWorkspaceSettings.json* と呼ばれる *.vs* フォルダーにファイルを追加します。
3. ユーザーは、サーバーから指定された設定の行を *VSWorkspaceSettings.json* ファイルに追加します。 次に例を示します。

    ```json
    {
        "foo.maxNumberOfProblems": 10
    }
    ```

### <a name="enable-diagnostics-tracing"></a>診断トレースを有効にする

診断トレースを有効にすると、クライアントとサーバー間のすべてのメッセージを出力でき、問題をデバッグするときに役立ちます。 診断トレースを有効にするには、次の手順を実行します。

1. ワークスペース設定ファイル *VSWorkspaceSettings.json* を開くか作成します (「ユーザーによるワークスペース設定の編集」を参照してください)。
2. 設定 json ファイルに次の行を追加します。

```json
{
    "foo.trace.server": "Off"
}
```

トレースの詳細度には次の 3 つの値を使用できます。

* "オフ": トレースを完全にオフにします
* "メッセージ": トレースをオンにしますが、メソッド名と応答 ID だけがトレースされます。
* "詳細": トレースをオンにします。rpc メッセージ全体がトレースされます。

トレースがオンになっている場合、 *%temp%\VisualStudio\LSP* ディレクトリ内のファイルにコンテンツが書き込まれます。 ログは、 *[LanguageClientName]-[Datetime Stamp].log* の名前付け形式に従います。 現在、トレースは、フォルダーを開くシナリオにのみ有効にできます。 単一のファイルを開いて言語サーバーをアクティブ化しても、診断トレースはサポートされません。

### <a name="custom-messages"></a>カスタム メッセージ

言語サーバーとのメッセージの受け渡しを容易にする、標準の言語サーバー プロトコルには含まれていない API が用意されています。 カスタム メッセージを処理するには、言語クライアント クラスで [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) インターフェイスを実装します。 [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) ライブラリは、言語クライアントと言語サーバーの間でカスタム メッセージを転送するために使用されます。 LSP 言語クライアント拡張機能は他の Visual Studio 拡張機能と同様なので、拡張機能でカスタム メッセージを通じて、(他の Visual Studio API を使用した) Visual Studio に (LSP ではサポートされていない) 追加機能を追加することもできます。

#### <a name="receive-custom-messages"></a>カスタム メッセージを受信する

言語サーバーからカスタム メッセージを受信するには、[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) に [CustomMessageTarget](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017&preserve-view=true) プロパティを実装し、カスタム メッセージの処理方法を把握しているオブジェクトを返します。 次に例を示します。

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public object CustomMessageTarget
    {
        get;
        set;
    }

    public class CustomTarget
    {
        public void OnCustomNotification(JToken arg)
        {
            // Provide logic on what happens OnCustomNotification is called from the language server
        }

        public string OnCustomRequest(string test)
        {
            // Provide logic on what happens OnCustomRequest is called from the language server
        }
    }
}
```

#### <a name="send-custom-messages"></a>カスタム メッセージを送信する

言語サーバーにカスタム メッセージを送信するには、[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) に [AttachForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017&preserve-view=true) メソッドを実装します。 このメソッドは、言語サーバーが起動され、メッセージを受信する準備ができたときに呼び出されます。 [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs) オブジェクトはパラメーターとして渡されます。これは、[VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) API を使用してメッセージを言語サーバーに送信するために保持できます。 次に例を示します。

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public async Task AttachForCustomMessageAsync(JsonRpc rpc)
    {
        await Task.Yield();

        this.customMessageRpc = rpc;
    }

    public async Task SendServerCustomNotification(object arg)
    {
        await this.customMessageRpc.NotifyWithParameterObjectAsync("OnCustomNotification", arg);
    }

    public async Task<string> SendServerCustomMessage(string test)
    {
        return await this.customMessageRpc.InvokeAsync<string>("OnCustomRequest", test);
    }
}
```

### <a name="middle-layer"></a>中間層

拡張機能の開発者は、言語サーバーとの間で送受信された LSP メッセージを傍受することが必要になる場合があります。 たとえば、拡張機能の開発者は、特定の LSP メッセージについて送信されるメッセージ パラメーターを変更したり、LSP 機能について言語サーバーから返される結果 (入力候補など) を変更したりすることが必要になる場合があります。 これが必要な場合、拡張機能の開発者は、MiddleLayer API を使用して LSP メッセージを傍受できます。

それぞれの LSP メッセージには、傍受用の独自の中間層インターフェイスがあります。 特定のメッセージを傍受するには、そのメッセージの中間層インターフェイスを実装するクラスを作成します。 次に、言語クライアント クラスに [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017&preserve-view=true) インターフェイスを実装し、[MiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017&preserve-view=true) プロパティにオブジェクトのインスタンスを返します。 次に例を示します。

```csharp
public class MockLanguageClient: ILanguageClient, ILanguageClientCustomMessage
{
    public object MiddleLayer => MiddleLayerProvider.Instance;

    private class MiddleLayerProvider : ILanguageClientWorkspaceSymbolProvider
    {
        internal readonly static MiddleLayerProvider Instance = new MiddleLayerProvider();

        private MiddleLayerProvider()
        {
        }

        public async Task<SymbolInformation[]> RequestWorkspaceSymbols(WorkspaceSymbolParams param, Func<WorkspaceSymbolParams, Task<SymbolInformation[]>> sendRequest)
        {
            // Send along the request as given
            SymbolInformation[] symbols = await sendRequest(param);

            // Only return symbols that are "files"
            return symbols.Where(sym => string.Equals(new Uri(sym.Location.Uri).Scheme, "file", StringComparison.OrdinalIgnoreCase)).ToArray();
        }
    }
}
```

中間層機能は開発中であり、まだ包括的ではありません。

## <a name="sample-lsp-language-server-extension"></a>サンプルの LSP 言語サーバー 拡張機能

Visual Studio で LSP クライアント API を使用したサンプルの拡張機能のソース コードを表示するには、VSSDK 拡張機能のサンプルで [LSP のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol)を参照してください。

## <a name="faq"></a>よく寄せられる質問

**Visual Studio で豊富な機能サポートを提供するために LSP 言語サーバーを補完する カスタム プロジェクト システムを構築したいと考えています。そのためにはどうすればよいですか。**

Visual Studio での LSP ベースの言語サーバーのサポートは、[フォルダーを開く機能](https://devblogs.microsoft.com/visualstudio/open-any-folder-with-visual-studio-15-preview/)に依存しており、カスタム プロジェクト システムが不要になるように設計されています。 [こちら](https://github.com/Microsoft/VSProjectSystem)の手順に従って独自のカスタム プロジェクト システムを構築できますが、設定などの一部の機能が動作しない可能性があります。 LSP 言語サーバーの既定の初期化ロジックは、現在開かれているフォルダーのルート フォルダーの場所を渡すというものであり、したがって、カスタム プロジェクト システムを使用する場合は、初期化中にカスタム ロジックを指定して、言語サーバーが正常に起動できるようにする必要があります。

**デバッガーのサポートを追加するにはどうすればよいですか。**

[共通デバッグ プロトコル](https://code.visualstudio.com/docs/extensionAPI/api-debugging)のサポートは、今後のリリースで提供される予定です。

**VS でサポートされている言語サービス (JavaScript など) が既にインストールされている場合でも、追加機能 (リンティングなど) を提供する LSP 言語サーバー拡張機能をインストールできますか。**

はい。ただし、すべての機能が正しく動作するわけではありません。 LSP 言語サーバー拡張機能の最終的な目標は、Visual Studio でネイティブにサポートされていない言語サービスを有効にすることです。 LSP 言語サーバーを使用して追加のサポートを提供する拡張機能を作成できますが、一部の機能 (IntelliSense など) は円滑に操作できません。 一般に、既存の言語を拡張するためではなく、新しい言語エクスペリエンスを提供するために LSP 言語サーバー拡張機能を使用することをお勧めします。

**完成した LSP 言語サーバー VSIX はどこに発行すればよいですか。**

[こちら](walkthrough-publishing-a-visual-studio-extension.md)の Marketplace の手順を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio エディターの他の言語のサポートの追加](../ide/adding-visual-studio-editor-support-for-other-languages.md)
