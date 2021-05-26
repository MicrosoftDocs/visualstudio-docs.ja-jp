---
title: 'チュートリアル: 対応するかっこの表示 | Microsoft Docs'
description: このチュートリアルを使用して、言語のコンテキストでかっこを定義し、かっこ照合タグをテキスト コンテンツ タイプに適用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e4565e095c6bd8fe26f0bb72bd66d6df935ff16b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217269"
---
# <a name="walkthrough-display-matching-braces"></a>チュートリアル: 対応するかっこを表示する
かっこのマッチングなど、言語ベースの機能を実装します。それには、対応させたいかっこを定義し、かっこの一方にあるのがキャレットであるときには対応するかっこにテキスト マーカー タグを追加します。 言語のコンテキストでかっこを定義し、独自のファイル名拡張子とコンテンツ タイプを定義して、そのタイプだけにタグを適用するか、既存のコンテンツ タイプ ("text" など) にタグを適用することができます。 以下のチュートリアルでは、かっこ照合タグを "text" コンテンツ タイプに適用する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. エディター分類子プロジェクトを作成します。 ソリューション `BraceMatchingTest`の名前を指定します。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-a-brace-matching-tagger"></a>かっこ照合タガーを実装する
 Visual Studio で使用されているものに似たかっこの強調表示効果を得る場合は、<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 型のタガーを実装できます。 以下のコードでは、どの入れ子レベルにあってもかっこのペアに対してタガーを定義する方法を示しています。 この例のタガー コンストラクターでは、[] と {} のかっこのペアが定義されていますが、完全な言語実装では、適切なかっこのペアが、言語仕様において定義されます。

### <a name="to-implement-a-brace-matching-tagger"></a>かっこ照合タガーを実装するには

1. クラス ファイルを追加し、その名前を BraceMatching にします。

2. 以下の名前空間をインポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet1":::

3. <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 型の <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> を継承する `BraceMatchingTagger` クラスを定義します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet2":::

4. テキスト ビュー、ソース バッファー、現在のスナップショット ポイントのプロパティに加えて、かっこのペアの組のためのプロパティも追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet3":::

5. タガー コンストラクター内で、プロパティを設定し、ビュー変更イベントの <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> と <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> をサブスクライブします。 この例では、説明目的で、対応するペアがコンストラクターでも定義されています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet4":::

6. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 実装の一部として、TagsChanged イベントを宣言します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet5":::

7. イベント ハンドラーでは、`CurrentChar` プロパティの現在のキャレット位置を更新し、TagsChanged イベントを発生させます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet6":::

8. Visual Studio でのように、現在の文字が左かっこであるとき、または前の文字が右かっこであるときにかっこを照合する <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> メソッドを実装します。 一致が検出されると、このメソッドは 2 つのタグをインスタンス化します。1 つは左かっこ用、もう 1 つは右かっこ用です。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet7":::

9. 次のプライベート メソッドでは、どのレベルの入れ子でも対応するかっこを検索します。 最初のメソッドでは、左文字に対応する右文字を検索します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet8":::

10. 次のヘルパー メソッドでは、右文字に対応する左文字を検索します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet9":::

## <a name="implement-a-brace-matching-tagger-provider"></a>かっこ照合タガー プロバイダーを実装する
 タガーを実装するのに加えて、タガー プロバイダーを実装してエクスポートする必要もあります。 この場合、プロバイダーのコンテンツ タイプは "text" です。 そのため、かっこ照合はすべての種類のテキスト ファイルに表示されますが、より完全な実装では、特定のコンテンツ タイプに対してのみ、かっこの照合が適用されます。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>かっこ照合タガー プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> から継承するタガー プロバイダーを宣言して、その名前を BraceMatchingTaggerProvider とし、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "text"、<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> として <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> を指定して、それをエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet10":::

2. BraceMatchingTagger をインスタンス化する <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> メソッドを実装します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet11":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、BraceMatchingTest ソリューションをビルドし、それを実験用インスタンスで実行します。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>BraceMatchingTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが開始されます。

3. テキスト ファイルを作成し、対応するかっこを含む何らかのテキストを入力します。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. 左かっこの前にキャレットを置くときには、そのかっこと、対応する右かっこの両方を強調表示する必要があります。 右かっこのすぐ後にカーソルを置くときには、そのかっこと、対応する左かっこの両方を強調表示する必要があります。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
