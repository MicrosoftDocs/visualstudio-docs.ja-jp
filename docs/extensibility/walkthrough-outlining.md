---
title: 'チュートリアル: アウトライン | Microsoft Docs'
description: 言語サービスのコンテキストで、または独自のファイル名拡張子やコンテンツ タイプのために、アウトライン領域を定義して表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: 7bf4c0cc8757ea4f034da2ac17d6c76971f86305
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217230"
---
# <a name="walkthrough-outlining"></a>チュートリアル: アウトライン
展開したり折りたたんだりするテキスト領域の種類を定義することで、アウトラインなどの言語ベースの機能を設定します。 言語サービスのコンテキストで領域を定義することも、独自のファイル名拡張子やコンテンツ タイプを定義して、そのタイプにのみ領域の定義を適用することもできます。または、既存のコンテンツ タイプ ("text" など) に領域の定義を適用できます。 このチュートリアルでは、アウトライン領域を定義して表示する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. VSIX プロジェクトを作成する。 ソリューション `OutlineRegionTest`の名前を指定します。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-an-outlining-tagger"></a>アウトライン タガーを実装する
 アウトライン領域は、ある種類のタグ (<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>) でマークされます。 このタグにより、標準のアウトライン動作が提供されます。 アウトラインの対象領域は、展開したり折りたたんだりすることができます。 アウトラインの対象領域は、折りたたまれている場合はプラス記号 ( **+** ) で、展開されている場合はマイナス記号 ( **-** ) でマークされます。そして、展開された領域は垂直線で区切られます。

 以下の手順では、角かっこ ( **[** 、 **]** ) で区切られたすべての領域に対してアウトライン領域を作成するタガーを定義する方法を示します。

### <a name="to-implement-an-outlining-tagger"></a>アウトライン タガーを実装するには

1. クラス ファイルを追加し、その名前を `OutliningTagger`にします。

2. 以下の名前空間をインポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet1":::

3. `OutliningTagger` という名前のクラスを作成し、それに <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> を実装します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet2":::

4. テキスト バッファーとスナップショットを追跡し、アウトライン領域としてタグ付けする必要がある行のセットを収集するため、いくつかのフィールドを追加します。 このコードには、アウトライン領域を表す Region オブジェクト (後で定義されます) の一覧が含まれています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet3":::

5. フィールドを初期化し、バッファーを解析して、<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> イベントにイベント ハンドラーを追加するタガー コンストラクターを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet4":::

6. タグの範囲をインスタンス化する <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> メソッドを実装します。 この例では、メソッドに渡される <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> 内の範囲が連続していることを前提としていますが、常にそうであるとは限りません。 このメソッドでは、アウトライン領域ごとに新しいタグの範囲をインスタンス化します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet5":::

7. `TagsChanged` イベント ハンドラーを宣言します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet6":::

8. テキスト バッファーを解析することによって <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> イベントに応答する `BufferChanged` イベント ハンドラーを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet7":::

9. バッファーを解析するメソッドを追加します。 ここに示した例は、例示のみを目的としています。 これによってバッファーは同期的に解析され、入れ子になったアウトライン領域に入れられます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet8":::

10. 次のヘルパー メソッドでは、アウトラインのレベルを表す整数を取得しており、1 が最も左側の中かっこのペアとなっています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet9":::

11. 次のヘルパー メソッドでは、(この記事の後方で定義されている) 1 つの Region を SnapshotSpan に変換しています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet10":::

12. 次のコードは、例示のみを目的としています。 これは、アウトライン領域の開始の行番号およびオフセットと、親領域 (存在する場合) への参照が含まれる PartialRegion クラスを定義しています。 このコードにより、パーサーは、入れ子になったアウトライン領域を設定できるようになります。 派生した Region クラスには、アウトライン領域の終了の行番号への参照が含まれています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet11":::

## <a name="implement-a-tagger-provider"></a>タガー プロバイダーを実装する
 作成したタガーのタガー プロバイダーをエクスポートします。 タガー プロバイダーでは、コンテンツ タイプが "text" であるバッファーのために `OutliningTagger` を作成します。または、バッファーにそれが既に存在する場合は `OutliningTagger` を返します。

### <a name="to-implement-a-tagger-provider"></a>タガー プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> を実装する `OutliningTaggerProvider` という名前のクラスを作成し、ContentType 属性と tagtype 属性を指定してそれをエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet12":::

2. バッファーのプロパティに `OutliningTagger` を追加して <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A> メソッドを実装します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet13":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、OutlineRegionTest ソリューションをビルドし、それを実験用のインスタンスで実行します。

### <a name="to-build-and-test-the-outlineregiontest-solution"></a>OutlineRegionTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが開始されます。

3. テキスト ファイルを作成します。 左角かっこと右角かっこの両方を含む何らかのテキストを入力します。

    ```
    [
       Hello
    ]
    ```

4. 両方の角かっこを含むアウトライン領域が存在する必要があります。 左角かっこの左側にあるマイナス記号をクリックすると、アウトライン領域を折りたたむことができるはずです。 領域が折りたたまれているときには、折りたたまれた領域の左側に省略記号 ( *...* ) が表示されるはずです。また、ポインターを省略記号の上に移動すると、そのテキストの **ホバー テキスト** が含まれるポップアップが表示されるはずです。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
