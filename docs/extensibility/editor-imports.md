---
title: エディターのインポート | Microsoft Docs
description: コア エディターへのさまざまな種類のアクセスを使用して、拡張機能を提供するエディター サービス、ファクトリ、およびブローカーをインポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - services
ms.assetid: 8d096de3-33b4-427a-a122-4aeff8a72da0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0587ed6487ec3a1bb833a804bb5ffa76cbc101f9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070155"
---
# <a name="editor-imports"></a>エディターのインポート
コア エディターへのさまざまな種類のアクセスを使用して、拡張機能を提供する多数のエディター サービス、ファクトリ、およびブローカーをインポートできます。 たとえば、<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> をインポートして、特定のコンテンツ タイプの <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> を提供できます (このナビゲーターを使用すると、テキスト バッファーに対してさまざまな種類の検索を実行できます)。

 エディターのインポートを使用するには、Managed Extensibility Framework コンポーネント パーツをエクスポートするクラスのフィールドまたはプロパティとしてインポートします。

> [!NOTE]
> Managed Extensibility Framework の詳細については、「[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)」を参照してください。

## <a name="import-syntax"></a>インポート構文
 次の例は、エディター オプションのファクトリ サービスをインポートする方法を示しています。

```
[Import]
internal IEditorOptionsFactoryService EditorOptions { get; set; }
```

 サービスをプロパティではなくフィールドとしてインポートする場合は、変数に割り当てられていないことに関するコンパイラの警告が表示されないように、宣言で `null` に設定する必要があります。

```
[Import]
internal IEditorOptionsFactoryService m_editorOptions = null;
```

 インポートを使用するその他の例については、次のチュートリアルを参照してください。

- [チュートリアル: 余白のグリフを作成する](../extensibility/walkthrough-creating-a-margin-glyph.md)

- [チュートリアル: テキスト ビューのカスタマイズ](../extensibility/walkthrough-customizing-the-text-view.md)

- [チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)

- [チュートリアル: QuickInfo ツールヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)

- [チュートリアル: シグネチャ ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)

- [チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)

- [チュートリアル: 電球アイコンによる提案の表示](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)

## <a name="import-the-service-provider"></a>サービス プロバイダーをインポートする
 同じ方法で (アセンブリ Microsoft.VisualStudio.Shell.Immutable.10.0 内にある) <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> をインポートして、Visual Studio サービスへのアクセスを取得することもできます。

```csharp
[Import]
internal SVsServiceProvider ServiceProvider = null;
```

 詳細については、「[チュートリアル: エディター拡張機能から DTE オブジェクトにアクセスする](../extensibility/walkthrough-accessing-the-dte-object-from-an-editor-extension.md)」を参照してください。

## <a name="services"></a>サービス
 通常、エディター サービスはサービスを提供する 1 つのエンティティであり、複数のコンポーネント間で共有されます。

|[インポート]|提供内容|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Utilities.IFileExtensionRegistryService>|ファイル拡張子と <xref:Microsoft.VisualStudio.Utilities.IContentType> オブジェクトの間のリレーションシップ。|
|<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> オブジェクトのコレクション。|
|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformationService>|<xref:Microsoft.VisualStudio.Editor.IVsFontsAndColorsInformation> オブジェクト。|
|<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>|多くのエディター アダプター オブジェクト:<br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|
|<xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearchFactoryService>|指定されたテキスト ビューの <xref:Microsoft.VisualStudio.Text.IncrementalSearch.IIncrementalSearch> オブジェクト。|
|<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextBuffer>。|
|<xref:Microsoft.VisualStudio.Text.ITextDocumentFactoryService>|<xref:Microsoft.VisualStudio.Text.ITextDocument>。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceService>|相違点の <xref:Microsoft.VisualStudio.Text.Differencing.IDifferenceCollection%601>。|
|<xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalStringDifferenceService>|相違点の <xref:Microsoft.VisualStudio.Text.Differencing.IHierarchicalDifferenceCollection>。|
|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService>|<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> または <xref:Microsoft.VisualStudio.Text.Projection.IElisionBuffer>。|
|<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService>|一連の <xref:Microsoft.VisualStudio.Text.ITextBuffer> オブジェクトの <xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph>。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>|<xref:Microsoft.VisualStudio.Text.ITextBuffer> の <xref:Microsoft.VisualStudio.Text.Classification.IClassifier>。|
|<xref:Microsoft.VisualStudio.Text.Classification.IViewClassifierAggregatorService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Classification.IClassifier>。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMapService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap>。|
|<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap>。|
|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService>|<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> オブジェクトのコレクションを保持します。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IBufferTagAggregatorFactoryService>|テキスト バッファーの <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>。|
|<xref:Microsoft.VisualStudio.Text.Tagging.IViewTagAggregatorFactoryService>|テキスト ビューの <xref:Microsoft.VisualStudio.Text.Tagging.ITagAggregator%601>。|
|<xref:Microsoft.VisualStudio.Text.Editor.IEditorOptionsFactoryService>|指定したスコープの <xref:Microsoft.VisualStudio.Text.Editor.IEditorOptions>。|
|<xref:Microsoft.VisualStudio.Text.Editor.IScrollMapFactoryService>|テキスト ビューの <xref:Microsoft.VisualStudio.Text.Editor.IScrollMap>。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Editor.ISmartIndent>。|
|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentationService>|<xref:Microsoft.VisualStudio.Text.Editor.ISmartIndentProvider> オブジェクトを使用して自動インデントを取得します。|
|<xref:Microsoft.VisualStudio.Text.Editor.ITextEditorFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> の <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> を管理します。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedTextSourceFactoryService>|<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.IRtfBuilderService>|一連のスナップショット スパンから RTF 形式のテキストを生成します。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencerFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Formatting.ITextAndAdornmentSequencer>。|
|<xref:Microsoft.VisualStudio.Text.Formatting.ITextParagraphPropertiesFactoryService>|ビュー内のテキスト行を書式設定するための <xref:System.Windows.Media.TextFormatting.TextParagraphProperties>。|
|<xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperations> オブジェクト。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextSearchService>|テキスト スナップショットを検索します。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>|<xref:Microsoft.VisualStudio.Utilities.IContentType> による <xref:Microsoft.VisualStudio.Text.ITextBuffer> の <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>。|
|<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService>|テキスト ビューの <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IGlyphService>|グリフの標準セット。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStackMapService>|<xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSessionStack>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IWpfKeyboardTrackingService>|キーボード処理を追跡します。|
|<xref:Microsoft.VisualStudio.Language.StandardClassification.IStandardClassificationService>|標準 <xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> オブジェクト。|
|<xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistoryRegistry>|テキスト バッファーと <xref:Microsoft.VisualStudio.Text.Operations.ITextUndoHistory> オブジェクトの間のリレーションシップを維持します。|

## <a name="other-imports"></a>その他のインポート
 プロバイダー ファクトリとブローカーは、通常、複数のコンポーネントに複数のインスタンスを持つことができるエンティティです。

|[インポート]|提供内容|
|------------|--------------|
|<xref:Microsoft.VisualStudio.Text.Adornments.IErrorProviderFactory>|指定されたバッファーの型 <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag>) の <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601>。|
|<xref:Microsoft.VisualStudio.Text.Adornments.ITextMarkerProviderFactory>|テキスト マーカー タガー (型 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> の <xref:Microsoft.VisualStudio.Text.Tagging.SimpleTagger%601>)。|
|<xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProviderFactory>|指定された <xref:Microsoft.VisualStudio.Text.Editor.ITextView> の <xref:Microsoft.VisualStudio.Text.Adornments.IToolTipProvider>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSession>。|
|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>|<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSession>。|

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
