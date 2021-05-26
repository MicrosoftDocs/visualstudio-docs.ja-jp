---
title: 'チュートリアル: 入力候補の表示 | Microsoft Docs'
description: このチュートリアルを使用して、プレーンテキスト コンテンツに対して言語ベースの入力候補を実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: leslierichardson95
ms.author: lerich
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 51281c261baf5744c1d3aa0903985a173ff240f2
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217477"
---
# <a name="walkthrough-display-statement-completion"></a>チュートリアル: 入力候補の表示
入力候補を提供する識別子を定義し、入力候補セッションをトリガーすることによって、言語ベースの入力候補を実装できます。 言語サービスのコンテキストで入力候補を定義し、独自のファイル名の拡張子とコンテンツ タイプを定義して、その型の入力候補だけを表示することができます。 または、既存のコンテンツ タイプ ("plaintext" など) の入力候補をトリガーすることもできます。 このチュートリアルでは、テキスト ファイルのコンテンツ タイプである "plaintext" コンテンツ タイプに対して入力候補をトリガーする方法について説明します。 "text" コンテンツ タイプは、コード ファイルや XML ファイルなど、他のすべてのコンテンツ タイプの先祖です。

 通常、入力候補は特定の文字を入力することによってトリガーされます。たとえば、"using" などの識別子の先頭を入力します。 通常、**Space** キー、**Tab** キー、または **Enter** キーを押して選択範囲をコミットすると、閉じます。 キーストローク (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイス) のコマンド ハンドラーと、<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> インターフェイスを実装するハンドラー プロバイダーを使用して、文字を入力するときにトリガーされる IntelliSense 機能を実装できます。 入力候補に含まれる識別子の一覧である入力候補ソースを作成するには、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> インターフェイスと入力候補ソース プロバイダー (<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> インターフェイス) を実装します。 プロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのパーツです。 ソースとコントローラーのクラスをエクスポートし、サービスとブローカーをインポートする役割を担います。たとえば、テキスト バッファー内の移動を可能にする <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> や、入力候補セッションをトリガーする <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> などです。

 このチュートリアルでは、ハードコーディングされた識別子のセットに対して入力候補を実装する方法について説明します。 完全な実装では、言語サービスと言語ドキュメントにそのコンテンツを提供する役割があります。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します。) ソリューションに `CompletionTest` という名前を付けます。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

4. 次の参照をプロジェクトに追加し、**CopyLocal** が `false` に設定されていることを確認します。

     Microsoft.VisualStudio.Editor

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     Microsoft.VisualStudio.Shell.15.0

     Microsoft.VisualStudio.Shell.Immutable.10.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-the-completion-source"></a>入力候補ソースの実装
 入力候補ソースは、識別子の最初の文字などの入力候補のトリガーをユーザーが入力したときに、一連の識別子を収集し、その内容を入力候補ウィンドウに追加する役割を担います。 この例では、識別子とその説明は、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> メソッドでハードコーディングされています。 ほとんどの実際の使用では、言語のパーサーを使用してトークンを取得し、入力候補一覧に入力します。

### <a name="to-implement-the-completion-source"></a>入力候補ソースを実装するには

1. クラス ファイルを追加し、その名前を `TestCompletionSource`にします。

2. 次のインポートを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet1":::

3. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> を実装するように、`TestCompletionSource` のクラス宣言を変更します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet2":::

4. ソース プロバイダー、テキスト バッファー、および (入力候補セッションに含まれる識別子に対応する) <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> オブジェクトの一覧のプライベート フィールドを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet3":::

5. ソース プロバイダーとバッファーを設定するコンストラクターを追加します。 `TestCompletionSourceProvider` クラスは、後の手順で定義します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet4":::

6. コンテキストで提供する入力候補を含む入力候補セットを追加して、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> メソッドを実装します。 各入力候補セットには <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> 入力候補のセットが含まれており、入力候補ウィンドウのタブに対応しています。 (Visual Basic プロジェクトでは、[入力候補] ウィンドウのタブの名前は **共通** と **すべて** になります。) `FindTokenSpanAtPosition` メソッドは、次の手順で定義します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet5":::

7. カーソルの位置から現在の単語を検索するには、次のメソッドを使用します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet6":::

8. `Dispose()` メソッドを実装します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet7":::

## <a name="implement-the-completion-source-provider"></a>入力候補ソース プロバイダーを実装します。
 入力候補ソース プロバイダーは、入力候補ソースをインスタンス化する MEF コンポーネントのパーツです。

### <a name="to-implement-the-completion-source-provider"></a>入力候補ソース プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> を実装する、`TestCompletionSourceProvider` という名前のクラスを追加します。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> を "plaintext"、<xref:Microsoft.VisualStudio.Utilities.NameAttribute> を "test completion" として、このクラスをエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet8":::

2. <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> をインポートします。これにより、入力候補ソース内の現在の単語が検索されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet9":::

3. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> メソッドを実装して、入力候補ソースをインスタンス化します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb" id="Snippet10":::

## <a name="implement-the-completion-command-handler-provider"></a>入力候補コマンド ハンドラー プロバイダーを実装する
 入力候補コマンド ハンドラー プロバイダーは、<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> から派生します。このクラスは、テキスト ビュー作成イベントをリッスンし、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> から、Visual Studio シェルのコマンド チェーンにコマンドを追加できるように、そのビューを <xref:Microsoft.VisualStudio.Text.Editor.ITextView> に変換します。 このクラスは MEF エクスポートであるため、このクラスを使用して、コマンド ハンドラー自体が必要とするサービスをインポートすることもできます。

#### <a name="to-implement-the-completion-command-handler-provider"></a>入力候補コマンド ハンドラー プロバイダーを実装するには

1. `TestCompletionCommandHandler` という名前のファイルを追加します。

2. 次の using ディレクティブを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet11":::

3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> を実装する、`TestCompletionHandlerProvider` という名前のクラスを追加します。 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> を "token completion handler"、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> を "plaintext"、および <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> を <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable> として、このクラスをエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet12":::

4. <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> をインポートします。これにより、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> から <xref:Microsoft.VisualStudio.Text.Editor.ITextView>、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>、および <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> への変換が可能になり、標準の Visual Studio サービスへのアクセスが可能になります。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet13":::

5. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> メソッドを実装して、コマンド ハンドラーをインスタンス化します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet14":::

## <a name="implement-the-completion-command-handler"></a>入力候補コマンド ハンドラーを実装する
 入力候補はキーストロークによってトリガーされるため、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装して、入力候補セッションをトリガー、コミット、および破棄するキーストロークを受信して処理する必要があります。

#### <a name="to-implement-the-completion-command-handler"></a>入力候補コマンド ハンドラーを実装するには

1. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実装する、`TestCompletionCommandHandler` という名前のクラスを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet15":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet15":::

2. 次のコマンド ハンドラー (コマンドの渡し先)、テキスト ビュー、コマンド ハンドラー プロバイダー (さまざまなサービスへのアクセスを可能にします)、および入力候補セッションのプライベート フィールドを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet16":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet16":::

3. テキスト ビューとプロバイダー フィールドを設定するコンストラクターを追加し、コマンド チェーンにコマンドを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet17":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet17":::

4. 次のコマンドを渡すことによって、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを実装します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet18":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet18":::

5. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを実装します。 このメソッドがキーストロークを受け取ったとき、次のいずれかの操作を行う必要があります。

   - 文字がバッファーに書き込まれることを許可し、その後、入力候補をトリガーまたはフィルター処理します。 (印刷文字はこれを行います。)

   - 入力候補をコミットしますが、バッファーへの文字の書き込みは許可しません。 (入力候補セッションが表示されるとき、Space キー、**Tab** キー、または **Enter キー** がこれを行います。)

   - コマンドを次のハンドラーに渡すことを許可します。 (その他のすべてのコマンド。)

     このメソッドは UI を表示する可能性があるため、<xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> を呼び出して、オートメーション コンテキストで呼び出されないようにします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet19":::

6. このコードは、入力候補セッションをトリガーするプライベート メソッドです。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet20":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet20":::

7. 次の例は、<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> イベントからアンサブスクライブするプライベート メソッドです。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet21":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet21":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、CompletionTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-completiontest-solution"></a>CompletionTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが開始されます。

3. テキスト ファイルを作成し、"add" という単語を含む何らかのテキストを入力します。

4. 最初に "a"、次に "d" を入力すると、"addition" と "adaptation" を含む一覧が表示されます。 addition が選択されていることを確認します。 もう 1 回 "d" を入力すると、一覧に "addition" のみが表示されます。これは現在選択されています。 **Space** キー、**Tab** キー、または **Enter** キーを押して "addition" をコミットするか、Esc キーまたは他のキーを入力して一覧を閉じます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
