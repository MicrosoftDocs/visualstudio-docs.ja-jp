---
title: エディターの内部
description: エディターのサブシステムと機能について説明します。 Visual Studio エディターの機能を拡張できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - architecture
ms.assetid: 822cbb8d-7ab4-40ee-bd12-44016ebcce81
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0bd45bb0a47de7283d75c083edc46b6fc38fe7d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079203"
---
# <a name="inside-the-editor"></a>エディターの内部

エディターはいくつかの異なるサブシステムで構成されています。これは、テキスト ビューとユーザー インターフェイスとは別にエディター テキスト モデルを保持するように設計されています。

以下のセクションでは、エディターのさまざまな特性について説明します。

- [サブシステムの概要](../extensibility/inside-the-editor.md#overview-of-the-subsystems)

- [テキスト モデル](../extensibility/inside-the-editor.md#the-text-model)

- [テキスト ビュー](../extensibility/inside-the-editor.md#the-text-view)

以下のセクションでは、エディターの機能について説明します。

- [タグと分類子](../extensibility/inside-the-editor.md#tags-and-classifiers)

- [表示要素](../extensibility/inside-the-editor.md#adornments)

- [射影](../extensibility/inside-the-editor.md#projection)

- [アウトライン](../extensibility/inside-the-editor.md#outlining)

- [マウス バインド](../extensibility/inside-the-editor.md#mouse-bindings)

- [エディターの操作](../extensibility/inside-the-editor.md#editor-operations)

- [IntelliSense](../extensibility/inside-the-editor.md#intellisense)

## <a name="overview-of-the-subsystems"></a>サブシステムの概要

### <a name="text-model-subsystem"></a>テキスト モデル サブシステム

テキスト モデル サブシステムは、テキストを表現し、その操作を有効にする役割を担います。 テキスト モデル サブシステムには、エディターによって表示される文字のシーケンスを記述する <xref:Microsoft.VisualStudio.Text.ITextBuffer> インターフェイスが含まれています。 このテキストは、さまざまな方法で変更、追跡、操作できます。 テキスト モデルでは、次の特性のタイプも提供されます。

- テキストをファイルに関連付け、ファイル システムでの読み取りと書き込みを管理するサービス。

- 2 つのオブジェクトのシーケンス間の最小限の違いを検出する差分サービス。

- 他のバッファー内のテキストのサブセットに関してバッファー内のテキストを記述するシステム。

テキスト モデル サブシステムは、ユーザー インターフェイス (UI) の概念に縛られていません。 たとえば、テキストの書式設定やテキスト レイアウトに関する役割はなく、テキストに関連付けられる視覚的な表示要素についての情報を持ちません。

テキスト モデル サブシステムのパブリック型は、*Microsoft.VisualStudio.Text.Data.dll* と *Microsoft.VisualStudio.CoreUtility.dll* に含まれています。これらは、.NET Framework 基本クラス ライブラリと Managed Extensibility Framework (MEF) にのみ依存しています。

### <a name="text-view-subsystem"></a>テキスト ビュー サブシステム

テキスト ビュー サブシステムは、テキストの書式設定と表示の役割を担います。 このサブシステムの種類は、種類が Windows Presentation Foundation (WPF) に依存しているかどうかに応じて、2 つのレイヤーに分割されます。 最も重要な種類は <xref:Microsoft.VisualStudio.Text.Editor.ITextView> と <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> です。これらによって、表示される一連のテキスト行、および WPF の UI 要素を使用してテキストを装飾するためのキャレット、選択、機能が制御されます。 また、このサブシステムでは、テキスト表示領域の周りに余白が提供されます。 これらの余白は拡張でき、さまざまな種類のコンテンツと視覚効果を含めることができます。 余白の例としては、行番号の表示とスクロール バーがあります。

テキスト ビュー サブシステムのパブリック型は、*Microsoft.VisualStudio.Text.UI.dll* と *Microsoft.VisualStudio.Text.UI.Wpf.dll* に含まれています。 最初のアセンブリにはプラットフォームに依存しない要素が含まれ、2 番目のアセンブリには WPF 固有の要素が含まれています。

### <a name="classification-subsystem"></a>分類サブシステム

分類サブシステムは、テキストのフォント プロパティを決定する役割を担います。 分類子によって、テキストが異なるクラス ("keyword" や "comment" など) に分割されます。 分類書式設定マップによって、これらのクラスが実際のフォント プロパティ ("Blue Consolas 10 pt" など) に関連付けられます。 この情報は、テキストを書式設定およびレンダリングするときにテキスト ビューによって使用されます。 タグ付け (このトピックで後で詳しく説明します) を使用すると、データをテキストの範囲に関連付けることができます。

分類サブシステムのパブリック型は、Microsoft.VisualStudio.Text.Logic.dll に含まれており、Microsoft.VisualStudio.Text.UI.Wpf.dll に含まれている分類の視覚的な特性とやり取りします。

### <a name="operations-subsystem"></a>操作サブシステム

操作サブシステムでは、エディターの動作が定義されます。 これにより、Visual Studio エディターのコマンドと「元に戻す」のシステムの実装が提供されます。

## <a name="a-closer-look-at-the-text-model-and-the-text-view"></a>テキスト モデルとテキスト ビューの詳細

### <a name="the-text-model"></a>テキスト モデル

テキスト モデル サブシステムは、さまざまなテキストの種類のグループで構成されます。 これらには、テキスト バッファー、テキスト スナップショット、テキスト範囲が含まれます。

#### <a name="text-buffers-and-text-snapshots"></a>テキスト バッファーとテキスト スナップショット

<xref:Microsoft.VisualStudio.Text.ITextBuffer> インターフェイスは、UTF-16 を使用してエンコードされた Unicode 文字のシーケンスを表します。UTF-16 は、.NET Framework の `String` 型によって使用されるエンコーディングです。 テキスト バッファーはファイル システム ドキュメントとして保持できますが、これは必須ではありません。

<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> は、空のテキスト バッファー、あるいは文字列または <xref:System.IO.TextReader> から初期化されたテキスト バッファーを作成するために使用されます。 テキスト バッファーは、<xref:Microsoft.VisualStudio.Text.ITextDocument> としてファイル システムに保持できます。

1 つのスレッドで <xref:Microsoft.VisualStudio.Text.ITextBuffer.TakeThreadOwnership%2A> を呼び出すことによってテキスト バッファーの所有権が取得されるまでは、すべてのスレッドでテキスト バッファーを編集できます。 その後は編集を実行できるのはそのスレッドのみです。

テキスト バッファーは、その有効期間中に多くのバージョンに変遷することがあります。 バッファーが編集されるたびに新しいバージョンが生成され、変更できない <xref:Microsoft.VisualStudio.Text.ITextSnapshot> はそのバージョンのバッファーの内容を表します。 テキスト スナップショットは不変であるため、それが表すテキスト バッファーが変化し続けている場合でも、任意のスレッドで制限なしにテキスト スナップショットにアクセスできます。

#### <a name="text-snapshots-and-text-snapshot-lines"></a>テキスト スナップショットとテキスト スナップショットの行

テキスト スナップショットの内容は、文字のシーケンスとして、または行のシーケンスとして表示できます。 文字と行にはどちらも 0 から始まるインデックスが作成されます。 空のテキスト スナップショットには、ゼロ個の文字と 1 つの空の行が含まれます。 行は、有効な Unicode 改行文字シーケンス、またはバッファーの先頭または末尾で区切られます。 改行文字はテキスト スナップショットで明示的に表され、テキスト スナップショット内の改行はすべて同じである必要はありません。

> [!NOTE]
> Visual Studio エディターの改行文字の詳細については、[エンコーディングと改行](../ide/encodings-and-line-breaks.md)に関する記事を参照してください。

1 行のテキストは <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> オブジェクトによって表されます。これは、特定の行番号または特定の文字位置のテキスト スナップショットから取得できます。

#### <a name="snapshotpoints-snapshotspans-and-normalizedsnapshotspancollections"></a>SnapshotPoint、Snapshotpoint、NormalizedSnapshotSpanCollection

<xref:Microsoft.VisualStudio.Text.SnapshotPoint> は、スナップショット内の文字位置を表します。 位置は、0 とスナップショットの長さの間であることが保証されます。 <xref:Microsoft.VisualStudio.Text.SnapshotSpan> は、スナップショット内のテキストの範囲を表します。 End の位置は、0 とスナップショットの長さの間であることが保証されます。 <xref:Microsoft.VisualStudio.Text.NormalizedSnapshotSpanCollection> は、同じスナップショットの一連の <xref:Microsoft.VisualStudio.Text.SnapshotSpan> オブジェクトで構成されます。

#### <a name="spans-and-normalizedspancollections"></a>Span と NormalizedSpanCollection

<xref:Microsoft.VisualStudio.Text.Span> は、テキスト スナップショット内のテキストの範囲に適用できる間隔を表します。 スナップショットの位置は 0 から始まるため、範囲は 0 を含む任意の位置から開始することができます。 範囲の `End` プロパティは、`Start` プロパティと `Length` プロパティの合計と等しくなります。 `Span` には、`End` プロパティによってインデックス付けされた文字は含まれません。 たとえば、Start = 5 および Length = 3 の範囲は End = 8 で、5、6、7 の位置の文字が含まれます。 この範囲の表記は [5..8) です。

任意の位置が共通である場合 (End の位置を含む)、2 つの範囲は交差しています。 このため、[3, 5) と [2, 7) の共通部分は [3, 5) であり、[3, 5) と [5, 7) の共通部分は [5, 5) です。 ([5, 5) は空の範囲であることに注意してください。)

共通する位置がある (End の位置を除く) 場合、2 つの範囲は重複しています。 空の範囲は他の範囲と重複することはないため、2 つの範囲の重複が空になることはありません。

<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> は、範囲の Start プロパティの順序での範囲のリストです。 このリストでは、重複する範囲または隣接する範囲がマージされます。 たとえば、範囲 [5..9)、[0..1)、[3..6)、[9..10) のセットがある場合、範囲の正規化されたリストは [0..1)、[3..10) になります。

#### <a name="itextedit-textversion-and-text-change-notifications"></a>ITextEdit、TextVersion、テキスト変更通知

テキスト バッファーの内容は、<xref:Microsoft.VisualStudio.Text.ITextEdit> オブジェクトを使用して変更できます。 (<xref:Microsoft.VisualStudio.Text.ITextBuffer> のいずれかの `CreateEdit()` メソッドを使用して) そのようなオブジェクトを作成すると、テキスト編集で構成されるテキスト トランザクションが開始されます。 すべての編集では、バッファー内のテキストの一部の範囲が文字列で置き換えられます。 すべての編集の座標と内容は、トランザクションの開始時のバッファーのスナップショットを基準にして表されます。 <xref:Microsoft.VisualStudio.Text.ITextEdit> オブジェクトでは、同じトランザクション内の他の編集によって影響を受ける編集の座標が調整されます。

たとえば、次の文字列を含むテキスト バッファーについて考えてみます。

```
abcdefghij
```

2 つの編集を含むトランザクションを適用します。1 番目の編集では文字 `X` を使用して [2..4) の範囲を置き換え、2 番目の編集では文字 `Y` を使用して [6..9) の範囲を置き換えます。 結果は次のバッファーになります。

```
abXefYj
```

2 番目の編集の座標は、最初の編集が適用される前に、トランザクションの開始時のバッファーの内容に対して計算されました。

バッファーへの変更は、<xref:Microsoft.VisualStudio.Text.ITextEdit> オブジェクトで `Apply()` メソッドを呼び出すことによってコミットされるときに有効になります。 空でない編集が少なくとも 1 つある場合は、新しい <xref:Microsoft.VisualStudio.Text.ITextVersion> が作成され、新しい <xref:Microsoft.VisualStudio.Text.ITextSnapshot> が作成されて、1 つの `Changed` イベントが発生します。 すべてのテキスト バージョンには、異なるテキスト スナップショットがあります。 テキスト スナップショットは編集トランザクションの後のテキスト バッファーの完全な状態を表しますが、テキスト バージョンにはあるスナップショットから次のスナップショットへの変更内容のみが記述されます。 一般に、テキスト スナップショットは一度だけ使用してから破棄するためのものですが、テキスト バージョンはしばらくの間は維持される必要があります。

テキスト バージョンには <xref:Microsoft.VisualStudio.Text.INormalizedTextChangeCollection> が含まれています。 このコレクションには、後続のスナップショットが生成される変更が (スナップショットに適用されるときに) 記述されます。 コレクション内のすべての <xref:Microsoft.VisualStudio.Text.ITextChange> には、変更の文字位置、置換された文字列、置換文字列が含まれています。 基本的な挿入では置き換えられる文字列は空であり、基本的な削除では置換文字列は空です。 正規化されたコレクションは、テキスト バッファーの最新バージョンでは常に `null` です。

テキスト バッファーに対してインスタンス化できる <xref:Microsoft.VisualStudio.Text.ITextEdit> オブジェクトは常に 1 つだけです。また、すべてのテキスト編集は、テキスト バッファーを所有しているスレッドで実行する必要があります (所有権が要求されている場合)。 テキストの編集は、その `Cancel` メソッドまたは `Dispose` メソッドを呼び出すことによって破棄できます。

また、<xref:Microsoft.VisualStudio.Text.ITextBuffer> では <xref:Microsoft.VisualStudio.Text.ITextEdit> インターフェイスにあるものに似た  `Insert()`、`Delete()`、`Replace()` の各メソッドも提供されます。 これらを呼び出すと、<xref:Microsoft.VisualStudio.Text.ITextEdit> オブジェクトを作成し、同様の呼び出しを行って、編集を適用するのと同じ効果があります。

#### <a name="tracking-points-and-tracking-spans"></a>追跡ポイントと追跡範囲

<xref:Microsoft.VisualStudio.Text.ITrackingPoint> は、テキスト バッファー内の文字位置を表します。 文字の位置をシフトするようにバッファーが編集されている場合、追跡ポイントはそれに従ってシフトします。 たとえば、追跡ポイントでバッファー内の位置 10 を参照していて、バッファーの先頭に 5 文字が挿入された場合、追跡ポイントでは位置 15 を参照するようになります。 追跡ポイントによって示される位置だけで挿入が行われる場合、その動作は <xref:Microsoft.VisualStudio.Text.PointTrackingMode> (`Positive` または `Negative` のいずれか) によって決まります。 追跡モードが Positive の場合、追跡ポイントでは (挿入の終わりにある) 同じ文字が参照されます。 追跡モードが Negative の場合、追跡ポイントでは元の位置に挿入された最初の文字が参照されます。 追跡ポイントによって表される位置にある文字が削除されると、追跡ポイントは削除された範囲の後の最初の文字にシフトします。 たとえば、追跡ポイントで位置 5 の文字を参照していて、位置 3 から 6 の文字が削除された場合、追跡ポイントでは位置 3 の文字を参照するようになります。

<xref:Microsoft.VisualStudio.Text.ITrackingSpan> は、1 つの位置だけではなく、文字の範囲を表します。 その動作は <xref:Microsoft.VisualStudio.Text.SpanTrackingMode> で決まります。 範囲追跡モードが [SpanTrackingMode.EdgeInclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeInclusive) の場合、追跡範囲は端に挿入されたテキストを取り込むように拡大されます。 範囲追跡モードが [SpanTrackingMode.EdgeExclusive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeExclusive) の場合、追跡範囲には端に挿入されたテキストは取り込まれません。 ただし、範囲追跡モードが [SpanTrackingMode.EdgePositive](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgePositive) の場合は、挿入によって現在位置が開始位置の方向にプッシュされます。範囲追跡モードが [SpanTrackingMode.EdgeNegative](xref:Microsoft.VisualStudio.Text.SpanTrackingMode.EdgeNegative) の場合は、挿入によって現在位置が終了位置の方向にプッシュされます。

(スナップショットが属する) テキスト バッファーのスナップショットの追跡ポイントの位置または追跡範囲の範囲を取得できます。 追跡ポイントと追跡範囲は、どのスレッドからでも安全に参照できます。

#### <a name="content-types"></a>コンテンツの種類

コンテンツの種類は、さまざまな種類のコンテンツを定義するためのメカニズムです。 コンテンツの種類は、"text"、"code"、"binary" などのファイルの種類や、"xml"、"vb"、"c#" などのテクノロジの種類にすることができます。 たとえば、"using" という単語は C# と Visual Basic の両方でキーワードですが、他のプログラミング言語ではそうではありません。 したがって、このキーワードの定義は、"c#" および "vb" のコンテンツの種類に限定されます。

コンテンツの種類は、エディターの表示要素およびその他の要素のフィルターとして使用されます。 エディターの多くの機能と拡張ポイントは、コンテンツの種類ごとに定義されます。 たとえば、テキストの色分けは、プレーンテキスト ファイル、XML ファイル、Visual Basic ソース コード ファイルで異なります。 通常、テキスト バッファーには作成時にコンテンツの種類が割り当てられ、テキスト バッファーのコンテンツの種類は変更できます。

コンテンツの種類は、他のコンテンツの種類から多重継承できます。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeDefinition> では、指定したコンテンツの種類の親として複数の基本の種類を指定できます。

開発者は、独自のコンテンツの種類を定義し、<xref:Microsoft.VisualStudio.Utilities.IContentTypeRegistryService> を使用して登録できます。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> を使用すると、特定のコンテンツの種類に対して多くのエディター機能を定義できます。 たとえば、エディターの余白、表示要素、マウス ハンドラーは、特定のコンテンツの種類を表示するエディターにのみ適用されるように定義できます。

### <a name="the-text-view"></a>テキスト ビュー

Model-View-Controller (MVC) パターンのビュー パーツでは、テキスト ビュー、ビューの書式設定、スクロール バーなどのグラフィック要素、キャレットを定義します。 Visual Studio エディターのすべてのプレゼンテーション要素は、WPF に基づいています。

#### <a name="text-views"></a>テキスト ビュー

<xref:Microsoft.VisualStudio.Text.Editor.ITextView> インターフェイスは、プラットフォームに依存しないテキスト ビューの表現です。 これは主にテキスト ドキュメントをウィンドウに表示するために使用されますが、他の目的 (ツールヒントなど) でも使用できます。

テキスト ビューでは、さまざまな種類のテキスト バッファーが参照されます。 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.TextViewModel%2A> プロパティでは、3 つの異なるテキスト バッファーを指す <xref:Microsoft.VisualStudio.Text.Editor.ITextViewModel> オブジェクトを参照します。それらは、最上位のデータレベル バッファーであるデータ バッファー、編集が行われる編集バッファー、テキスト ビューに表示されるバッファーであるビジュアル バッファーです。

テキストは、基になるテキスト バッファーに関連付けられている分類子に基づいて書式設定され、テキスト ビュー自体に関連付けられている表示要素プロバイダーを使用して装飾されます。

#### <a name="the-text-view-coordinate-system"></a>テキスト ビューの座標系

テキスト ビューの座標系によって、テキスト ビュー内の位置が指定されます。 この座標系では、x 値 0.0 は表示されるテキストの左端に対応し、y 値 0.0 は表示されるテキストの上端に対応します。 x 座標は左から右に増加し、y 座標は上から下に増加します。

ビューポート (テキスト ウィンドウに表示されるテキストの一部) は、垂直方向にスクロールさせるのと同じ方法で水平方向にスクロールさせることはできません。 ビューポートは、描画サーフェイスに合わせて移動するように左の座標を変更することで、水平方向にスクロールされます。 ただし、ビューポートは、レンダリングされるテキストを変更することによってのみ垂直方向にスクロールできます。これにより <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> イベントが発生します。

座標系の距離は、論理ピクセルに対応します。 テキスト レンダリング サーフェイスがスケーリング変換なしで表示される場合、テキスト レンダリングの座標系の 1 単位が、ディスプレイの 1 ピクセルに対応します。

#### <a name="margins"></a>余白

<xref:Microsoft.VisualStudio.Text.Editor.ITextViewMargin> インターフェイスは、余白を表し、余白の可視性とそのサイズを制御できます。 定義済みの余白が 4 つあります。それらは、"Top"、"Bottom"、"Left"、"Right" という名前で、ビューの上、下、左、または右の端に関連付けられています。 これらの余白は、他の余白を配置できるコンテナーです。 インターフェイスには、余白のサイズと余白の可視性を返すメソッドが定義されます。 余白は、関連付けられているテキスト ビューに関する追加情報を提供するビジュアル要素です。 たとえば、行番号の余白にはテキスト ビューの行番号が表示されます。 グリフの余白には UI 要素が表示されます。

<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewMarginProvider> インターフェイスによって、余白の作成と配置が処理されます。 余白は、他の余白に対して順序付けることができます。 優先順位の高い余白は、テキスト ビューの近くに配置されます。 たとえば、左余白が 2 つあり (余白 A と余白 B)、余白 B の優先順位が余白 A より低い場合、余白 B は余白 A の左側に表示されます。

#### <a name="the-text-view-host"></a>テキスト ビューのホスト

<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> インターフェイスには、テキスト ビューと、ビューに付随するすべての隣接する装飾 (スクロール バーなど) が含まれています。 テキスト ビューのホストには、ビューの境界線に関連付けられる余白も含まれています。

#### <a name="formatted-text"></a>書式付きテキスト

テキスト ビューに表示されるテキストは、<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> オブジェクトで構成されます。 すべてのテキスト ビュー行は、テキスト ビュー内の 1 行のテキストに対応します。 基になるテキスト バッファー内の長い行は、部分的に隠されるか (ワード ラップが有効ではない場合)、テキスト ビューの複数の行に分割される場合があります。 <xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> インターフェイスには、座標と文字の間のマッピング、およびその行に関連付けられる可能性のある表示要素のメソッドとプロパティが含まれています。

<xref:Microsoft.VisualStudio.Text.Formatting.ITextViewLine> オブジェクトは、<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> インターフェイスを使用して作成されます。 現在ビューに表示されるテキストのみに関心がある場合は、ソースの書式設定を無視できます。 ビューに表示されないテキストの書式設定に関心がある場合 (リッチテキストの切り取りと貼り付けをサポートする場合など) は、<xref:Microsoft.VisualStudio.Text.Formatting.IFormattedLineSource> を使用してテキスト バッファー内のテキストを書式設定できます。

テキスト ビューでは、一度に 1 つの <xref:Microsoft.VisualStudio.Text.ITextSnapshotLine> が書式設定されます。

## <a name="editor-features"></a>エディターの機能

エディターの機能は、機能の定義が実装と分離されるように設計されています。 エディターには、次の機能が含まれています。

- タグと分類子

- 表示要素

- Projection

- アウトライン

- マウスとキーのバインド

- 操作とプリミティブ

- IntelliSense

### <a name="tags-and-classifiers"></a>タグと分類子

タグは、テキストの範囲に関連付けられたマーカーです。 たとえば、テキストの色分け、下線、グラフィックス、ポップアップなどを使用して、さまざまな方法で表示できます。 分類子はタグの一種です。

他の種類のタグには、テキストの強調表示用の <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>、アウトライン表示用の <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>、コンパイル エラー用の <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> があります。

#### <a name="classification-types"></a>分類の種類

<xref:Microsoft.VisualStudio.Text.Classification.IClassificationType> インターフェイスは、テキストの抽象カテゴリである同等クラスを表します。 分類の種類は、他の分類の種類から多重継承できます。 たとえば、プログラミング言語の分類には、"keyword"、"comment"、"identifier" などがありますが、これらはすべて "code" から継承されます。 自然言語の分類の種類には、"noun"、"verb"、"adjective" などがありますが、これらはすべて "natural language" から継承されます。

#### <a name="classifications"></a>分類

分類は、特定の分類の種類のインスタンスであり、通常はテキストの範囲を超えています。 <xref:Microsoft.VisualStudio.Text.Classification.ClassificationSpan> は、分類を表すために使用されます。 分類範囲は、特定のテキスト範囲をカバーするラベルと考えることができ、このテキストの範囲が特定の分類の種類であることがシステムに通知されます。

#### <a name="classifiers"></a>分類子

<xref:Microsoft.VisualStudio.Text.Classification.IClassifier> は、テキストを一連の分類に分割するメカニズムです。 分類子は、特定のコンテンツの種類に対して定義し、特定のテキスト バッファー用にインスタンス化する必要があります。 テキスト分類に参加するには、クライアントで <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> を実装する必要があります。

#### <a name="classifier-aggregators"></a>分類子アグリゲーター

分類子アグリゲーターは、1 つのテキスト バッファーのすべての分類子を 1 つの分類セットにまとめるメカニズムです。 たとえば、C# の分類子と英語の分類子の両方で、C# ファイル内のコメントに対して分類を作成できます。 次のコメントについて考えてみます。

```
// This method produces a classifier
```

C# の分類子では、範囲全体にコメントとしてラベルを付けることができます。また、英語の分類子では、"produces" を "verb" として、"method" を "noun" として分類できます。 アグリゲーターでは一連の重複しない分類が生成され、一連の種類はすべての寄与に基づいています。

分類子アグリゲーターでは、テキストが一連の分類に分割されるため、分類器でもあります。 また、分類子アグリゲーターを使用すると、重複する分類がなく、分類が並べ替えられることが保証されます。 個々の分類子は、一連の任意の分類を任意の順序で返し、何らかの形で重複することができます。

#### <a name="classification-formatting-and-text-coloring"></a>分類の書式設定とテキストの色分け

テキストの書式設定は、テキスト分類に基づいて作成された機能の一例です。 これは、テキスト ビュー レイヤーによって、アプリケーションでのテキストの表示を決定するために使用されます。 テキストの書式設定領域は WPF に依存していますが、分類の論理定義は異なります。

分類の書式設定は、特定の分類の種類に対する一連の書式設定プロパティです。 これらの書式設定は、分類の種類の親の書式設定から継承されます。

<xref:Microsoft.VisualStudio.Text.Classification.IClassificationFormatMap> は、分類の種類から一連のテキスト書式設定プロパティへのマップです。 エディターに書式設定マップを実装することによって、分類の書式設定のすべてのエクスポートが処理されます。

### <a name="adornments"></a>表示要素

表示要素は、テキスト ビュー内の文字のフォントと色に直接関係しないグラフィック効果です。 たとえば、多くのプログラミング言語でコンパイルされないコードをマークするために使用される赤い波線の下線は埋め込まれた表示要素であり、ツールヒントはポップアップ表示要素です。 表示要素は <xref:System.Windows.UIElement> から派生し、<xref:Microsoft.VisualStudio.Text.Tagging.ITag> が実装されます。 表示要素タグの 2 つの特殊な種類には、ビュー内のテキストと同じスペースを占有する表示要素のための <xref:Microsoft.VisualStudio.Text.Tagging.SpaceNegotiatingAdornmentTag>、および波線の下線のための <xref:Microsoft.VisualStudio.Text.Tagging.ErrorTag> があります。

埋め込み表示要素は、書式設定されたテキスト ビューの一部を形成するグラフィックスです。 これらは、さまざまな Z オーダー レイヤーに編成されます。 テキスト、キャレット、選択の 3 つの組み込みレイヤーがあります。 ただし、開発者はさらにレイヤーを定義し、相対的な順序で配置することができます。 埋め込み表示要素の 3 種類は、テキスト相対表示要素 (テキストが移動されると移動され、テキストが削除されると削除されます)、ビュー相対表示要素 (ビューのテキスト以外の部分に関係しています)、所有者制御の表示要素 (開発者が配置を管理する必要があります) です。

ポップアップ表示要素は、テキスト ビューの上に小さなウィンドウで表示されるグラフィックスです (ツールヒントなど)。

### <a name="projection"></a><a name="projection"></a> 投影

投影は、実際にテキストを格納しないが他のテキスト バッファーのテキストを結合する、別の種類のテキスト バッファーを作成するための手法です。 たとえば、投影バッファーは、他の 2 つのバッファーのテキストを連結して 1 つのバッファーにあるかのように結果を表したり、1 つのバッファー内のテキストの一部を非表示にしたりするために使用できます。 投影バッファーは、別の投影バッファーへのソース バッファーとして機能することができます。 投影によって関連付けられた一連のバッファーを作成して、さまざまな方法でテキストを再配置することができます。 (このようなセットは、"*バッファー グラフ*" とも呼ばれます)。Visual Studio のテキスト アウトライン機能は、折りたたまれたテキストを非表示にするために、投影バッファーを使用して実装されます。また、ASP.NET ページの Visual Studio エディターでは、投影を使用して Visual Basic や C# などの埋め込み言語がサポートされています。

<xref:Microsoft.VisualStudio.Text.Projection.IProjectionBuffer> は <xref:Microsoft.VisualStudio.Text.Projection.IProjectionBufferFactoryService> を使用して作成されます。 投影バッファーは、"*ソース範囲*" と呼ばれる順序付けられた <xref:Microsoft.VisualStudio.Text.ITrackingSpan> オブジェクトのシーケンスによって表されます。 これらの範囲の内容は、文字のシーケンスとして表されます。 ソース範囲が取り出されるテキスト バッファーには、"*ソース バッファー*" という名前が付けられます。 投影バッファーのクライアントは、通常のテキスト バッファーと異なることを認識している必要はありません。

投影バッファーでは、ソース バッファーのテキスト変更イベントをリッスンします。 ソース範囲内のテキストが変更されると、投影バッファーでは、変更されたテキストの座標を独自の座標にマップし、適切なテキスト変更イベントを発生させます。 たとえば、次の内容を持つソース バッファー A と B について考えてみます。

```
A: ABCDE
B: vwxyz
```

投影バッファー P が 2 つのテキスト範囲 (1 つはバッファー A のすべてで、もう 1 つはバッファー B のすべて) から形成されている場合、P の内容は次のようになります。

```
P: ABCDEvwxyz
```

部分文字列 `xy` がバッファー B から削除されると、バッファー P によって、位置 7 と 8 の文字が削除されたことを示すイベントが生成されます。

また、投影バッファーを直接編集することもできます。 適切なソース バッファーに編集が伝搬されます。 たとえば、文字列がバッファー P の位置 6 (文字 "v" の元の位置) に挿入される場合、挿入はバッファー B の位置 1 に伝搬されます。

投影バッファーに寄与するソース範囲には制限があります。 ソース範囲は重複することはできません。投影バッファー内の位置を、ソース バッファー内の複数の位置にマップすることはできません。また、ソース バッファー内の位置を、投影バッファー内の複数の位置にマップすることはできません。 ソース バッファーとの関係では、循環は許可されません。

イベントが発生するのは、投影バッファーのソース バッファーのセットが変更されたときと、ソース範囲のセットが変更されたときです。
省略バッファーは、特別な種類の投影バッファーです。 これは主に、アウトライン処理と、テキストのブロックの展開と折りたたみを行う操作に使用されます。 省略バッファーは、1 つのソース バッファーのみに基づいています。省略バッファー内の範囲は、ソース バッファーで順序付けられているのと同じ順序にする必要があります。

#### <a name="the-buffer-graph"></a>バッファー グラフ

<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraph> インターフェイスを使用すると、投影バッファーのグラフ間でマッピングを行うことができます。 すべてのテキスト バッファーと投影バッファーは、言語コンパイラによって生成される抽象構文ツリーと同様に、有向非巡回グラフで収集されます。 このグラフは、上位バッファーによって定義されます。このバッファーには、任意のテキスト バッファーを使用できます。 バッファー グラフでは、上位バッファー内のポイントからソース バッファー内のポイントに、または上部バッファー内の範囲からソース バッファー内の一連の範囲にマップできます。 同様に、ソース バッファーのポイントまたは範囲から上位バッファー内のポイントにマップすることができます。 バッファー グラフは、<xref:Microsoft.VisualStudio.Text.Projection.IBufferGraphFactoryService> を使用して作成されます。

#### <a name="events-and-projection-buffers"></a>イベントと投影バッファー

投影バッファーを変更すると、その変更が投影バッファーからそれに依存するバッファーに送信されます。 すべてのバッファーが変更されると、バッファー変更イベントが発生します。これは、最も深いバッファーから開始されます。

### <a name="outlining"></a>アウトライン

アウトラインは、テキスト ビュー内のさまざまなテキストのブロックの展開または折りたたみを行う機能です。 アウトラインは、表示要素を定義する場合と同様に、<xref:Microsoft.VisualStudio.Text.Tagging.ITag> の一種として定義します。 <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> は、展開または折りたたみが可能なテキスト領域を定義するタグです。 アウトラインを使用するには、<xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManagerService> をインポートして <xref:Microsoft.VisualStudio.Text.Outlining.IOutliningManager> を取得する必要があります。 アウトライン マネージャーでは、<xref:Microsoft.VisualStudio.Text.Outlining.ICollapsible> オブジェクトとして表されるさまざまなブロックを列挙、折りたたみ、展開し、それに応じてイベントを発生させます。

### <a name="mouse-bindings"></a>マウス バインド

マウス バインドによって、マウスの移動がさまざまなコマンドにリンクされます。 マウス バインドは <xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessorProvider> を使用して定義し、キー バインドは <xref:Microsoft.VisualStudio.Text.Editor.IKeyProcessorProvider> を使用して定義します。 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewHost> によって、すべてのバインドが自動的にインスタンス化され、ビュー内のマウス イベントに接続されます。

<xref:Microsoft.VisualStudio.Text.Editor.IMouseProcessor> インターフェイスには、さまざまなマウス イベントの処理前および処理後のイベント ハンドラーが含まれています。 いずれかのイベントを処理するには、<xref:Microsoft.VisualStudio.Text.Editor.MouseProcessorBase> の一部のメソッドをオーバーライドできます。

### <a name="editor-operations"></a>エディターの操作

エディターの操作は、スクリプトやその他の目的で、エディターでの操作を自動化するために使用できます。 <xref:Microsoft.VisualStudio.Text.Operations.IEditorOperationsFactoryService> をインポートして、指定された <xref:Microsoft.VisualStudio.Text.Editor.ITextView> に対する操作にアクセスできます。 その後、これらのオブジェクトを使用して、選択の変更、ビューのスクロールを行ったり、キャレットをビューのさまざまな部分に移動したりすることができます。

### <a name="intellisense"></a>IntelliSense

IntelliSense では、ステートメント入力候補、シグネチャ ヘルプ (パラメーター ヒントとも呼ばれます)、クイック ヒント、および電球アイコンがサポートされています。

ステートメント入力候補では、メソッド名、XML 要素、その他のコーディング要素やマークアップ要素に対して潜在的な入力候補のポップアップ リストが表示されます。 一般に、ユーザーのジェスチャによって、入力候補セッションが呼び出されます。 このセッションでは、潜在的な入力候補の一覧が表示されます。ユーザーは 1 つ選択するか、一覧を無視することができます。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> は、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSession> を作成およびトリガーする役割を担います。 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> によって、セッションの入力候補項目の <xref:Microsoft.VisualStudio.Language.Intellisense.CompletionSet> が計算されます。

## <a name="see-also"></a>関連項目

- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
- [エディターのインポート](../extensibility/editor-imports.md)
