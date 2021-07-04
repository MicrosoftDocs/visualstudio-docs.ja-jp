---
title: Visual Studio のイメージとアイコン / Microsoft Docs
description: Visual Studio のイメージとアイコンの作成に使用されるデザインの概念について説明します。
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 36b77dc79574b1741c8feaded65104810e58c2fb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898793"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio のイメージとアイコン
## <a name="image-use-in-visual-studio"></a><a name="BKMK_ImageUseInVisualStudio"> Visual Studio でのイメージの使用</a>
 アートワークを作成する前に、[Visual Studio Image Library](https://www.microsoft.com/download/details.aspx?id=35825) の 1,000 以上のイメージを利用することを検討してください。

### <a name="types-of-images"></a>イメージの種類

- **アイコン**。 コマンド、階層、テンプレートなどに表示される小さいイメージ。 Visual Studio で使用される既定のアイコン サイズは、16 x 16 の PNG です。 イメージ サービスによって生成されるアイコンにより、HDPI サポート用の XAML 形式が自動的に生成されます。

    > [!NOTE]
    > メニュー システムでイメージが使用されている間は、どのコマンドに対してもアイコンを作成しないでください。 コマンドのアイコンを取得する必要があるかどうかを確認する場合は、「[Visual Studio のメニューとコマンド](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)」を参照してください。

- **サムネイル。** [新しいプロジェクト] ダイアログなどのダイアログのプレビュー領域で使用されるイメージ。

- **ダイアログのイメージ。** 説明用のグラフィックまたはメッセージ インジケーターとして、ダイアログまたはウィザードに表示されるイメージ。 難しい概念を示したり、ユーザーの注意を引いたりするために、まれに、必要な場合にのみ使用します (アラート、警告)。

- **アニメーション化されたイメージ。** 進行状況インジケーター、ステータス バー、操作ダイアログで使用されます。

- **カーソル。** オブジェクトが削除される可能性がある場合など、マウスを使用して操作を行えるかどうかを示すために使用されます。

## <a name="icon-design"></a><a name="BKMK_IconDesign"></a> アイコンのデザイン

### <a name="overview"></a>概要
 ジオメトリがクリーンで、肯定的/否定的 (ライト/ダーク) の 50/50 のバランスが保たれた、直接的でわかりやすいメタファーが使用される最新のスタイルのアイコンが Visual Studio で使用されます。 重要なアイコンのデザインのポイントは、わかりやすさ、単純化、コンテキストが中心となります。

- **わかりやすさ:** アイコンの意味と個性を示す、主なメタファーに焦点を当てます。

- **単純化:** アイコンで主な意味のみを示すようにします。つまり、必要な要素のみを使用して、余分な装飾のないテーマにします。

- **コンテキスト:** 概念の開発時に、アイコンの役割のすべての側面を考慮します。これは、アイコンの主なメタファーを構成する要素を決定する場合に重要です。

  アイコンを使用する場合は、次のようないくつかのデザイン ポイントを回避する必要があります。

- 適切な場合を除き、UI 要素を示すアイコンは使用しないでください。 UI 要素が一般的でもなく、明らかでもなく、一意でもない場合は、より抽象的な、あるいはシンボリックなアプローチを選択します。

- ドキュメント、フォルダー、矢印、虫眼鏡などの一般的な要素を使いすぎないようにしてください。 このような要素は、アイコンの意味に不可欠な場合にのみ使用してください。 たとえば、右向きの虫眼鏡は、検索、参照、検出のみを示す必要があります。

- 一部の従来のアイコン要素ではパースペクティブの使用が維持されますが、要素の明確さが欠けない限り、パースペクティブを使用する新しいアイコンを作成しないでください。

- アイコンに情報を詰め込みすぎないようにしてください。 簡単に認識できる、あるいは認識可能なシンボルとして認知できるシンプルなイメージは、複雑すぎるイメージよりもはるかに便利です。 アイコンですべてを伝えることはできません。

### <a name="icon-creation"></a>アイコンの作成

#### <a name="concept-development"></a>概念の開発
 Visual Studio の UI 内には、さまざまな種類のアイコンがあります。 開発時にアイコンの種類を慎重に検討してください。 アイコンの要素には、明確ではない、あるいは一般的ではない UI オブジェクトを使用しないでください。 このような場合 (スマート タグ アイコンを使用する場合など) は、シンボリックを選択します。 左側の抽象タグの意味は、右側のあいまいな UI ベースのバージョンよりも明確であることにご注意ください。

|**シンボリック イメージの正しい使用**|**シンボリック イメージの正しくない使用**|
|-|-|
|![正しい [スマート タグ] アイコン](../../extensibility/ux-guidelines/media/0404-01_smarttagcorrect.png "0404-01_SmartTagCorrect")|![正しくない [スマート タグ] アイコン](../../extensibility/ux-guidelines/media/0404-02_smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 標準的でわかりやすい UI 要素がアイコンに適している場合があります。 [ウィンドウの追加] がその一例です。

|**アイコンの正しい UI 要素**|**アイコンの正しくない UI 要素**|
|-|-|
|![正しい [ウィンドウの追加] アイコン](../../extensibility/ux-guidelines/media/0404-03_addwindowcorrect.png "0404-03_AddWindowCorrect")|![正しくない [ウィンドウの追加] アイコン](../../extensibility/ux-guidelines/media/0404-04_addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 アイコンの意味に不可欠でない限り、ドキュメントを基本要素として使用しないでください。 [ドキュメントの追加] に (下記のように) ドキュメントの要素がない場合は、意味が失われます。一方、[更新] を使用する場合、ドキュメントの要素で意味を伝える必要がなくなります。

|**ドキュメント アイコンの正しい使用**|**ドキュメント アイコンの正しくない使用**|
|-|-|
|![正しい [ドキュメント] アイコン](../../extensibility/ux-guidelines/media/0404-05_documenticoncorrect.png "0404-05_DocumentIconCorrect")|![正しくない [ドキュメント] アイコン](../../extensibility/ux-guidelines/media/0404-06_documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 "表示" の概念は、表示されている内容を示すのに最も適したアイコンで表す必要があります (たとえば、[すべてのファイルを表示] など)。 レンズのメタファーを使用すると、必要に応じて "ビュー" の概念を示すことができます (たとえば、[リソース ビュー] など)。

|**"表示"**|**"ビュー"**|
|-|-|
|![表示アイコン](../../extensibility/ux-guidelines/media/0404-07_show.png "0404-07_Show")|![ビュー アイコン](../../extensibility/ux-guidelines/media/0404-08_view.png "0404-08_View")|

 右向きの虫眼鏡アイコンは、検索、検出、および参照のみを表す必要があります。 正符号または負符号の付いた左向きのバリアントは、ズームインとズームアウトのみを表す必要があります。

|**"検索"**|**"ズーム"**|
|-|-|
|![[検索] アイコン](../../extensibility/ux-guidelines/media/0404-09_search.png "0404-09_Search")|![ズーム アイコン](../../extensibility/ux-guidelines/media/0404-10_zoom.png "0404-10_Zoom")|

 ツリー ビューでは、フォルダー アイコンと修飾子の両方を使用しないでください。 使用できる場合は、修飾子のみを使用します。

|**正しいツリー ビュー アイコン**|**正しくないツリー ビュー アイコン**|
|-|-|
|![正しいツリー ビュー アイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11_treeviewcorrect1.png "0404-11_TreeViewCorrect1") ![正しいツリー ビュー アイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12_treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![正しくないツリー ビュー アイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13_treeviewincorrect1.png "0404-13_TreeViewIncorrect1") ![正しくないツリー ビュー アイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14_treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>スタイルの詳細

#### <a name="layout"></a>Layout
 標準的な 16 x 16 アイコンに表示されるスタック要素:

 ![16 x 16 のアイコンのレイアウト スタック](../../extensibility/ux-guidelines/media/0404-15_layoutstack.png "0404-15_LayoutStack")<br />16 x 16 のアイコンのレイアウト スタック

 状態通知要素は、スタンドアロン アイコンとして使用することをお勧めします。 しかし、[タスクの完了] アイコンを使用する場合など、基本要素に通知を積み重ねる必要があるコンテキストがあります。

 ![Visual Studio でのスタンドアロン通知](../../extensibility/ux-guidelines/media/0404-16_standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")<br />スタンドアロン通知アイコン

 ![[タスクの完了] アイコン](../../extensibility/ux-guidelines/media/0404-17_taskcomplete.png "0404-17_TaskComplete")<br />[タスクの完了] アイコン

 プロジェクト アイコンは、通常、複数のサイズを含む .ico ファイルです。 ほとんどの 16 x 16 アイコンに同じ要素が含まれています。 32 x 32 バージョンには、プロジェクトの種類 (該当する場合) などの詳細が含まれています。

 ![Visual Studio での [プロジェクト] アイコン](../../extensibility/ux-guidelines/media/0404-18_iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")<br />VB Windows コントロール ライブラリ プロジェクトのアイコン、16 x 16 および 32 x 32

 ピクセル フレーム内の中央にアイコンを配置します。 そのようにできない場合は、アイコンをフレームの上部または右に揃えます。

 ![ピクセル フレーム内に中央揃えで配置されたアイコン](../../extensibility/ux-guidelines/media/0404-19_iconcentered.png "0404-19_IconCentered")<br />ピクセル フレーム内に中央揃えで配置されたアイコン

 ![ピクセル フレームの右上に配置されたアイコン](../../extensibility/ux-guidelines/media/0404-20_icontopright.png "0404-20_IconTopRight")<br />フレームの右上に配置されたアイコン

 ![ピクセル フレームの上部中央揃えで配置されたアイコン](../../extensibility/ux-guidelines/media/0404-21_icontopalign.png "0404-21_IconTopAlign")<br />フレームの上部中央揃えで配置されたアイコン

 最適な配置とバランスを実現するには、アイコンの基本要素がアクション グリフで妨げられないようにします。 基本要素の左上付近にグリフを配置します。 要素をさらに追加する場合は、アイコンの配置とバランスを考慮してください。

|**正しい配置とバランス**|**正しくない配置とバランス**|
|-|-|
|![正しいアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-22_alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![正しくないアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-23_alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 要素を共有し、セットで使用されるアイコンのサイズのパリティを確保します。 正しくないペアリングでは、円と矢印が大きすぎて一致しないことにご注意ください。

|**正しいサイズのパリティ**|**正しくないサイズのパリティ**|
|-|-|
|![正しいアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-24_sizeparitycorrect.png "0404-24_SizeParityCorrect")|![正しくないアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-25_sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 一貫した線と視覚的なウェイトを使用します。 構築するアイコンが、並べて比較を使用して他のアイコンとどのように比較されるかを評価します。 16 x 16 のフレーム全体を使用するのではなく、15 x 15 以下を使用します。 否定的と肯定的 (ダークとライト) の比率は 50/50 である必要があります。

|**正しい否定的と肯定的の比率**|**正しくない否定的と肯定的の比率**|
|-|-|
|![アイコンの正しい視覚的なウェイト &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-26_visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![アイコンの正しい視覚的なウェイト &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27_visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![アイコンの正しい視覚的なウェイト &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-28_visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![アイコンの正しくない視覚的なウェイト](../../extensibility/ux-guidelines/media/0404-29_visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 要素の整合性を損なうことなく、シンプルで比較可能な図形と余角を使用して要素を構築します。 可能な場合は、45° または 90° の角度を使用します。

 ![正しいアイコンの角度](../../extensibility/ux-guidelines/media/0404-30_iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>パースペクティブ
 アイコンは明確でわかりやすい状態にしておいてください。 必要な場合にのみ、パースペクティブと光源を使用します。 アイコン要素でパースペクティブを使用しないようにする必要がありますが、使用しないと一部の要素を認識できません。 そのような場合は、定型のパースペクティブで要素の明確さが伝えられます。

 ![3 点透視投影](../../extensibility/ux-guidelines/media/0404-31_3pointperspective.png "0404-31_3PointPerspective")<br />3 点透視投影

 ![1 点透視投影](../../extensibility/ux-guidelines/media/0404-32_1pointperspective.png "0404-32_1PointPerspective")<br />1 点透視投影

 ほとんどの要素は、右を向いているか、右に傾いている必要があります。

 ![右に傾いたアイコン](../../extensibility/ux-guidelines/media/0404-33_angledright.png "0404-33_AngledRight")

 オブジェクトに必要な明確さを加える場合にのみ、光源を使用します。

|**正しい光源**|**正しくない光源**|
|-|-|
|![正しいアイコンの光源](../../extensibility/ux-guidelines/media/0404-34_lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![正しくないアイコンの光源](../../extensibility/ux-guidelines/media/0404-35_lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 さらに読みやすくするか、メタファーをより効果的に伝える場合にのみ、アウトラインを使用します。 否定的と肯定的 (ダークとライト) のバランスは 50/50 である必要があります。

|**アウトラインの正しい使用**|**アウトラインの正しくない使用**|
|-|-|
|![正しいアウトライン](../../extensibility/ux-guidelines/media/0404-36_outlinescorrect.png "0404-36_OutlinesCorrect")|![正しくないアウトライン](../../extensibility/ux-guidelines/media/0404-37_outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>アイコンの種類
 **シェルおよびコマンド バー** アイコンは、1 つの基本、1 つの修飾子、1 つのアクション、または 1 つの状態の 3 つ以下の要素で構成されます。

 ![シェルおよびコマンド バーのアイコンの例](../../extensibility/ux-guidelines/media/0404-38_shellicons.png "0404-38_ShellIcons")<br />シェルおよびコマンド バーのアイコンの例

 **ツール ウィンドウのコマンド バー** アイコンは、1 つの基本、1 つの修飾子、1 つのアクション、または 1 つの状態の 3 つ以下の要素で構成されます。

 ![ツール ウィンドウのコマンド バー アイコンの例](../../extensibility/ux-guidelines/media/0404-39_toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")<br />ツール ウィンドウのコマンド バー アイコンの例

 **ツール ビューの曖昧性解消子** アイコンは、1 つの基本、1 つの修飾子、1 つのアクション、または 1 つの状態の 3 つ以下の要素で構成されます。

 ![ツリー ビューの曖昧性解消子アイコンの例](../../extensibility/ux-guidelines/media/0404-40_treeviewicons.png "0404-40_TreeViewIcons")<br />ツリー ビューの曖昧性解消子アイコンの例

 **状態ベースの値の分類** アイコンは、アクティブ、アクティブが無効、および非アクティブが無効の状態で存在します。

 ![状態ベースの値の分類アイコンの例](../../extensibility/ux-guidelines/media/0404-41_statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")<br />状態ベースの値の分類アイコンの例

 **IntelliSense** アイコンは、1 つの基本、1 つの修飾子、および 1 つの状態の 3 つ以下の要素で構成されます。

 ![IntelliSense アイコンの例](../../extensibility/ux-guidelines/media/0404-42_intellisenseicons.png "0404-42_IntelliSenseIcons")<br />IntelliSense アイコンの例

 **小さい (16 x 16) プロジェクト** アイコンには、1 つの基本と 1 つの修飾子の 2 つ以下の要素を含める必要があります。

 ![小さい (16 x 16) プロジェクト アイコンの例](../../extensibility/ux-guidelines/media/0404-43_16x16project1.png "0404-43_16x16Project1") ![16 x 16 のプロジェクト アイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44_16x16project2.png "0404-44_16x16Project2") ![16 x 16 のプロジェクト アイコン &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45_16x16project3.png "0404-45_16x16Project3")<br />小さい (16 x 16) プロジェクト アイコンの例

 **大きい (32 x 32) プロジェクト** アイコンは、1 つの基本、1 つから 2 つの修飾子、および 1 つの言語オーバーレイの 4 つ以下の要素で構成されます。

 ![大きい (32 x 32) プロジェクト アイコンの例](../../extensibility/ux-guidelines/media/0404-46_32x32project.png "0404-46_32x32Project")<br />大きい (32 x 32) プロジェクト アイコンの例

### <a name="production-details"></a>生成の詳細
 すべての新しい UI 要素は Windows Presentation Foundation (WPF) を使用して作成する必要があり、WPF の新しいアイコンはすべて 32 ビットの PNG 形式である必要があります。 24 ビットの PNG は、透明度がサポートされない従来の形式であるため、アイコンには推奨されません。

 解像度を 96 DPI で保存します。

#### <a name="file-types"></a>ファイルの種類

- **32 ビットの PNG:** アイコンに推奨される形式。 単一のラスター (ピクセル) イメージを格納できる無損失データ圧縮ファイル形式。 32 ビットの PNG ファイルでは、アルファチャネル透明度、ガンマ補正、およびインターレースがサポートされています。

- **32 ビットの BMP:** 非 WPF コントロール用。 XP (つまり、ハイカラー) とも呼ばれる 32 ビットの BMP は、RGB/A イメージ形式であり、アルファチャネル透明度を持つトゥルーカラーのイメージです。 アルファ チャネルは Adobe Photoshop で指定された透明度のレイヤーであり、追加 (4 番目) のカラー チャネルとしてビットマップ内に保存されます。 アートワークの生成時には、すべての 32 ビットの BMP ファイルに黒の背景が追加され、色深度について視覚的にすばやく確認できます。 この黒の背景は、UI でマスクアウトされる領域を表します。

- **32 ビットの ICO:** [プロジェクト] アイコンおよび [項目の追加] 用。 すべての ICO ファイルは、アルファチャネル透明度 (RGB/A) を使用する 32 ビットのトゥルー カラーです。 ICO ファイルには複数のサイズと色深度を格納できるため、Vista のアイコンは多くの場合、16 x 16、32 x 32、48 x 48、256 x 256 のイメージ サイズを含む ICO 形式となります。 エクスプローラーで適切に表示するには、イメージ サイズごとに、ICO ファイルの色深度を 24 ビットと 8 ビットに抑える必要があります。

- **XAML:** デザイン サーフェイスおよび Windows の装飾用。 XAML アイコンは、スケーリング、回転、ファイリング、透明度がサポートされるベクターベースのイメージ ファイルです。 現在、Visual Studio では一般的ではありませんが、柔軟性があるため、人気が高まっています。

- **SVG**

- **24 ビットの BMP:** Visual Studio のコマンド バー用。 トゥルーカラーの RGB イメージ形式である 24 ビットの BMP は、抜き合わせ透明度レイヤーのカラー キーとしてマゼンタ (R=255, G=0, B=255) を使用して透明度のレイヤーを作成するアイコン規則です。 24 ビットの BMP では、マゼンタ画面がすべて背景色を使用して表示されます。

- **24 ビットの GIF:** Visual Studio のコマンド バー用。 透明度がサポートされる、トゥルーカラーの RGB イメージ形式。 GIF ファイルは、ウィザードのアートワークと GIF アニメーションでよく使用されます。

### <a name="icon-construction"></a>アイコンの構築
 Visual Studio の最小アイコン サイズは 16 x 16 です。 一般的に使用される最大値は 32 x 32 です。 アイコンをデザインするときは、16 x 16、24 x 24、または 32 x 32 のフレーム全体を埋め尽くさないようにご注意ください。 読みやすく、一様なアイコンの構築はユーザーに認識させるのに不可欠です。 アイコンを構築するときは、次の点に従ってください。

- アイコンは、明確でわかりやすく、一貫性のあるものである必要があります。

- 状態通知要素をアイコンの基本要素の上に積み重ねるのではなく、1 つのアイコンとして使用することをお勧めします。 特定のコンテキストでは、UI で状態要素を基本要素と組み合わせる必要がある場合があります。

- プロジェクト アイコンは、通常、複数のサイズを含む .ico ファイルです。 16 x 16、24 x 24、および 32 x 32 アイコンのみが更新されます。 ほとんどの 16 x 16 および 24 x 24 アイコンに同じ要素が含まれます。 32 x 32 アイコンには、プロジェクトの言語の種類 (該当する場合) などの詳細が含まれています。

- 32 x 32 アイコンの場合、基本要素の線の太さは通常、2 ピクセルです。 1 または 2 ピクセルの線の太さを、詳細な要素に使用することができます。 慎重に検討し、どちらがより適しているかを判断してください。

- 16 x 16 および 24 x 24 アイコンの要素間のスペースは 1 ピクセル以上にしてください。 32 x 32 アイコンの場合は、要素間、および修飾子と基本要素の間に 2 ピクセルのスペースを使用します。

  ![16 x 16、24 x 24、32 x 32 サイズのアイコンの要素間スペース](../../extensibility/ux-guidelines/media/0404-47_elementspacing.png "0404-47_ElementSpacing")<br />16 x 16、24 x 24、32 x 32 サイズのアイコンの要素間スペース

#### <a name="color-and-accessibility"></a>色とユーザー補助
 Visual Studio のコンプライアンス ガイドラインでは、製品のすべてのアイコンが色とコントラストのユーザー補助の要件を満たしていることが求められます。 これはアイコンの反転によって実現されます。デザイン時には、製品内でプログラムによって反転されることに注意する必要があります。

 Visual Studio のアイコンでの色の使用について詳しくは、「[画像での色の使用](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)」を参照してください。

## <a name="using-color-in-images"></a><a name="BKMK_UsingColorInImages"></a> イメージでの色の使用

### <a name="overview"></a>概要
 Visual Studio のアイコンは主にモノクロです。 色は、特定の情報を伝えるために予約されており、装飾には使用されません。 色は以下の用途で使用されます。

- アクションを示す

- ユーザーに状態通知について警告する

- 言語の関連付けを指定する

- IntelliSense 内の項目を区別する

### <a name="accessibility"></a>ユーザー補助
 Visual Studio のコンプライアンス ガイドラインでは、製品にチェックインされているすべてのアイコンが、色とコントラストのユーザー補助の要件を満たしていることが求められます。 ビジュアル言語パレットの色はテストされており、これらの要件を満たしています。

#### <a name="color-inversion-for-dark-themes"></a>ダーク テーマの色の反転
 Visual Studio のダーク テーマで、正しいコントラスト比でアイコンを表示するために、プログラムによって反転が適用されます。 このガイドの色は、正しく反転するように一部が選択されています。 色の使用はこのパレットに限定してください。そうしないと、反転が適用されたときに予測できない結果になります。

 ![色が反転したアイコンの例](../../extensibility/ux-guidelines/media/0405-01_darkthemeinversion.png "0405-01_DarkThemeInversion")<br />色が反転したアイコンの例

### <a name="base-palette"></a>基本パレット
 すべての標準アイコンには、3 つの基本色が含まれています。 アイコンにはグラデーションやドロップ シャドウは含まれません。ただし、3D ツール アイコンの場合は 1 つまたは 2 つの例外があります。

|使用法|名前|値 (ライト テーマ)|見本|例|
|-----------|----------|---------------------------|------------|-------------|
|背景/ダーク|VS BG|424242 / 66,66,66|![見本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|![基本パレットの例](../../extensibility/ux-guidelines/media/0405-02_basepaletteexample.png "0405-02_BasePaletteExample")|
|前景/ライト|VS FG|F0EFF1 / 240,239,241|![見本 F0EFF1](../../extensibility/ux-guidelines/media/0405_f0eff1.png "0405_F0EFF1")||
|[外枠]|VS Out|F6F6F6 / 246,246,246|![見本 F6F6F6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")||

 基本色に加えて、各アイコンには拡張パレットの 1 つの追加の色が含まれる場合があります。

### <a name="extended-palette"></a>拡張パレット

#### <a name="action-modifiers"></a>アクション修飾子
 以下の 4 つの色は、アクション修飾子で必要なアクションの種類を示しています。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|正|VS Action Green|388A34 / 56,138,52|![見本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|負|VS Action Red|A1260D / 161,38,13|![見本 A1260D](../../extensibility/ux-guidelines/media/0405_a1260d.png "0405_A1260D")|
|中立|VS Action Blue|00539C / 0,83,156|![見本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|作成および新規作成|VS Action Orange|C27D1A / 194,156,26|![見本 C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>例
 緑は、"追加"、"実行"、"再生"、"確認" などの肯定的なアクションの修飾子に使用されます。

|実行|クエリの実行|すべてのステップの再生|コントロールの追加|
|-|-|-|-|
|![実行アイコン](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")|![[クエリの実行] アイコン](../../extensibility/ux-guidelines/media/0405-04_executequery.png "0405-04_ExecuteQuery")|![[すべてのステップの再生] アイコン](../../extensibility/ux-guidelines/media/0405-05_playallsteps.png "0405-05_PlayAllSteps")|![[コントロールの追加] アイコン](../../extensibility/ux-guidelines/media/0405-06_addcontrol.png "0405-06_AddControl")|

 赤は、"削除"、"停止"、"取り消し"、"閉じる" などの否定的なアクション修飾子に使用されます。

|リレーションシップの削除|列の削除|クエリの停止|オフラインの接続|
|-|-|-|-|
|![[リレーションシップの削除] アイコン](../../extensibility/ux-guidelines/media/0405-07_deleterelationship.png "0405-07_DeleteRelationship")|![[列の削除] アイコン](../../extensibility/ux-guidelines/media/0405-08_deletecolumn.png "0405-08_DeleteColumn")|![[クエリの停止] アイコン](../../extensibility/ux-guidelines/media/0405-09_stopquery.png "0405-09_StopQuery")|![[オフラインの接続] アイコン](../../extensibility/ux-guidelines/media/0405-10_connectionoffline.png "0405-10_ConnectionOffline")|

 青は、"開く"、"次へ"、"前へ"、"インポート"、"エクスポート" など、一般的に矢印として表されるニュートラル アクション修飾子に適用されます。

|フィールドに移動|バッチ処理されたチェックイン|アドレス エディター|関連付けエディター|
|-|-|-|-|
|![[オブジェクトの選択] アイコン](../../extensibility/ux-guidelines/media/0405-11_gotofield.png "0405-11_GoToField")|![[バッチ処理されたチェックイン] アイコン](../../extensibility/ux-guidelines/media/0405-12_batchedcheckin.png "0405-12_BatchedCheckIn")|![[アドレス エディター] アイコン](../../extensibility/ux-guidelines/media/0405-13_addresseditor.png "0405-13_AddressEditor")|![[関連付けエディター] アイコン](../../extensibility/ux-guidelines/media/0405-14_associationeditor.png "0405-14_AssociationEditor")|

 ダーク ゴールドは主に "新しい" 修飾子に使用されます。

|[新しいプロジェクト]|新しいグラフの作成|新しい単体テスト|新しいリスト アイテム|
|-|-|-|-|
|![[新しいプロジェクト] アイコン](../../extensibility/ux-guidelines/media/0405-15_newproject.png "0405-15_NewProject")|![[新しいグラフの作成] アイコン](../../extensibility/ux-guidelines/media/0405-16_createnewgraph.png "0405-16_CreateNewGraph")|![[新しい単体テスト] アイコン](../../extensibility/ux-guidelines/media/0405-17_newunittest.png "0405-17_NewUnitTest")|![[新しいリスト アイテム] アイコン](../../extensibility/ux-guidelines/media/0405-18_newlistitem.png "0405-18_NewListItem")|

#### <a name="special-cases"></a>特殊なケース
 特殊なケースでは、色分けされたアクション修飾子をスタンドアロン アイコンとして単独で使用できます。 アイコンに使用される色には、アイコンが関連付けられているアクションが反映されます。 この使用は、次のような、アイコンの小さなサブセットに制限されます。

|実行|Stop|削除|保存|最近参照した場所|
|-|-|-|-|-|
|![実行アイコン](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405-03_ActionModifierRun")|![停止アイコン - 実線の赤の四角形。](../../extensibility/ux-guidelines/media/0405-19_stop.png "0405-19_Stop")|![削除アイコン](../../extensibility/ux-guidelines/media/0405-20_delete.png "0405-20_Delete")|![[Save]\(保存\) アイコン](../../extensibility/ux-guidelines/media/0405-21_save.png "0405-21_Save")|![[戻る] アイコン](../../extensibility/ux-guidelines/media/0405-22_navigateback.png "0405-22_NavigateBack")|

### <a name="code-hierarchy-palette"></a>コード階層パレット

#### <a name="folder"></a>Folder

|使用法|名前|値 (すべてのテーマ)|見本|例|
|-----------|----------|--------------------------|------------|-------------|
|フォルダー|Folder|DCB67A / 220,182,122|![見本 DCB67A](../../extensibility/ux-guidelines/media/0405_dcb67a.png "0405_DCB67A")|![フォルダーの色のアイコン](../../extensibility/ux-guidelines/media/0405-23_foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio の言語
 Visual Studio で使用できる各共通言語またはプラットフォームには色が関連付けられています。 これらの色は、基本アイコン、または複合アイコンの右上隅に表示される言語修飾子で使用されます。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|ASP、HTML、WPF|ASP HTML WPF Blue|0095D7 / 0,149,215|![見本 0095D7](../../extensibility/ux-guidelines/media/0405_0096d7.png "0405_0096D7")|
|C++|CPP Purple|9B4F96 / 155,79,150|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|C#|CS Green (VS Action Green)|388A34 / 56,138,52|![見本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|CSS|CSS Red|BD1E2D / 189,30,45|![見本 BD1E2D](../../extensibility/ux-guidelines/media/0405_bd1e2d.png "0405_BD1E2D")|
|F#|FS Purple|672878 / 103,40,120|![見本 672878](../../extensibility/ux-guidelines/media/0405_672878.png "0405_672878")|
|JavaScript|JS Orange|F16421 / 241,100,33|![見本 F16421](../../extensibility/ux-guidelines/media/0405_f16421.png "0405_F16421")|
|VB|VB Blue (VS Action Blue)|00539C / 0,83,156|![見本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|TypeScript|TS Orange|E04C06 / 224,76,6|![見本 E04C06](../../extensibility/ux-guidelines/media/0405_e04c06.png "0405_E04C06")|
|Python|PY Green|879636 / 135,150,54|![見本 879636](../../extensibility/ux-guidelines/media/0405_879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>言語の修飾子があるアイコンの例

|VB|C#|C++|F#|JavaScript|Python|
|-|-|-|-|-|-|
|![Visual Basic アイコン](../../extensibility/ux-guidelines/media/0405-25_vb.png "0405-25_VB")|![C&#35; アイコン](../../extensibility/ux-guidelines/media/0405-26_csharp.png "0405-26_CSharp")|![C&#43;&#43; アイコン](../../extensibility/ux-guidelines/media/0405-27_cplusplus.png "0405-27_CPlusPlus")|![F&#35; アイコン](../../extensibility/ux-guidelines/media/0405-28_fsharp.png "0405-28_FSharp")|![JavaScript アイコン](../../extensibility/ux-guidelines/media/0405-29_javascript.png "0405-29_JavaScript")|![Python アイコン](../../extensibility/ux-guidelines/media/0405-30_python.png "0405-30_Python")|

|HTML|WPF|ASP|CSS|TypeScript|
|-|-|-|-|-|
|![HTML アイコン](../../extensibility/ux-guidelines/media/0405-31_html.png "0405-31_HTML")<br />HTML|![WPF アイコン](../../extensibility/ux-guidelines/media/0405-32_wpf.png "0405-32_WPF")<br />WPF|![ASP アイコン](../../extensibility/ux-guidelines/media/0405-33_asp.png "0405-33_ASP")<br />ASP|![CSS アイコン](../../extensibility/ux-guidelines/media/0405-34_css.png "0405-34_CSS")<br />CSS|![TypeScript アイコン](../../extensibility/ux-guidelines/media/0405-35_typescript.png "0405-35_TypeScript")<br />TypeScript|

#### <a name="intellisense"></a>IntelliSense
 IntelliSense アイコンには専用のカラー パレットが使用されます。 これらの色を使用すると、ユーザーが IntelliSense のポップアップ リスト内のさまざまな項目をすばやく区別するのに役立ちます。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|クラス、イベント|VS Action Orange|C27D1A / 194,125,26|![見本 C27D1A](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|
|拡張メソッド、メソッド、モジュール、デリゲート|VS Action Purple|652D90 / 101,45,144|![見本 652D90](../../extensibility/ux-guidelines/media/0405_652d90.png "0405_652D90")|
|フィールド、列挙型項目、マクロ、構造体、共用体の値の型、演算子、インターフェイス|VS Action Blue|00539C / 0,83,156|![見本 00539C](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|Object|VS Action Green|388A34 / 56,138,52|![見本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|定数、例外、列挙型項目、マップ、マップ項目、名前空間、テンプレート、型定義|Background (VS BG)|424242 / 66,66,66|![見本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense アイコンの例

|クラス|プライベート イベント|代理人|メソッド フレンド|フィールド|
|-|-|-|-|-|
|![IntelliSense クラスのアイコン](../../extensibility/ux-guidelines/media/0405-36_intellisenseclass.png "0405-36_IntelliSenseClass")|![IntelliSense プライベート イベントのアイコン](../../extensibility/ux-guidelines/media/0405-37_intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")|![IntelliSense デリゲートのアイコン](../../extensibility/ux-guidelines/media/0405-38_intellisensedelegate.png "0405-38_IntelliSenseDelegate")|![IntelliSense メソッド フレンドのアイコン](../../extensibility/ux-guidelines/media/0405-39_intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")|![フィールド アイコン](../../extensibility/ux-guidelines/media/0405-40_field.png "0405-40_Field")|

|保護された列挙型項目|Object|Template|例外のショートカット|
|-|-|-|-|
|![IntelliSense の保護された列挙型の項目のアイコン](../../extensibility/ux-guidelines/media/0405-41_intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")|![IntelliSense オブジェクトのアイコン](../../extensibility/ux-guidelines/media/0405-42_intellisenseobject.png "0405-42_IntelliSenseObject")|![IntelliSense テンプレートのアイコン](../../extensibility/ux-guidelines/media/0405-43_intellisensetemplate.png "0405-43_IntelliSenseTemplate")|![IntelliSense の例外のショートカットのアイコン](../../extensibility/ux-guidelines/media/0405-44_intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")|

### <a name="notifications"></a>通知
 Visual Studio での通知は、状態を示すために使用されます。 通知パレットで次の 4 つの色と、黒または白の前景の塗りつぶしオプションが使用され、以下の状態レベルで通知が定義されます。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|状態: ニュートラル|Notification Blue (VS Blue)|1BA1E2 / 27,161,226|![見本 1BA1E2](../../extensibility/ux-guidelines/media/0405_1ba1e2.png "0405_1BA1E2")|
|状態: 肯定的|Notification Green (VS Green)|339933 / 51,153,51|![見本 339933](../../extensibility/ux-guidelines/media/0405_339933.png "0405_339933")|
|状態: 否定的|Notification Red (VS Red)|E51400 / 229,20,0|![見本 E51400](../../extensibility/ux-guidelines/media/0405_e51400.png "0405_E51400")|
|状態: 警告|Notification Yellow (VS Orange)|FFCC00 / 255,204,0|![見本 FFCC00](../../extensibility/ux-guidelines/media/0405_ffcc00.png "0405_FFCC00")|
|前景塗りつぶし|Notification Black (Black)|000000 / 0,0,0|![見本 &#35;000000](../../extensibility/ux-guidelines/media/0405_000000.png "0405_000000")|
|前景塗りつぶし|Notification White (White)|FFFFFF / 255,255,255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知アイコンの例

|アラート:|警告|完了|Stop|
|-|-|-|-|
|![通知アイコン](../../extensibility/ux-guidelines/media/0405-45_alert.png "0405-45_Alert")|![警告アイコン](../../extensibility/ux-guidelines/media/0405-48_warning.png "0405-48_Warning")|![完了アイコン](../../extensibility/ux-guidelines/media/0405-46_complete.png "0405-46_Complete")|![停止アイコン - 中央に白い正方形の付いた実線の赤い丸が付いています。](../../extensibility/ux-guidelines/media/0405-47_stop.png "0405-47_Stop")|