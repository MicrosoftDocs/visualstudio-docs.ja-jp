---
title: 'チュートリアル: シグネチャ ヘルプの表示 | Microsoft Docs'
description: このチュートリアルを使用して、text コンテンツ タイプのシグネチャ ヘルプを表示する方法について説明します。 シグネチャ ヘルプでは、メソッドのシグネチャがツールヒントに表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d6ffa2a0e646c11cb56d08ef91e3d7a4b9af7572
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217503"
---
# <a name="walkthrough-display-signature-help"></a>チュートリアル: シグネチャ ヘルプを表示する
シグネチャ ヘルプ ("*パラメーター ヒント*" とも呼ばれます) には、ユーザーがパラメーター リストの開始文字 (通常は始めかっこ) を入力したときに、ツールヒントにメソッドのシグネチャを表示します。 パラメーターおよびパラメーターの区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。 シグネチャ ヘルプは、次の方法で定義できます。言語サービスのコンテキストでは、独自のファイル名拡張子とコンテンツ タイプを定義し、その種類のみのシグネチャ ヘルプを表示するか、既存のコンテンツ タイプ (たとえば、"text") のシグネチャ ヘルプを表示します。 このチュートリアルでは、"text" コンテンツ タイプのシグネチャ ヘルプを表示する方法を示します。

 シグネチャ ヘルプは、通常、"(" (始めかっこ) などの特定の文字を入力するとトリガーされ、")" (終わりかっこ) などの別の文字を入力すると破棄されます。 文字を入力するとトリガーされる IntelliSense 機能は、キーストローク (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイス) のコマンド ハンドラーと、<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> インターフェイスを実装するハンドラー プロバイダーを使用して実装できます。 シグネチャ ヘルプに参加するシグネチャの一覧であるシグネチャ ヘルプ ソースを作成するには、<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> インターフェイスと、<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> インターフェイスを実行するソース プロバイダーを実装します。 プロバイダーは、Managed Extensibility Framework (MEF) コンポーネント パーツであり、ソースとコントローラーのクラスをエクスポートしたり、テキスト バッファー内を移動できるようにする <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> や、シグネチャ ヘルプ セッションをトリガーする <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> などのサービスやブローカーをインポートしたりする役割を担います。

 このチュートリアルでは、ハードコーディングされた識別子のセットに対してシグネチャ ヘルプをセットアップする方法を示します。 完全な実装では、言語がそのコンテンツを提供する役割を担います。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します)。ソリューションに `SignatureHelpTest` という名前を付けます。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

4. 次の参照をプロジェクトに追加し、**CopyLocal** が `false` に設定されていることを確認します。

     Microsoft.VisualStudio.Editor

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     Microsoft.VisualStudio.Shell.14.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-signature-help-signatures-and-parameters"></a>シグネチャ ヘルプのシグネチャとパラメーターを実装する
 シグネチャ ヘルプ ソースは、<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> を実装するシグネチャに基づいています。そのシグネチャそれぞれには、<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> を実装するパラメーターが含まれています。 完全な実装では、この情報は言語ドキュメントから取得されますが、この例では、シグネチャはハードコーディングされています。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>シグネチャ ヘルプのシグネチャとパラメーターを実装するには

1. クラス ファイルを追加し、その名前を `SignatureHelpSource`にします。

2. 次のインポートを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet1":::

3. <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> を実装する、`TestParameter` という名前のクラスを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet2":::

4. すべてのプロパティを設定するコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet3":::

5. <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> のプロパティを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet4":::

6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> を実装する、`TestSignature` という名前のクラスを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet5":::

7. いくつかのプライベート フィールドを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet6":::

8. フィールドを設定し、<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> イベントをサブスクライブするコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet7":::

9. `CurrentParameterChanged` イベントを宣言します。 このイベントは、ユーザーがシグネチャのいずれかのパラメーターを入力したときに発生します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet8":::

10. プロパティ値が変更されたときに `CurrentParameterChanged` イベントが発生するように、<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> プロパティを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet9":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet9":::

11. `CurrentParameterChanged` イベントを発生させるメソッドを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet10":::

12. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> におけるコンマの数とシグネチャ内のコンマの数を比較して、現在のパラメーターを計算するメソッドを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet11":::

13. `ComputeCurrentParameter()` メソッドを呼び出す <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> イベントのイベント ハンドラーを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet12":::

14. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> プロパティを実装します。 このプロパティは、シグネチャが適用されるバッファー内のテキストの範囲に対応する <xref:Microsoft.VisualStudio.Text.ITrackingSpan> を保持します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet13":::

15. 他のパラメーターを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet14":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet14":::

## <a name="implement-the-signature-help-source"></a>シグネチャ ヘルプ ソースを実装する
 シグネチャ ヘルプ ソースは、情報の提供先の一連のシグネチャです。

#### <a name="to-implement-the-signature-help-source"></a>シグネチャ ヘルプ ソースを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> を実装する、`TestSignatureHelpSource` という名前のクラスを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet15":::

2. テキスト バッファーに参照を追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet16":::

3. テキスト バッファーとシグネチャ ヘルプ ソース プロバイダーを設定するコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet17":::

4. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> メソッドを実装します。 この例では、シグネチャがハードコーディングされていますが、完全な実装では、言語ドキュメントからこの情報を取得します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet18":::

5. ヘルパー メソッド `CreateSignature()` は、例を示す目的でのみ用意されています。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet19":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet19":::

6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> メソッドを実装します。 この例では、2 つのシグネチャとそのそれぞれに 2 つのパラメーターがあります。 したがって、このメソッドは必要ありません。 複数のシグネチャ ヘルプ ソースを使用できる完全な実装では、このメソッドは、優先度が最も高いシグネチャ ヘルプ ソースで、一致するシグネチャを提供できるかどうかを判断するために使用されます。 できない場合は、メソッドから null が返され、次に高い優先度のソースが一致を提供するように求められます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet20":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet20":::

7. `Dispose()` メソッドを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet21":::

## <a name="implement-the-signature-help-source-provider"></a>シグネチャ ヘルプ ソース プロバイダーを実装する
 シグネチャ ヘルプ ソース プロバイダーは、Managed Extensibility Framework (MEF) コンポーネント パーツのエクスポートと、シグネチャ ヘルプ ソースのインスタンス化を担当します。

#### <a name="to-implement-the-signature-help-source-provider"></a>シグネチャ ヘルプ ソース プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> を実装する、`TestSignatureHelpSourceProvider` という名前のクラスを追加し、<xref:Microsoft.VisualStudio.Utilities.NameAttribute>、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "text"、<xref:Microsoft.VisualStudio.Utilities.OrderAttribute> として Before="default" を使用してこれをエクスポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet22":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet22":::

2. `TestSignatureHelpSource` をインスタンス化して <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A> を実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet23":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet23":::

## <a name="implement-the-command-handler"></a>コマンド ハンドラーを実装する
 シグネチャ ヘルプは、通常、始めかっこ "(" 文字でトリガーされ、終わりかっこ ")" 文字で終了します。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実行して、既知のメソッド名が前に置かれた始めかっこ文字を受け取ったときにシグネチャ ヘルプ セッションをトリガーし、終わりかっこ文字を受け取ったときにセッションを破棄することで、これらのキーストロークを処理できます。

#### <a name="to-implement-the-command-handler"></a>コマンド ハンドラーを実装するには

1. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実装する、`TestSignatureHelpCommand` という名前のクラスを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet24":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet24":::

2. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> アダプター (コマンド ハンドラーのチェーンにコマンド ハンドラーを追加できるようにします)、テキスト ビュー、シグネチャ ヘルプ ブローカーおよびセッション、<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>、次の <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> のプライベート フィールドを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet25":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet25":::

3. これらのフィールドを初期化し、コマンド フィルターをコマンド フィルターのチェーンに追加するためにコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet26":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet26":::

4. 既知のいずれかのメソッド名の後でコマンド フィルターが始めかっこ "(" 文字を受け取ると、シグネチャ ヘルプ セッションをトリガーし、セッションがまだアクティブな間に終わりかっこ ")" 文字を受け取ると、セッションを破棄するように <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを実装します。 いずれの場合も、コマンドは転送されます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet27":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet27":::

5. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを実装して、常にコマンドを転送するようにします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet28":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet28":::

## <a name="implement-the-signature-help-command-provider"></a>シグネチャ ヘルプ コマンド プロバイダーを実装する
 テキスト ビューが作成されるときに、<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> を実装してコマンド ハンドラーをインスタンス化すると、シグネチャ ヘルプ コマンドを提供できます。

### <a name="to-implement-the-signature-help-command-provider"></a>シグネチャ ヘルプ コマンド プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> を実装する、`TestSignatureHelpController` という名前のクラスを追加し、<xref:Microsoft.VisualStudio.Utilities.NameAttribute>、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>、<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> を使用してエクスポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet29":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet29":::

2. (<xref:Microsoft.VisualStudio.Text.Editor.ITextView> を取得するために使用され、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクトが与えられる) <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>、(現在の単語を検索するために使用される) <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>、(シグネチャ ヘルプ セッションをトリガーする) <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> をインポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet30":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet30":::

3. `TestSignatureCommandHandler` をインスタンス化して <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> メソッドを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet31":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet31":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、SignatureHelpTest ソリューションをビルドして、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>SignatureHelpTest ソリューションをビルドしテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスが起動されます。

3. テキスト ファイルを作成し、"add" という単語と始めかっこを含むテキストを入力します。

4. 始めかっこを入力した後、`add()` メソッドの 2 つのシグネチャの一覧を示すツールヒントが表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
