---
title: 'チュートリアル: QuickInfo ツールヒントの表示 | Microsoft Docs'
description: このチュートリアルを使用して、テキスト コンテンツの QuickInfo を表示する方法について説明します。 QuickInfo では、メソッドのシグネチャと、メソッド名の説明が表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: d374aa41d85b1d64b6623cb99f6183787a2afc53
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217256"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>チュートリアル: QuickInfo ツールヒントを表示する
QuickInfo は、ユーザーがメソッド名の上にポインターを移動したときにメソッドのシグネチャと説明を表示する、IntelliSense 機能です。 QuickInfo のような言語ベースの機能は、QuickInfo の説明の提供対象となる識別子を定義した後で、コンテンツを表示するためのツールヒントを作成することによって実装できます。 言語サービスのコンテキストで QuickInfo を定義することも、独自のファイル名拡張子とコンテンツ タイプを定義し、そのタイプだけのために QuickInfo を表示することもできます。または、既存のコンテンツ タイプ ("text" など) のために QuickInfo を表示することもできます。 このチュートリアルでは、"text" コンテンツ タイプのために QuickInfo を表示する方法を示します。

 このチュートリアルの QuickInfo の例では、ユーザーがポインターをメソッド名の上に移動したときにツールヒントを表示します。 この設計では、以下の 4 つのインターフェイスを実装する必要があります。

- ソース インターフェイス

- ソース プロバイダー インターフェイス

- コントローラー インターフェイス

- コントローラー プロバイダー インターフェイス

  ソースとコントローラーのプロバイダーは、Managed Extensibility Framework (MEF) コンポーネント パーツであり、ソースとコントローラーのクラスをエクスポートしたり、ツールヒントのテキスト バッファーを作成する <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> や、QuickInfo セッションをトリガーする <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> などのサービスやブローカーをインポートしたりする役割を担います。

  この例では QuickInfo ソースで、ハードコーディングされた、メソッド名と説明のリストを使用していますが、完全な実装では、言語サービスと言語ドキュメントが、そのコンテンツを提供する役割を担います。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールする必要はありません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します。) ソリューションに `QuickInfoTest` という名前を付けます。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-the-quickinfo-source"></a>QuickInfo ソースを実装する
 QuickInfo ソースでは、識別子とその説明のセットを収集し、いずれかの識別子が検出されたときに、ツールヒントのテキスト バッファーにコンテンツを追加します。 この例では、識別子とその説明が、ソース コンストラクターに追加されたところです。

#### <a name="to-implement-the-quickinfo-source"></a>QuickInfo ソースを実装するには

1. クラス ファイルを追加し、その名前を `TestQuickInfoSource`にします。

2. *Microsoft.VisualStudio.Language.IntelliSense* への参照を追加します。

3. 次のインポートを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet1":::

4. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> を実装するクラスを宣言し、その名前を `TestQuickInfoSource` にします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet2":::

5. QuickInfo ソース プロバイダー、テキスト バッファー、および一連のメソッド名とメソッド シグネチャのためのフィールドを追加します。 この例では、メソッド名とシグネチャが `TestQuickInfoSource` コンストラクター内で初期化されています。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet3":::

6. QuickInfo ソース プロバイダーとテキスト バッファーを設定するコンストラクターを追加し、メソッド名、メソッドのシグネチャ、メソッドの説明のセットを指定します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet4":::

7. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> メソッドを実装します。 この例のメソッドでは、現在の単語を検索するか、カーソルが行またはテキスト バッファーの末尾にある場合は、前の単語を検索します。 単語がメソッド名の 1 つである場合、そのメソッド名の説明が QuickInfo コンテンツに追加されます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet5":::

8. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> では <xref:System.IDisposable> を実装しているため、Dispose() メソッドも実装する必要があります。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet6":::

## <a name="implement-a-quickinfo-source-provider"></a>QuickInfo ソース プロバイダーを実装する
 QuickInfo ソースのプロバイダーは、主に、MEF コンポーネント パーツとして自身をエクスポートして、QuickInfo ソースをインスタンス化します。 これは MEF コンポーネント パーツであるため、その他の MEF コンポーネント パーツをインポートできます。

#### <a name="to-implement-a-quickinfo-source-provider"></a>QuickInfo ソース プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider> を実装している `TestQuickInfoSourceProvider` という名前の QuickInfo ソース プロバイダーを宣言し、<xref:Microsoft.VisualStudio.Utilities.NameAttribute> として "ToolTip QuickInfo Source"、<xref:Microsoft.VisualStudio.Utilities.OrderAttribute> として Before = "default"、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "text" を指定してそれをエクスポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet7":::

2. <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> と <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> の 2 つのエディター サービスを、`TestQuickInfoSourceProvider` のプロパティとしてインポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet8":::

3. 新しい `TestQuickInfoSource` を返す <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> を実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet9":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet9":::

## <a name="implement-a-quickinfo-controller"></a>QuickInfo コントローラーを実装する
 QuickInfo コントローラーでは、QuickInfo がいつ表示されるかを指定します。 この例では、いずれかのメソッド名に対応する単語の上にポインターが置かれたときに QuickInfo が表示されます。 QuickInfo コントローラーには、QuickInfo セッションをトリガーするマウス ホバー イベントのハンドラーを実装します。

### <a name="to-implement-a-quickinfo-controller"></a>QuickInfo コントローラーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> を実装するクラスを宣言し、その名前を `TestQuickInfoController` にします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet10":::

2. テキスト ビューのプライベート フィールド、そのテキスト ビューで表示されるテキスト バッファー、QuickInfo セッション、QuickInfo コントローラー プロバイダーを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet11":::

3. フィールドを設定するコンストラクターを追加し、マウス ホバー イベントのハンドラーを追加ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet12":::

4. QuickInfo セッションをトリガーするマウス ホバー イベントのハンドラーを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet13":::

5. コントローラーがテキスト ビューからデタッチされたときにマウス ホバー イベントのハンドラーが削除されるように <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A> メソッドを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet14":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet14":::

6. この例では、<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A> メソッドと <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> メソッドを空のメソッドとして実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet15":::

## <a name="implementing-the-quickinfo-controller-provider"></a>QuickInfo コントローラー プロバイダーの実装
 QuickInfo コントローラーのプロバイダーは、主に、MEF コンポーネント パーツとして自身をエクスポートして、QuickInfo コントローラーをインスタンス化します。 これは MEF コンポーネント パーツであるため、その他の MEF コンポーネント パーツをインポートできます。

### <a name="to-implement-the-quickinfo-controller-provider"></a>QuickInfo コントローラー プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider> を実装する `TestQuickInfoControllerProvider` という名前のクラスを宣言し、<xref:Microsoft.VisualStudio.Utilities.NameAttribute> として "ToolTip QuickInfo Controller" を、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "text" を指定して、それをエクスポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet16":::

2. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> をプロパティとしてインポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet17":::

3. QuickInfo コントローラーをインスタンス化することで <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A> メソッドを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet18":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、QuickInfoTest ソリューションをビルドし、それを実験用インスタンスで実行します。

### <a name="to-build-and-test-the-quickinfotest-solution"></a>QuickInfoTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが開始されます。

3. テキスト ファイルを作成し、"add" と "subtract" という単語を含む何らかのテキストを入力します。

4. いずれかの "add" の位置にポインターを移動します。 `add` メソッドのシグネチャと説明が表示されるはずです。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
