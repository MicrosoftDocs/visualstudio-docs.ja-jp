---
title: 'チュートリアル: 余白のグリフの作成 | Microsoft Docs'
description: このチュートリアルでは、カスタム エディター拡張機能を使用してエディターの余白の外観をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ec5eecef40220c2cf2d4e3f1ece8eb5eb763bdeb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217412"
---
# <a name="walkthrough-create-a-margin-glyph"></a>チュートリアル: 余白のグリフを作成する
カスタム エディター拡張機能を使用して、エディターの余白の外観をカスタマイズできます。 このチュートリアルでは、コード コメントに "todo" という単語が表れるたびに、インジケーターの余白にカスタム グリフを配置します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します。) ソリューションに `TodoGlyphTest` という名前を付けます。

2. エディター分類子のプロジェクト項目を追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-the-glyph"></a>グリフを定義する
 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> インターフェイスを実行してグリフを定義します。

### <a name="to-define-the-glyph"></a>グリフを定義するには

1. クラス ファイルを追加し、その名前を `TodoGlyphFactory`にします。

2. 宣言を使用して次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet1":::

3. <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> を実装する、`TodoGlyphFactory` という名前のクラスを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet2":::

4. グリフのディメンションを定義するプライベート フィールドを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet3":::

5. グリフのユーザー インターフェイス (UI) 要素を定義して、`GenerateGlyph` を実装します。 `TodoTag` については、このチュートリアルで後ほど定義します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet4":::

6. <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider> を実装する、`TodoGlyphFactoryProvider` という名前のクラスを追加します。 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> として "TodoGlyph"、<xref:Microsoft.VisualStudio.Utilities.OrderAttribute> として After VsTextMarker、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "code"、<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> として TodoTag を指定して、このクラスをエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet5":::

7. `TodoGlyphFactory` をインスタンス化することで <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A> メソッドを実装します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet6":::

## <a name="define-a-todo-tag-and-tagger"></a>Todo タグとタガーを定義する
 以前の手順で定義した UI 要素とインジケーター マージンとの間の関係を定義します。 タグの種類とタガーを作成し、それを、タガー プロバイダーを使用してエクスポートします。

### <a name="to-define-a-todo-tag-and-tagger"></a>Todo タグとタガーを定義するには

1. 新しいクラス ファイルをプロジェクトに追加し、`TodoTagger` という名前を付けます。

2. 次のインポートを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet7":::

3. `TodoTag`という名前のクラスを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet8":::

4. `TodoTag` 型の <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> を実装する、`TodoTagger` という名前のクラスを変更します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet9":::

5. `TodoTagger` クラスに対して、<xref:Microsoft.VisualStudio.Text.Classification.IClassifier> と、分類範囲内で検索するテキストのためのプライベート フィールドを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet10":::

6. 分類子を設定するコンストラクターを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet11":::

7. その名前に "comment" という単語が含まれていて、そのテキストに検索テキストが含まれているすべての分類範囲を検索することで、<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> メソッドを実装します。 検索テキストが見つかるたびに、`TodoTag` 型の新しい <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> が返されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet12":::

8. `TagsChanged` イベントを宣言します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet13":::

9. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> を実装する、`TodoTaggerProvider` という名前のクラスを追加し、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> として "code"、<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> として TodoTag を指定してそれをエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet14":::

10. <xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService> をインポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet15":::

11. `TodoTagger` をインスタンス化することで <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A> メソッドを実装します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet16":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、TodoGlyphTest ソリューションをビルドし、それを実験用インスタンスで実行します。

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>TodoGlyphTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. **F5** キーを押してプロジェクトを実行します。 Visual Studio の 2 番目のインスタンスが開始されます。

3. インジケーター マージンが表示されていることを確認します。 ( **[ツール]** メニューの **[オプション]** をクリックします。 **[テキスト エディター]** ページで、 **[インジケーター マージン]** が選択されていることを確認します。)

4. コメントが含まれているコード ファイルを開きます。 コメント セクションの 1 つに "todo" という単語を追加します。

5. コード ウィンドウの左側のインジケーター マージンに、濃い青の輪郭の付いた薄い青の円が表示されます。
