---
title: 'チュートリアル: テキスト ビューのカスタマイズ | Microsoft Docs'
description: このチュートリアルでは、エディター書式マップでいくつかのプロパティを変更して、テキスト ビューをカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5ef4d0b408afc00a806e73d1e2eae7a07dde7814
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216853"
---
# <a name="walkthrough-customize-the-text-view"></a>チュートリアル: テキスト ビューのカスタマイズ
テキスト ビューをカスタマイズするには、次の任意のプロパティをエディター書式マップで変更します。

- インジケーター マージン

- 挿入キャレット

- 上書きキャレット

- 選択されたテキスト

- 非アクティブの選択されたテキスト (フォーカスが失われたテキスト)

- 可視空白

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールすることはしません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[Visual C#]、[拡張機能]** 、 **[VSIX プロジェクト]** の順に選択します)。ソリューションに `ViewPropertyTest` という名前を付けます。

2. プロジェクトに、[エディター分類子] 項目テンプレートを追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-the-content-type"></a>コンテンツ タイプを定義する

1. クラス ファイルを追加し、その名前を `ViewPropertyModifier`にします。

2. 次の `using` ディレクティブを追加します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet1":::

3. <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> から継承する `TestViewCreationListener` というクラスを宣言します。 次の属性を使って、このクラスをエクスポートします。

   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>: このリスナーが適用されるコンテンツの種類を指定します。

   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>: このリスナーのロールを指定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet2":::

4. このクラスで、<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> をインポートします。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet3":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet3":::

## <a name="change-the-view-properties"></a>ビューのプロパティを変更する

1. ビューを開いたときにビューのプロパティが変更されるように、<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> メソッドを設定します。 この変更を行うには、まず、目的のビュー特性に対応する <xref:System.Windows.ResourceDictionary> を探します。 次に、リソース ディクショナリで適切なプロパティを変更し、プロパティを設定します。 プロパティを設定する前に <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> メソッドを呼び出し、プロパティを設定した後に <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> を呼び出すことで、<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A> メソッドへの呼び出しをバッチ処理します。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet4":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet4":::

## <a name="build-and-test-the-code"></a>コードのビルドとテスト

1. ソリューションをビルドします。

     デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが開始されます。

2. テキスト ファイルを作成し、いくつかのテキストを入力します。

    - 挿入キャレットはマゼンタ、上書きキャレットは水色になります。

    - インジケーター マージン (テキスト ビューの左側) は、薄い緑になります。

3. 入力したテキストを選択します。 選択したテキストの色が、薄いピンクになります。

4. テキストが選択された状態で、テキスト ウィンドウの外側の任意の場所をクリックします。 選択したテキストの色が、濃いピンクになります。

5. 可視空白を有効にします ( **[編集]** メニューの **[詳細設定]** をポイントし、 **[スペースの表示]** をクリックします)。 テキストにいくつかのタブを入力します。 タブを表す赤い矢印が表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
