---
title: コンテンツ タイプとファイル名拡張子とをリンクさせる
description: このチュートリアルでは、エディター Managed Extensibility Framework 拡張機能を使用して、独自のコンテンツ タイプとファイル名拡張子とをリンクさせる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link content type to file name extension
ms.assetid: 21ee64ce-9afe-4b08-94a0-8389cc4dc67c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 990f10fe82b9230c12ba13d736750f2f644c3ee5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078449"
---
# <a name="walkthrough-link-a-content-type-to-a-file-name-extension"></a>チュートリアル: コンテンツ タイプとファイル名拡張子とをリンクさせる
エディター Managed Extensibility Framework (MEF) 拡張機能を使用して、独自のコンテンツ タイプを定義し、ファイル名拡張子をリンクさせることができます。 場合によっては、ファイル名拡張子が言語サービスによって既に定義されていることがあります。 ただし、これを MEF で使用するには、コンテンツ タイプにリンクさせる必要があります。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します。) ソリューションに `ContentTypeTest` という名前を付けます。

2. **Source.extension.vsixmanifest** ファイルで、 **[資産]** タブにアクセスし、 **[種類]** フィールドを **[Microsoft.VisualStudio.MefComponent]** に、 **[ソース]** フィールドを **[現在のソリューション内のプロジェクト]** に、 **[プロジェクト]** フィールドをプロジェクトの名前に設定します。

## <a name="define-the-content-type"></a>コンテンツ タイプを定義する

1. クラス ファイルを追加し、その名前を `FileAndContentTypes`にします。

2. 次のアセンブリへの参照を追加します。

    1. System.ComponentModel.Composition

    2. Microsoft.VisualStudio.Text.Logic

    3. Microsoft.VisualStudio.CoreUtility

3. 次の `using` ディレクティブを追加します。

    ```csharp
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text.Classification;
    using Microsoft.VisualStudio.Utilities;

    ```

4. 定義を含む静的クラスを宣言します。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {. . .}
    ```

5. このクラスでは、"hid" という名前の <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> をエクスポートし、その基本定義を "text" として宣言します。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
        [Export]
        [Name("hid")]
        [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;
    }
    ```

## <a name="link-a-file-name-extension-to-a-content-type"></a>ファイル名拡張子とコンテンツ タイプとをリンクさせる

- このコンテンツ タイプをファイル名拡張子にマップするには、拡張子が *hid* でコンテンツ タイプが "hid" の <xref:Microsoft.VisualStudio.Utilities.FileExtensionToContentTypeDefinition> をエクスポートします。

    ```csharp
    internal static class FileAndContentTypeDefinitions
    {
         [Export]
         [Name("hid")]
         [BaseDefinition("text")]
        internal static ContentTypeDefinition hidingContentTypeDefinition;

         [Export]
         [FileExtension(".hid")]
         [ContentType("hid")]
        internal static FileExtensionToContentTypeDefinition hiddenFileExtensionDefinition;
    }
    ```

## <a name="add-the-content-type-to-an-editor-export"></a>コンテンツ タイプをエディター エクスポートに追加する

1. エディター拡張機能を作成します。 たとえば、「[チュートリアル: 余白のグリフの作成](../extensibility/walkthrough-creating-a-margin-glyph.md)」で説明されている余白のグリフ拡張機能を使用できます。

2. この手順で定義したクラスを追加します。

3. 拡張クラスをエクスポートするときに、タイプが "hid" の <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> をそれに追加します。

    ```csharp
    [Export]
    [ContentType("hid")]
    ```

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
