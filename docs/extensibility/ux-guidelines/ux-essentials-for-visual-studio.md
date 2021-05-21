---
title: UX Essentials for Visual Studio | Microsoft Docs
description: 画面解像度の認識も含め、Visual Studio 向けに開発する新機能に関してこれらのユーザー エクスペリエンスのベスト プラクティスを確認します。
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce44b9234465af6bf52ce8baa0e60e641e845d3c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052672"
---
# <a name="ux-essentials-for-visual-studio"></a>UX Essentials for Visual Studio

## <a name="best-practices"></a>ベスト プラクティス

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. Visual Studio 環境で一貫性を維持します。

- シェル内で既存の[相互作用パターン](interaction-patterns-for-visual-studio.md)に従います。

- シェルのビジュアル言語および[クラフトマンシップ要件](evaluation-tools-for-visual-studio.md)に合わせて機能を設計します。

- 共有されるコマンドとコントロールが存在する場合は、それらを使用します。

- Visual Studio の階層と、それによってコンテキストがどのように確立されるか、UI がどのように設定されるかを理解します。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. フォントおよび色について環境サービスを使用します。

- UI は、[オプション] ダイアログの [フォントおよび色] ページのカスタマイズの対象でない限り、現在の[環境フォント](fonts-and-formatting-for-visual-studio.md)設定に従う必要があります。

- UI 要素は、共有環境トークンまたは機能固有トークンを使用して、[VSColor サービス](colors-and-styling-for-visual-studio.md)を使用する必要があります。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. すべての画像を新しい VS スタイルと一致させます。

- アイコン、グリフ、およびその他のグラフィックスについて、Visual Studio の設計原則に従います。

- テキストをグラフィック要素に配置しないでください。

### <a name="4-design-from-a-user-centric-perspective"></a>4. ユーザー中心の観点で設計します。

- タスク フローを作成してから、その中の個々の機能を作成します。

- ユーザーについて理解し、その知識を仕様で明示的に表します。

- UI をレビューするときは、エクスペリエンス全体と詳細を評価します。

- ロケールや言語に関係なく、機能的かつ魅力的になるように UI を設計します。

## <a name="screen-resolution"></a>画面解像度

### <a name="minimum-resolution"></a>最小解像度

- Visual Studio 2015 の最小解像度は **1280x720** です。 つまり、この解像度で Visual Studio を使用 "*できます*" が、最適なユーザー エクスペリエンスではない可能性があります。 1280x720 未満の解像度ではすべての機能が使用できるという保証はありません。

- Visual Studio の目標の解像度は **1366x768** です。 これは、"*優れた*" たユーザー エクスペリエンスを保証する最小解像度です。

- ダイアログの初期の高さを **700 ピクセル未満** にする必要があります。IDE フレームの最小解像度 (96 dpi) に収まるようにするためです。

### <a name="high-density-displays"></a>高画素密度ディスプレイ
 Visual Studio の UI は、Windows が既定でサポートしているすべての DPI スケール ファクター (150%、200%、250%) で適切に動作する必要があります。

## <a name="anti-patterns"></a>アンチ パターン
 Visual Studio には、ガイドラインとベスト プラクティスに従う UI の例が多数含まれています。 開発者が、一貫性を保とうとして、ビルドしているものと似た製品の UI 設計パターンを借用することがよくあります。 これはユーザー操作やビジュアル デザインの一貫性を向上させることができる方法ですが、場合によっては、スケジュールの制約や誤った優先順位付けのために、いくつかの細部がガイドラインに合っていない機能を提供することがあります。 このようなケースでは、これらの "アンチパターン" のいずれかをチームがコピーしないようにする必要があります。これらによって Visual Studio 環境内の不適切な UI または一貫性のない UI が急増するためです。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>既定でエラー状態として表示される必須フィールド/設定

#### <a name="feature-team-goals"></a>フィーチャー チームの目標

- 構成する必要がある要素が追加されたことをユーザーに警告します。

- 入力が必要な領域にユーザーの注意を引き付けます。

#### <a name="anti-pattern-solution"></a>アンチパターン ソリューション
 ユーザーが操作を開始したらすぐ、タスクを完了する前に、構成が必要な領域の横にシステム エラー アイコンを直ちに配置します。

#### <a name="example-manifest-designer-declarations"></a>例: マニフェスト デザイナーの宣言
 リストに宣言を追加すると、すぐにエラー状態になり、必要なプロパティをユーザーが設定するまでそのままになります。

 このケースには他の問題もあります。アラートに使用されるアイコンに "&times;" アイコンが含まれるため、その横で通常の削除アイコンを使用できません。 その結果、UI では [削除] ボタンが使用され、ぎこちない制御が行われます。

 ![既定で UI をエラー状態にすることは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti-pattern")<br />既定で UI をエラー状態にすることは、Visual Studio のアンチパターンです。

#### <a name="alternatives"></a>代替

この問題を適切に解決するには次のようにします。

- ユーザーが警告なしで宣言を追加でき、すぐに項目のプロパティを設定できるようにします。

- 項目からフォーカスが移動したとき (リストに別の宣言を追加するときや、デザイナー内のタブを変更しようとするときなど) に警告アイコン (金色の三角形) を追加します。

- ユーザーが宣言のプロパティを設定する前にタブを変更しようとすると、警告が解決されるまでアプリケーションがビルドされない (または影響がある) ことを示すダイアログが表示されます。 ユーザーがこのダイアログを閉じてタブを変更すると、アイコン (状況に応じてクリティカルまたは警告) が [宣言] タブに追加されます。

### <a name="multiple-clicks-to-dismiss-ui"></a>UI を閉じるための複数回のクリック

#### <a name="feature-team-goals"></a>フィーチャー チームの目標
 ユーザーが最初に説明テキストを確認せずに UI を閉じられないようにします。

#### <a name="anti-pattern"></a>アンチパターン
 VS UI 内のさまざまな場所にビデオ リンクを挿入するチームが、UX によって指定されている "&times;" (閉じる) ボタンとツールヒントの説明という一般的なパターンを使用しないことにしました。代わりに、ドロップダウンと [今後は表示しない] リンクを実装しました。

#### <a name="example-video-links-in-team-explorer"></a>例: チーム エクスプローラーのビデオ リンク
ユーザーが UI を閉じる前に、強制的に説明テキストを読み取らせるのは、Visual Studio 内のアンチパターンです。 適切に設計したビデオ リンクには、ホバー時に追加情報のツールヒントが表示されます。"&times;" をクリックすると、それ以上の操作を必要とせずにメッセージを閉じることができます。

 ![説明テキストのアンチパターン &#45; 正しくない](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />正しくないビデオ リンク パターン

ユーザーは、ビデオ リンクが表示されるすべての場所で UI を閉じるためだけに、単純な [閉じる] ボタン (ワン クリック) ではなく、2 回のクリックを強制されます。

この状況の正しい設計は、Internet Explorer、Office、および Visual Studio に共通するパターンに従うことです。つまり、ユーザーがホバー時にツールヒントの説明を確認でき、ワン クリックで UI を非表示にすることができます。

 ![説明テキストのアンチパターン &#45; 正しい](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-pattern-correct")<br />正しいビデオ リンク パターン

### <a name="using-command-bars-for-settings"></a>設定用のコマンド バーの使用

**図 A** は、このアンチパターンを示しています。つまり、あるコマンド ボタンの下に配置した設定が、そのコマンド以外にも適用されます。 このスケッチでは、[デバッグの開始] 以外に、選択した設定に従うコマンド ([ブラウザーで表示]、[デバッグなしで開始]、[ステップイン] など) があります。

![図 A: コマンド バーのアンチパターン](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-pattern-FigureA")<br />図 A: コマンド バーのアンチパターン

**図 B** のようにこのような設定をツールバーに配置すると、少し改善されますが、まだ望ましくありません。分割ボタンはそれほど場所を取らないためドロップダウンよりも優れていますが、どちらのデザインでもツールバーが使用され、実際にコマンドではないものが昇格されています。

![図 B: 改善されたものの依然としてアンチパターンであるコマンド バー](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-pattern-FigureB")<br />図 B: 改善されたものの依然としてアンチパターンであるコマンド バー

**図 C** に示されている正しい方法では、設定が一連のコマンドに関連付けられています。 グローバル設定が設定されず、4 つのコマンドを切り替えるだけです。 これは、ツールバー内のコマンドが許容される唯一の状況です。

![図 C: Visual Studio のコマンド バーの正しい使用パターン](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-pattern-FigureC")<br />図 C: Visual Studio のコマンド バーの正しい使用パターン

### <a name="control-anti-patterns"></a>アンチパターンの制御
 アンチパターンには、コントロールまたはコントロールのグループが不適切に使用されたり表示されたりしているだけのものもあります。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>ハイパーリンクではなくグループ ラベルとして使用される下線
 テキストの下線はハイパーリンクに対してのみ使用してください。

 **不適切:** \
 ![ハイパーリンク以外の下線付きテキストは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />ハイパーリンク以外の下線付きテキストは、Visual Studio のアンチパターンです。

 **適切:** \
 ![正しいスタイルの非ハイパーリンク テキストは、環境フォントで修飾なしで表示されます。](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />正しいスタイルの非ハイパーリンク テキストは、環境フォントで修飾なしで表示されます。

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>チェック ボックスをクリックするとポップアップダイアログが表示される
 [Windows Azure アプリケーションの発行] ウィザードで [すべてのロールに対してリモート デスクトップを有効にする] チェック ボックスをオンにすると、すぐにポップアップ ダイアログが表示されます (Visual Studio のアンチパターン)。 また、チェック ボックスが選択された後でもチェック ボックス フィールドに入力されません (もう 1 つの相互作用アンチパターン)。

 ![チェック ボックスのクリック後にダイアログを表示することは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />チェック ボックスのクリック後にダイアログを表示することは、Visual Studio のアンチパターンです。

### <a name="hyperlink-anti-patterns"></a>ハイパーリンクのアンチ パターン
 次の例には、2 つのアンチパターンが含まれています。

1. ホバー時に前景が赤色になるのは、フォント サービスの正しい共有色が使用されていないことを意味します。

2. [詳細情報] は、概念的なトピックへのリンクのテキストとして適切ではありません。 ユーザーの目標は、詳細情報を得ることではなく、選択内容の選択した場合の結果を理解することです。

   ![カラー サービスの無視とハイパーリンクでの [詳細情報] の使用は、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />カラー サービスの無視とハイパーリンクでの [詳細情報] の使用は、Visual Studio のアンチパターンです。

**最適なソリューション:** ユーザーがリンクをクリックして尋ねそうな質問を示します。 次に例を示します。

- Windows Azure サービスはどのように機能しますか。

- Windows Azure Mobile Services プロジェクトはどのような場合に必要ですか。

#### <a name="using-click-here-for-links"></a>リンクに対する "ここをクリック" の使用
 ハイパーリンクはそれ自体で意味がわかる必要があります。 "ここをクリック" または類似したバリエーションの使用はアンチパターンです。

 **不適切:** "新しいプロジェクトを作成する手順については、ここをクリックしてください。"

 **適切:** "新しいプロジェクトはどのように作成すればよいですか。"
