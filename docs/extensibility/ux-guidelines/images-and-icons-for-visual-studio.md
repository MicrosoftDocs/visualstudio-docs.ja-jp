---
title: Visual Studio のイメージとアイコン |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0ba4a5c52bf972236914c06ec9672653fbde9cea
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67891053"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio のイメージとアイコン
## <a name="BKMK_ImageUseInVisualStudio"></a> Visual Studio でのイメージの使用
 アートワークを作成する前に考慮で 1,000 個以上のイメージの使用、 [Visual Studio Image Library](http://www.microsoft.com/en-my/download/details.aspx?id=35825)します。

### <a name="types-of-images"></a>イメージの種類

- **アイコン**します。 コマンド、階層、テンプレート、および具合に表示される小さいイメージ。 Visual Studio で使用される既定のアイコン サイズは、16 x 16 PNG です。 イメージのサービスによって自動的に生成されたアイコンの HDPI サポートを XAML 形式を生成します。

    > [!NOTE]
    > イメージは、メニューで使用されますが、すべてのコマンドのアイコンを作成しないでください。 参照してください[Visual Studio のメニューとコマンド](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)コマンドがアイコンを取得するかどうかを確認します。

- **縮小表示します。** 新しいプロジェクト ダイアログなどのダイアログ ボックスの プレビュー 領域で使用されるイメージ。

- **ダイアログの画像。** ダイアログ ボックスまたはウィザードでは、わかりやすいグラフィックスまたはメッセージ インジケーターとして表示される画像。 難しい概念を示しています。 または、ユーザーの注意 (アラート、警告) を確保するために必要な場合にのみ、頻繁に使用します。

- **アニメーション化されたイメージ。** 進行状況の指標、ステータス バー、および操作のダイアログ ボックスで使用されます。

- **カーソル。** するオブジェクトが破棄される可能性があります、ため、マウスを使用して、操作を許可するかどうかを示すために使用します。

## <a name="BKMK_IconDesign"></a> アイコンの設計

### <a name="overview"></a>概要
 Visual Studio では、クリーンのジオメトリと (淡色/濃色) の成功/失敗の 50/50 残高および理解できる、直接のメタファを使用して、モダン スタイル アイコンを使用します。 重要なアイコンの設計では、わかりやすくするため、単純化、およびコンテキストの中心を指します。

- **わかりやすくするため:** の意味と個性にアイコンを提供するコア メタファに注目します。

- **簡素化:** の中核的な意味にアイコンを減らす - 必要な要素だけを省いた間でのテーマを取得します。

- **コンテキスト:** どの要素を構成して、アイコンのコアのメタファを決定する際に重要になる概念開発中にアイコンのロールのすべての側面を検討してください。

  アイコンには、回避するために設計ポイント数があります。

- 該当する場合を除く、UI 要素を示すアイコンを使用しないでください。 UI 要素は、一般的な明らかも一意でもない場合より抽象的またはシンボリック アプローチを選択します。

- ドキュメント、フォルダー、矢印、拡大鏡などの共通の要素を過剰に使用しません。 アイコンの意味に不可欠な場合にのみ、このような要素を使用します。 たとえば、右向きの虫眼鏡がのみの検索を示す必要がありますを参照し、検索します。

- 一部のレガシ アイコン要素は、パースペクティブの使用を管理、作成しないでください新しいアイコンの観点でしない限り、要素なしでわかりやすくするためが不足しています。

- アイコンに情報が多すぎるを詰め込もうはありません。 簡単に認識または認識可能なシンボルとして学習できる単純なイメージが過度に複雑な画像よりもはるかに便利です。 アイコンは、全体のストーリーを伝えることはできません。

### <a name="icon-creation"></a>アイコンの作成

#### <a name="concept-development"></a>開発の概念
 Visual Studio では、さまざまなアイコンの種類の UI 内でに。 開発中にアイコンの種類を慎重に検討します。 アイコンの要素の不明なまたは一般的でない UI オブジェクトを使用しないでください。 スマート タグ アイコンをなど、このような場合は、シンボリック リンクの選択します。 左側の抽象タグの意味は、右側に、UI ベースの漠然としたバージョンよりもより明白なことに注意してください。

|||
|-|-|
|**シンボルの画像の正しい使用**|**シンボルの画像の不適切な使用**|
|![スマート タグ アイコンの正しい](../../extensibility/ux-guidelines/media/0404-01_smarttagcorrect.png "0404 01_SmartTagCorrect")|![スマート タグ アイコンの正しくない](../../extensibility/ux-guidelines/media/0404-02_smarttagincorrect.png "0404 02_SmartTagIncorrect")|

 標準的なわかりやすい UI 要素が操作もアイコンのインスタンスがあります。 ウィンドウは、このような 1 つの例を追加します。

|||
|-|-|
|**アイコンの正しい UI 要素**|**アイコンの不適切な UI 要素**|
|![ウィンドウの追加 アイコンの正しい](../../extensibility/ux-guidelines/media/0404-03_addwindowcorrect.png "0404 03_AddWindowCorrect")|![正しくないウィンドウの追加 アイコン](../../extensibility/ux-guidelines/media/0404-04_addwindowincorrect.png "0404 04_AddWindowIncorrect")|

 アイコンの意味するために不可欠である場合を除き、基本要素として、ドキュメントを使用しないでください。 ドキュメントなし (下記参照)、意味の追加ドキュメントの要素は、更新でドキュメント要素で意味を伝える必要はありませんが、失われます。

|||
|-|-|
|**ドキュメント アイコンの正しい使用**|**ドキュメント アイコンの不適切な使用**|
|![ドキュメント アイコンの正しい](../../extensibility/ux-guidelines/media/0404-05_documenticoncorrect.png "0404 05_DocumentIconCorrect")|![正しくないドキュメント アイコン](../../extensibility/ux-guidelines/media/0404-06_documenticonincorrect.png "0404 06_DocumentIconIncorrect")|

 "Show"の概念は、最適に表示される内容などのすべてのファイルを表示する例と同じを示すアイコンで表示する必要があります。 レンズのメタファをリソース ビューの例など、必要に応じて、"view"の概念を示すために使用できます。

|||
|-|-|
|**"Show"**|**"View"**|
|![アイコンを表示する](../../extensibility/ux-guidelines/media/0404-07_show.png "0404 07_Show")|![表示アイコン](../../extensibility/ux-guidelines/media/0404-08_view.png "0404 08_View")|

 右向きのガラスのアイコンに表す・のみ検索を拡大、検索、および参照します。 プラス記号またはマイナス記号の左側に接続するバリアントはのみに拡大を表す/ズーム アウトする必要があります。

|||
|-|-|
|**"Search"**|**"Zoom"**|
|![検索アイコン](../../extensibility/ux-guidelines/media/0404-09_search.png "0404 09_Search")|![[ズーム] アイコン](../../extensibility/ux-guidelines/media/0404-10_zoom.png "0404 10_Zoom")|

 ツリー フォルダーのアイコンと修飾子の両方、ビューは使わないでください。 有効な場合は、修飾子のみを使用します。

|||
|-|-|
|**正しい ツリー ビュー アイコン**|**正しくない ツリー ビュー アイコン**|
|![正しい ツリー ビュー アイコン&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11_treeviewcorrect1.png "0404 11_TreeViewCorrect1") ![正しい ツリー ビュー アイコン&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12_treeviewcorrect2.png "0404 12_TreeViewCorrect2")|![正しくない ツリー ビュー アイコン&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13_treeviewincorrect1.png "0404 13_TreeViewIncorrect1") ![正しくない ツリー ビュー アイコン&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14_treeviewincorrect2.png "0404 14_TreeViewIncorrect2")|

### <a name="style-details"></a>スタイルの詳細

#### <a name="layout"></a>レイアウト
 標準の 16 x 16 のアイコンのように要素をスタック:

 ![16 x 16 のアイコンのレイアウト スタック](../../extensibility/ux-guidelines/media/0404-15_layoutstack.png "0404 15_LayoutStack")<br />16 x 16 のアイコンのレイアウト スタック

 状態通知要素は、スタンドアロンのアイコンとして使用されています。 ただしを通知する必要がありますに重ねることが、base 要素など、タスクの完了のアイコンでコンテキストがあります。

 ![Visual Studio でのスタンドアロン通知](../../extensibility/ux-guidelines/media/0404-16_standalonenotificationicons.png "0404 16_StandaloneNotificationIcons")<br />スタンドアロンの通知アイコン

 ![タスクの完了 アイコン](../../extensibility/ux-guidelines/media/0404-17_taskcomplete.png "0404 17_TaskComplete")<br />タスクの完了 アイコン

 プロジェクト アイコンは、通常、複数のサイズが含まれている .ico ファイルです。 ほとんどの 16 x 16 のアイコンには、同じ要素が含まれます。 32 x 32 のバージョンでは、詳細については、該当する場合、プロジェクトの種類などがあります。

 ![プロジェクトで Visual Studio のアイコン](../../extensibility/ux-guidelines/media/0404-18_iconprojectthreesizes.png "0404 18_IconProjectThreeSizes")<br />16 x 16、32 x 32 の VB Windows コントロール ライブラリ プロジェクト アイコン

 ピクセル フレーム内のアイコンを中央揃えします。 それは不可能である場合、アイコン、ページのトップへ、またはフレームの右に揃えます。

 ![ピクセル フレーム内で中央揃えアイコン](../../extensibility/ux-guidelines/media/0404-19_iconcentered.png "0404 19_IconCentered")<br />ピクセル フレーム内に中央揃えで配置されたアイコン

 ![配置されたアイコン上のピクセル フレームの右](../../extensibility/ux-guidelines/media/0404-20_icontopright.png "0404 20_IconTopRight")<br />一番上に配置されたアイコン、フレームの右

 ![アイコンが中央に配置され、ピクセル フレームの上部に揃えて配置](../../extensibility/ux-guidelines/media/0404-21_icontopalign.png "0404 21_IconTopAlign")<br />中央揃えにし、フレームの上部に配置されたアイコン

 最適な配置とのバランスを実現するには、アクションで、アイコンの基本要素の障害を回避します。 基本要素の上部にあるグリフが左を置きます。 その他の要素を追加する場合は、アイコンの分散と配置を検討してください。

|||
|-|-|
|**適切なアラインメントと分散**|**不適切な配置と分散**|
|![アイコンの分散と配置を修正](../../extensibility/ux-guidelines/media/0404-22_alignbalancecorrect.png "0404 22_AlignBalanceCorrect")|![正しくないアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-23_alignbalanceincorrect.png "0404 23_AlignBalanceIncorrect")|

 要素を共有し、セットで使用されるアイコンのサイズのパリティを確認してください。 正しくない組み合わせで、円と矢印はサイズ超過に注意してくださいし、一致しません。

|||
|-|-|
|**適切なサイズのパリティ**|**不適切なサイズのパリティ**|
|![アイコンのサイズとパリティ修正](../../extensibility/ux-guidelines/media/0404-24_sizeparitycorrect.png "0404 24_SizeParityCorrect")|![正しくないアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-25_sizeparityincorrect.png "0404 25_SizeParityIncorrect")|

 一貫性のある行とビジュアルの重みを使用します。 その他のアイコンをサイド バイ サイドで比較を使用して作成するアイコンの比較を評価します。 使用して、全体の 16 x 16 フレームが 15 x 15、またはより小さいを使用しないでください。 負の値が正数 (暗い光) の比率が 50/50 必要があります。

|||
|-|-|
|**負の値が正数の正しい比**|**正しくない負の値が正数の比率**|
|![アイコンの視覚的なウェイトを修正&#40;1&#41;](../../extensibility/ux-guidelines/media/0404-26_visualweightcorrect1.png "0404 26_VisualWeightCorrect1")<br /><br /> ![アイコンの視覚的なウェイトを修正&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27_visualweightcorrect2.png "0404 27_VisualWeightCorrect2")<br /><br /> ![アイコンの視覚的なウェイトを修正&#40;3&#41;](../../extensibility/ux-guidelines/media/0404-28_visualweightcorrect3.png "0404 28_VisualWeightCorrect3")|![アイコンの正しくない視覚的なウェイト](../../extensibility/ux-guidelines/media/0404-29_visualweightincorrect.png "0404 29_VisualWeightIncorrect")|

 要素の整合性を損なうことがなく、要素を構築するのにには、シンプルで同等の図形と補色角度を使用します。 可能であれば、45 度または 90 度の角度を使用します。

 ![アイコンの角度を修正](../../extensibility/ux-guidelines/media/0404-30_iconanglescorrect.png "0404 30_IconAnglesCorrect")

#### <a name="perspective"></a>透視投影
 明確でわかりやすく、アイコンを保持します。 パースペクティブと光の光源を使用しているために必要な場合にのみ使用します。 パースペクティブを使用して、アイコンの要素では避ける必要があります、いくつかの要素はなしで認識されていません。 このような場合は、定型のパースペクティブは、要素のわかりやすくするためと通信します。

 ![3 点透視投影](../../extensibility/ux-guidelines/media/0404-31_3pointperspective.png "0404 31_3PointPerspective")<br />3 点透視投影

 ![1 点透視投影](../../extensibility/ux-guidelines/media/0404-32_1pointperspective.png "0404 32_1PointPerspective")<br />1 点透視投影

 ほとんどの要素に直面している必要があります。 または右側の角度。

 ![アイコンを右に傾いた](../../extensibility/ux-guidelines/media/0404-33_angledright.png "0404 33_AngledRight")

 オブジェクトに必要なわかりやすくするためを追加する場合にのみ、光源を使用します。

|||
|-|-|
|**正しい光源**|**正しくない光源**|
|![アイコンの光源を修正](../../extensibility/ux-guidelines/media/0404-34_lightsourcescorrect.png "0404 34_LightSourcesCorrect")|![アイコンの正しくない光源](../../extensibility/ux-guidelines/media/0404-35_lightsourcesincorrect.png "0404 35_LightSourcesIncorrect")|

 アウトラインを使用して、読みやすさを強化するのみかメタファのコミュニケーションを改善します。 負の値が正数 (暗い光) 残高が 50/50 必要があります。

|||
|-|-|
|**アウトラインの正しい使用**|**アウトラインの不適切な使用**|
|![アウトラインの修正](../../extensibility/ux-guidelines/media/0404-36_outlinescorrect.png "0404 36_OutlinesCorrect")|![正しくないアウトライン](../../extensibility/ux-guidelines/media/0404-37_outlinesincorrect.png "0404 37_OutlinesIncorrect")|

#### <a name="icon-types"></a>アイコンの種類
 **シェルおよびコマンド バー**アイコンは、次の要素の 3 個で構成されている: 基数が 1 つ、修飾子を 1 つ、1 つのアクション、または 1 つの状態。

 ![シェルおよびコマンド バーのアイコンの例については](../../extensibility/ux-guidelines/media/0404-38_shellicons.png "0404 38_ShellIcons")<br />シェルとコマンド バーのアイコンの例

 **ツール ウィンドウ コマンド バー**アイコンは、次の要素の 3 個で構成されている: 基数が 1 つ、修飾子を 1 つ、1 つのアクション、または 1 つの状態。

 ![ツール ウィンドウの例のコマンド バーのアイコン](../../extensibility/ux-guidelines/media/0404-39_toolwindowcommandbaricons.png "0404 39_ToolWindowCommandBarIcons")<br />ツール ウィンドウ コマンド バーのアイコンの例

 **ツリー ビューの曖昧性解消子**アイコンは、次の要素の 3 個で構成されている: 基数が 1 つ、修飾子を 1 つ、1 つのアクション、または 1 つの状態。

 ![ツリーの例については、曖昧性解消子アイコンを表示](../../extensibility/ux-guidelines/media/0404-40_treeviewicons.png "0404 40_TreeViewIcons")<br />ツリーの例については、曖昧性解消子アイコンを表示します。

 **値の状態に基づく分類**アイコンは、次の状態で存在: アクティブ、無効になっている、アクティブおよび非アクティブな無効になっています。

 ![値の状態に基づく分類アイコンの例](../../extensibility/ux-guidelines/media/0404-41_statebasedtaxonomy.png "0404 41_StateBasedTaxonomy")<br />値の状態に基づく分類アイコンの例

 **IntelliSense**アイコンは、次の要素の 3 個で構成されている: 基数が 1 つ、1 つの修飾子、および 1 つの状態。

 ![IntelliSense アイコンの例](../../extensibility/ux-guidelines/media/0404-42_intellisenseicons.png "0404 42_IntelliSenseIcons")<br />IntelliSense アイコンの例

 **小規模な (16 x 16) プロジェクト**アイコンは、2 つまで要素を持つ必要があります: 1 つのベースと 1 つの修飾子。

 ![小規模 (16 x 16) の例のプロジェクト アイコン](../../extensibility/ux-guidelines/media/0404-43_16x16project1.png "0404 43_16x16Project1") ![16 x 16 プロジェクト アイコン&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44_16x16project2.png "0404 44_16x16Project2") ![16 x 16 プロジェクト アイコン&#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45_16x16project3.png "0404 45_16x16Project3")<br />小規模 (16 x 16) プロジェクト アイコンの例

 **大規模 (32 x 32) プロジェクト**次の要素の 4 個のアイコンで構成されます: 基数が 1 つ、1 ~ 2 の修飾子、およびオーバーレイの 1 つの言語。

 ![大規模な (32 x 32) の例のプロジェクト アイコン](../../extensibility/ux-guidelines/media/0404-46_32x32project.png "0404 46_32x32Project")<br />大規模な (32 x 32) プロジェクト アイコンの例

### <a name="production-details"></a>運用環境の詳細
 すべての新しい UI 要素は、Windows Presentation Foundation (WPF) を使用して作成する必要があり、WPF のすべての新しいアイコンは、32 ビット PNG 形式である必要があります。 24 ビット PNG は、透過性をサポートしていませんし、そのため、アイコンの推奨されませんレガシ形式です。

 96 DPI の解像度を保存します。

#### <a name="file-types"></a>ファイルの種類

- **32 ビット PNG:** アイコンの推奨される形式。 1 つ (ピクセル) をラスター イメージを格納できるロスレス データの圧縮ファイル形式。 32 ビット PNG ファイルは、アルファ チャネル透明度、ガンマ補正、およびインター レースをサポートします。

- **32 ビット BMP:** 非 WPF コントロール。 XP または高の色とも呼ばれ、32 ビット BMP は、RGB のイメージ形式、アルファ チャネルの透明度 true 色の画像です。 アルファ チャネルは、レイヤーの透明度の追加 (4) として、ビットマップ内に保存しています Adobe の Photoshop で指定されているカラー チャネル。 黒の背景色の解像度についてのクイック ビジュアル キューを提供するすべての 32 ビット BMP ファイルにオブジェクトの実稼動中に追加されます。 この背景を黒には、ui にマスクされる領域を表します。

- **32 ビット ICO:** プロジェクト アイコンと項目の追加。 すべての ICO ファイルは、32 ビットの場合は true。 カラー アルファ チャネル透明度 (RGB/A)。 ICO ファイルは、複数のサイズと色深度を格納するため Vista アイコンは 16 x 16、32 x 32、48 x 48, 256 x 256 の画像のサイズを含む ICO 形式で多くの場合は。 Windows エクスプ ローラーで正しく表示するには ICO ファイルする必要がある保存リスト イメージ サイズごとに 24 ビットと 8 ビットの色深度。

- **XAML:** デザイン サーフェイスと Windows の装飾。 XAML のアイコンは、拡大縮小、回転、ファイリング、および透明度をサポートするベクター ベースのイメージ ファイルです。 これらは、今すぐ Visual Studio では一般的ではないが、柔軟性のため人気になっています。

- **SVG**

- **24 ビット BMP:** Visual Studio のコマンド バーにします。 True-色の RGB イメージ形式、24 ビット BMP は、knock アウト透過性レイヤーの色キーとしてマゼンタ (R = 255, G = 0, B = 255) を使用してレイヤーの透明度を作成する、アイコン規約です。 24 ビット BMP、背景色を使用してすべてのマゼンタ サーフェスが表示されます。

- **24 ビット GIF:** Visual Studio のコマンド バーにします。 透明度をサポートする true 色の RGB イメージ形式。 GIF ファイルは、ウィザードのアートワークや GIF アニメーションでよく使用されます。

### <a name="icon-construction"></a>アイコンの構築
 Visual Studio で最も小さいアイコンのサイズは、16 x 16 です。 最大共通の使用は 32 x 32 です。 アイコンを設計するときに、全体の 16 x 16、24 x 24、または 32 x 32 のフレームがいっぱいにしないに留意してください。 読みやすい、統一されたアイコンの構築は、ユーザーの認識に不可欠です。 アイコンを構築するときに、次の点に準拠します。

- アイコンは、明確でわかりやすく、かつ一貫性のある必要があります。

- 状態通知の要素を 1 つのアイコンとして使用して、アイコンの基本要素の上に重ねることがお勧めします。 特定のコンテキストで、UI は、基本要素と組み合わせて使用状態要素を必要があります。

- プロジェクト アイコンは、通常は、いくつかのサイズが含まれている .ico ファイルです。 16 x 16、24 x 24、および 32 x 32 アイコンのみを更新しています。 ほとんどの 16 x 16、24 x 24 アイコンは、同じ要素が含まれます。 32 x 32 のアイコンには、詳細についてには、該当する場合は、プロジェクトの言語の種類などが含まれます。

- 32 x 32 のアイコンの基本要素では、2 ピクセルの太さが通常があります。 詳細要素の 1 または 2 ピクセル線の太さを使用できます。 最適な判断を使用するより適しているを確認できます。

- 16 x 16 の要素と 24 x 24 アイコンの間、少なくとも 1 ピクセルの間隔があります。 32 x 32 のアイコンの間および修飾子と基本要素の要素間の 2 ピクセルの空白文字を使用します。

  ![16 x 16、24 x 24、および 32 x 32 アイコンのサイズの要素間のスペース](../../extensibility/ux-guidelines/media/0404-47_elementspacing.png "0404 47_ElementSpacing")<br />16 x 16、24 x 24、および 32 x 32 アイコンの要素間のスペースのサイズ

#### <a name="color-and-accessibility"></a>色とアクセシビリティ
 Visual Studio のコンプライアンス ガイドラインでは、製品のすべてのアイコンの色とコントラストのアクセシビリティ要件に合格する必要があります。 これはアイコンの反転によって実現しをデザインするときに注意する必要が製品のプログラムで反転されますある。

 Visual Studio のアイコンの色の使用に関する詳細については、次を参照してください。[イメージの色を使用して](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)します。

## <a name="BKMK_UsingColorInImages"></a> イメージの色を使用してください。

### <a name="overview"></a>概要
 Visual Studio のアイコンは、主にモノクロです。 色は特定の情報を伝達するために予約されていて、装飾のことはありません。 色が使用されます。

- アクションを示す

- 状態の通知をユーザーに警告するには

- 言語への関連付けを指定するには

- IntelliSense 内の項目を区別するために

### <a name="accessibility"></a>ユーザー補助
 Visual Studio のコンプライアンス ガイドラインでは、製品のパスにチェックインされたすべてのアイコンが、色およびコントラストのアクセシビリティ要件を使用することが必要です。 Visual 言語パレットの色は、テストされ、これらの要件を満たしています。

#### <a name="color-inversion-for-dark-themes"></a>ダーク テーマの色の反転
 Visual Studio ダーク テーマで適切なコントラスト比で表示されるアイコンを作成するために、反転がプログラムで適用されます。 正しくを反転するように部分的にこのガイドの色が選択されたしました。 このパレットに色の使用が制限または反転が適用されるときに予期しない結果が得られます。

 ![それぞれの色が反転されているアイコンの例](../../extensibility/ux-guidelines/media/0405-01_darkthemeinversion.png "0405 01_DarkThemeInversion")<br />それぞれの色が反転されているアイコンの例

### <a name="base-palette"></a>基本パレット
 すべての標準アイコンには、次の 3 つの基本色が含まれます。 アイコンは、グラデーションを含んでいないか、ドロップ シャドウなどの 3D ツール アイコンの 1 つまたは 2 つの例外。

|使用法|名前|値 (ライト テーマ)|見本|例|
|-----------|----------|---------------------------|------------|-------------|
|バック グラウンド/濃色|VS BG|424242 / 66,66,66|![見本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|![基本パレットの例](../../extensibility/ux-guidelines/media/0405-02_basepaletteexample.png "0405 02_BasePaletteExample")|
|フォア グラウンド/低負荷|VS FG|F0EFF1 240,239,241/|![見本f0eff1](../../extensibility/ux-guidelines/media/0405_f0eff1.png "0405_F0EFF1")||
|外枠|VS アウト|F6F6F6 / 246,246,246|![見本f6f6f6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")||

 基本の色だけでなく、各アイコンは拡張パレットから 1 つ追加の色を含めることができます。

### <a name="extended-palette"></a>拡張パレット

#### <a name="action-modifiers"></a>操作の修飾子
 次の 4 つの色は、操作の修飾子で必要なアクションの種類を示します。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|正|VS アクション緑|388A34 56,138,52/|![見本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|負|VS アクション赤|A1260D 161,38,13/|![見本 A1260D](../../extensibility/ux-guidelines/media/0405_a1260d.png "0405_A1260D")|
|ニュートラル|VS アクション青|00539 C 0,83,156/|![見本 00539c](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|作成/新しい|VS アクション オレンジ|C27D1A 194,156,26/|![見本c27d1a](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>使用例
 緑は「追加」のような正の操作の修飾子の使用「実行」「プレイ、」と「を検証します」。

|||||
|-|-|-|-|
|![実行アイコン](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405 03_ActionModifierRun")<br />実行|![[クエリ] アイコンを実行](../../extensibility/ux-guidelines/media/0405-04_executequery.png "0405 04_ExecuteQuery")<br />クエリを実行します。|![すべての手順のアイコンを再生](../../extensibility/ux-guidelines/media/0405-05_playallsteps.png "0405 05_PlayAllSteps")<br />すべてのステップを再生します。|![コントロール アイコンを追加](../../extensibility/ux-guidelines/media/0405-06_addcontrol.png "0405 06_AddControl")<br />コントロールを追加します。|

 赤は"Delete、"「停止」と同様に、負の値の操作の修飾子の使用「キャンセル」と「閉じる」。

|||||
|-|-|-|-|
|![[リレーションシップ] アイコンを削除](../../extensibility/ux-guidelines/media/0405-07_deleterelationship.png "0405 07_DeleteRelationship")<br />リレーションシップを削除します。|![[列] アイコンを削除](../../extensibility/ux-guidelines/media/0405-08_deletecolumn.png "0405 08_DeleteColumn")<br />列の削除|![停止クエリ アイコン](../../extensibility/ux-guidelines/media/0405-09_stopquery.png "0405 09_StopQuery")<br />クエリを停止します。|![接続のオフライン アイコン](../../extensibility/ux-guidelines/media/0405-10_connectionoffline.png "0405 10_ConnectionOffline")<br />オフラインの接続|

 青は修飾子を最もよく「開くには、」「次」、"Previous、"などの矢印で示され"Import"、「エクスポート」ニュートラル アクションに適用されます。

|||||
|-|-|-|-|
|![フィールドのアイコンに移動して](../../extensibility/ux-guidelines/media/0405-11_gotofield.png "0405 11_GoToField")<br />フィールドに移動します。|![確認をバッチ処理&#45;アイコン](../../extensibility/ux-guidelines/media/0405-12_batchedcheckin.png "0405 12_BatchedCheckIn")<br />バッチ処理されたチェックイン|![アドレス エディター アイコン](../../extensibility/ux-guidelines/media/0405-13_addresseditor.png "0405 13_AddressEditor")<br />アドレス エディター|![[関連付けエディター] アイコン](../../extensibility/ux-guidelines/media/0405-14_associationeditor.png "0405 14_AssociationEditor")<br />関連付けエディター|

 濃い金は「新規」修飾子は、主に使用します。

|||||
|-|-|-|-|
|![新しいプロジェクト アイコン](../../extensibility/ux-guidelines/media/0405-15_newproject.png "0405 15_NewProject")<br />新しいプロジェクト|![[新しいグラフ] アイコンを作成する](../../extensibility/ux-guidelines/media/0405-16_createnewgraph.png "0405 16_CreateNewGraph")<br />新しいグラフを作成します。|![新しい単体テスト アイコン](../../extensibility/ux-guidelines/media/0405-17_newunittest.png "0405 17_NewUnitTest")<br />新しい単体テスト|![新しいリスト アイテムのアイコン](../../extensibility/ux-guidelines/media/0405-18_newlistitem.png "0405 18_NewListItem")<br />新しいリスト アイテム|

#### <a name="special-cases"></a>特殊なケース
 、特殊なケースで色付きアクション修飾子が単独で使用スタンドアロン アイコンとして。 アイコンを使用する色、アイコンが関連付けられているアクションが反映されます。 このような使用も含め、アイコンの小さなサブセットに制限されています。

||||||
|-|-|-|-|-|
|![実行アイコン](../../extensibility/ux-guidelines/media/0405-03_actionmodifierrun.png "0405 03_ActionModifierRun")<br />実行|![停止アイコン](../../extensibility/ux-guidelines/media/0405-19_stop.png "0405 19_Stop")<br />停止|![削除アイコン](../../extensibility/ux-guidelines/media/0405-20_delete.png "0405 20_Delete")<br />削除|![[保存] アイコン](../../extensibility/ux-guidelines/media/0405-21_save.png "0405 21_Save")<br />保存|![戻るアイコンを移動](../../extensibility/ux-guidelines/media/0405-22_navigateback.png "0405 22_NavigateBack")<br />戻る|

### <a name="code-hierarchy-palette"></a>コード階層パレット

#### <a name="folder"></a>フォルダー

|使用法|名前|値 (すべてのテーマ)|見本|例|
|-----------|----------|--------------------------|------------|-------------|
|フォルダー|フォルダー|DCB67A 220,182,122/|![見本 DCB67A](../../extensibility/ux-guidelines/media/0405_dcb67a.png "0405_DCB67A")|![フォルダーの色のアイコン](../../extensibility/ux-guidelines/media/0405-23_foldercolor.png "0405 23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio の言語
 一般的な言語や Visual Studio で使用可能なプラットフォームの各は、関連付けられた色があります。 これらの色は、基本のアイコンまたは複合アイコンの右上隅に表示される言語修飾子に使用されます。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|ASP では、HTML、WPF|ASP HTML WPF 青|0095D7 / 0,149,215|![見本 0095d7](../../extensibility/ux-guidelines/media/0405_0096d7.png "0405_0096D7")|
|C++|CPP 紫|9B4F96 155,79,150/|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|C#|CS 緑 (VS アクション緑)|388A34 56,138,52/|![見本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|CSS|CSS の赤|BD1E2D 189,30,45/|![見本bd1e2d](../../extensibility/ux-guidelines/media/0405_bd1e2d.png "0405_BD1E2D")|
|F#|FS 紫|672878 / 103,40,120|![見本 672878](../../extensibility/ux-guidelines/media/0405_672878.png "0405_672878")|
|JavaScript|JS オレンジ|F 16421 241,100,33/|![見本 f 16421](../../extensibility/ux-guidelines/media/0405_f16421.png "0405_F16421")|
|VB|VB 青 (VS アクション青)|00539 C 0,83,156/|![見本 00539c](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|TypeScript|TS オレンジ|E04C06 224,76,6/|![見本e04c06](../../extensibility/ux-guidelines/media/0405_e04c06.png "0405_E04C06")|
|Python|PY 緑|879636 / 135,150,54|![見本 879636](../../extensibility/ux-guidelines/media/0405_879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>言語修飾子を持つアイコンの例

|||||||
|-|-|-|-|-|-|
|![Visual Basic アイコン](../../extensibility/ux-guidelines/media/0405-25_vb.png "0405 25_VB")<br />VB|![C&#35;アイコン](../../extensibility/ux-guidelines/media/0405-26_csharp.png "0405 26_CSharp")<br />C#|![C&#43; &#43;アイコン](../../extensibility/ux-guidelines/media/0405-27_cplusplus.png "0405 27_CPlusPlus")<br />C++|![F&#35;アイコン](../../extensibility/ux-guidelines/media/0405-28_fsharp.png "0405 28_FSharp")<br />F#|![JavaScript アイコン](../../extensibility/ux-guidelines/media/0405-29_javascript.png "0405 29_JavaScript")<br />JavaScript|![Python アイコン](../../extensibility/ux-guidelines/media/0405-30_python.png "0405 30_Python")<br />Python|
|![HTML アイコン](../../extensibility/ux-guidelines/media/0405-31_html.png "0405 31_HTML")<br />HTML|![WPF アイコン](../../extensibility/ux-guidelines/media/0405-32_wpf.png "0405 32_WPF")<br />WPF|![ASP アイコン](../../extensibility/ux-guidelines/media/0405-33_asp.png "0405 33_ASP")<br />ASP|![CSS アイコン](../../extensibility/ux-guidelines/media/0405-34_css.png "0405 34_CSS")<br />CSS|![TypeScript アイコン](../../extensibility/ux-guidelines/media/0405-35_typescript.png "0405 35_TypeScript")<br />TypeScript||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense アイコンは、排他的なカラー パレットを使用します。 これらの色は、IntelliSense のポップアップ リスト内のさまざまな項目をすばやく区別やすくために使用されます。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|イベント クラス|VS アクション オレンジ|C27D1A 194,125,26/|![見本c27d1a](../../extensibility/ux-guidelines/media/0405_c27d1a.png "0405_C27D1A")|
|拡張メソッド、メソッド、モジュール、デリゲート|VS アクション紫|652 D 90 101,45,144/|![見本 652d90](../../extensibility/ux-guidelines/media/0405_652d90.png "0405_652D90")|
|フィールド、列挙型項目、マクロ、構造体、共用体の値の型、演算子、インターフェイスします。|VS アクション青|00539 C 0,83,156/|![見本 00539c](../../extensibility/ux-guidelines/media/0405_00539c.png "0405_00539C")|
|Object|VS アクション緑|388A34 56,138,52/|![見本 388A34](../../extensibility/ux-guidelines/media/0405_388a34.png "0405_388A34")|
|定数、例外、列挙型項目、マップ、マップ項目、Namespace、テンプレート、種類の定義|バック グラウンド (VS BG)|424242 / 66,66,66|![見本 424242](../../extensibility/ux-guidelines/media/0405_424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense アイコンの例

||||||
|-|-|-|-|-|
|![IntelliSense クラスのアイコン](../../extensibility/ux-guidelines/media/0405-36_intellisenseclass.png "0405 36_IntelliSenseClass")<br />クラス|![IntelliSense プライベート イベント アイコン](../../extensibility/ux-guidelines/media/0405-37_intellisenseprivateevent.png "0405 37_IntelliSensePrivateEvent")<br />プライベート イベント|![IntelliSense デリゲートのアイコン](../../extensibility/ux-guidelines/media/0405-38_intellisensedelegate.png "0405 38_IntelliSenseDelegate")<br />Delegate|![IntelliSense メソッド フレンドのアイコン](../../extensibility/ux-guidelines/media/0405-39_intellisensemethodfriend.png "0405 39_IntelliSenseMethodFriend")<br />メソッドのフレンド|![フィールド アイコン](../../extensibility/ux-guidelines/media/0405-40_field.png "0405 40_Field")<br />フィールド|
|![IntelliSense には、列挙型項目のアイコンが保護されている](../../extensibility/ux-guidelines/media/0405-41_intellisenseprotectedenumitem.png "0405 41_IntelliSenseProtectedEnumItem")<br />保護された列挙型項目|![IntelliSense オブジェクトのアイコン](../../extensibility/ux-guidelines/media/0405-42_intellisenseobject.png "0405 42_IntelliSenseObject")<br />Object|![IntelliSense テンプレートのアイコン](../../extensibility/ux-guidelines/media/0405-43_intellisensetemplate.png "0405 43_IntelliSenseTemplate")<br />テンプレート|![IntelliSense の例外のショートカット アイコン](../../extensibility/ux-guidelines/media/0405-44_intellisenseexceptionshortcut.png "0405 44_IntelliSenseExceptionShortcut")<br />例外のショートカット||

### <a name="notifications"></a>通知
 Visual Studio での通知は、ステータスを示すために使用されます。 通知パレットは、次の 4 色として白か黒のフォア グラウンドの塗りつぶしのオプションを使用して、次のステータス レベルを使用した通知を定義します。

|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|----------|--------------------------|------------|
|状態: ニュートラル|通知の青 (VS 青)|1BA1E2 27,161,226/|![見本 1BA1E2](../../extensibility/ux-guidelines/media/0405_1ba1e2.png "0405_1BA1E2")|
|状態: 正の値|通知の緑 (VS 緑)|339933 / 51,153,51|![見本 339933](../../extensibility/ux-guidelines/media/0405_339933.png "0405_339933")|
|状態: 負の値|通知の赤 (VS 赤)|E 51400 229,20,0/|![見本 e 51400](../../extensibility/ux-guidelines/media/0405_e51400.png "0405_E51400")|
|状態: 警告|通知黄色 (VS オレンジ色)|FFCC00 255,204,0/|![見本 FFCC00](../../extensibility/ux-guidelines/media/0405_ffcc00.png "0405_FFCC00")|
|前景の塗りつぶし|通知 Black (黒)|000000 / 0,0,0|![見本&#35;000000](../../extensibility/ux-guidelines/media/0405_000000.png "0405_000000")|
|前景の塗りつぶし|通知ホワイト (白)|FFFFFF / 255,255,255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知アイコンの例

|||||
|-|-|-|-|
|![警告アイコン](../../extensibility/ux-guidelines/media/0405-45_alert.png "0405 45_Alert")<br />警告|![警告アイコン](../../extensibility/ux-guidelines/media/0405-48_warning.png "0405 48_Warning")<br />警告|![完了アイコン](../../extensibility/ux-guidelines/media/0405-46_complete.png "0405 46_Complete")<br />完了しました|![停止アイコン](../../extensibility/ux-guidelines/media/0405-47_stop.png "0405 47_Stop")<br />停止|

### <a name="visual-studio-online"></a>Visual Studio Online
 一般に、Visual Studio Online の機能で構成をブラウザーでホストされています。 別の環境で色が異なりますが、スタイルは変わりません。

|グループ化|使用法|名前|値 (すべてのテーマ)|見本|
|-----------|-----------|----------|--------------------------|------------|
|TFS|背景|TFSO BG|656565/ 101, 101, 101|![見本 656565](../../extensibility/ux-guidelines/media/0405_656565.png "0405_656565")|
|TFS|外枠|OUT TFSO|FFFFFF/255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|Napa|背景|白|FFFFFF/255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|モナコ|背景|白|FFFFFF/255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|F12|背景|白|FFFFFF/255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405_ffffff.png "0405_FFFFFF")|
|F12|標準|F12 Grey_Primary|555555 / 85, 85, 85|![見本 555555](../../extensibility/ux-guidelines/media/0405_555555.png "0405_555555")|
|F12|ホバー|F12 Blue_Hover|2279BF / 34,121,191|![見本 2279 bf](../../extensibility/ux-guidelines/media/0405_2279bf.png "0405_2279BF")|
|F12|無効|F12 LtGrey_Disabled|ABABAC 171,171,172/|![見本 ABABAC](../../extensibility/ux-guidelines/media/0405_ababac.png "0405_ABABAC")|
|F12|ポイント時の背景|Bg のマウス ポインターを移動します。|D9EBF7 217,235,247/|![見本d9ebf7](../../extensibility/ux-guidelines/media/0405_d9ebf7.png "0405_D9EBF7")|
|F12|押された状態のバック グラウンド|押された bg|B2D7F0 178,215,240/|![見本b2d7f0](../../extensibility/ux-guidelines/media/0405_b2d7f0.png "0405_B2D7F0")|
|F12|外枠|VS アウト|F6F6F6 / 246,246,246|![見本f6f6f6](../../extensibility/ux-guidelines/media/0405_f6f6f6.png "0405_F6F6F6")|
|F12|情報|情報|00BCF2 0,188,242/|![見本 00BCF2](../../extensibility/ux-guidelines/media/0405_00bcf2.png "0405_00BCF2")|
|F12|警告|警告|F 28300 242,131,0/|![見本 f 28300](../../extensibility/ux-guidelines/media/0405_f28300.png "0405_F28300")|
|F12|エラー/負の値|Error_Negative|E 81123 232,17,35/|![見本 e 81123](../../extensibility/ux-guidelines/media/0405_e81123.png "0405_E81123")|
|F12|開始/正の値|Start_Positive|009E49 0,158,73/|![Swatch 009E49](../../extensibility/ux-guidelines/media/0405_009e49.png "0405_009E49")|
|F12|改行の種類|改行の種類|9B4F96 155,79,150/|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405_9b4f96.png "0405_9B4F96")|
|F12|イベントのマーク|イベントのマーク|A51F00 165,31,0/|![見本 A51F00](../../extensibility/ux-guidelines/media/0405_a51f00.png "0405_A51F00")|
|F12|ユーザー マーク|ユーザー マーク|F 16220 241,98,32/|![見本 f 16220](../../extensibility/ux-guidelines/media/0405_f16220.png "0405_F16220")|

#### <a name="examples-of-visual-studio-online-icons"></a>Visual Studio Online のアイコンの例

|TFS オンライン||||
|----------------|-|-|-|
|![TFS オンライン チームのアイコン](../../extensibility/ux-guidelines/media/0405-49_tfsonlineteam.png "0405 49_TFSOnlineTeam")<br />オンライン チーム|![TFS 情報アイコン](../../extensibility/ux-guidelines/media/0405-50_tfsinformation.png "0405 50_TFSInformation")<br />情報|![TFS 履歴アイコン](../../extensibility/ux-guidelines/media/0405-51_tfshistory.png "0405 51_TFSHistory")<br />履歴|![TFS 分岐アイコン](../../extensibility/ux-guidelines/media/0405-52_tfsbranch.png "0405 52_TFSBranch")<br />分岐|

|Napa||||
|----------|-|-|-|
|![Napa コンテンツ アイコン](../../extensibility/ux-guidelines/media/0405-53_napacontent.png "0405 53_NapaContent")<br />Content|![Napa office メール アイコン](../../extensibility/ux-guidelines/media/0405-54_napaofficemail.png "0405 54_NapaOfficeMail")<br />Office のメール|![Napa SharePoint アイコン](../../extensibility/ux-guidelines/media/0405-55_napasharepoint.png "0405 55_NapaSharePoint")<br />SharePoint|![Napa 作業ウィンドウ アイコン](../../extensibility/ux-guidelines/media/0405-56_napataskpane.png "0405 56_NapaTaskPane")<br />作業ウィンドウ|

|モナコ||||
|------------|-|-|-|
|![モナコ ファイル アイコン](../../extensibility/ux-guidelines/media/0405-57_monacofiles.png "0405 57_MonacoFiles")<br />ファイル|![モナコ Git アイコン](../../extensibility/ux-guidelines/media/0405-58_monacogit.png "0405 58_MonacoGit")<br />Git|![モナコの検索アイコン](../../extensibility/ux-guidelines/media/0405-59_monacosearch.png "0405 59_MonacoSearch")<br />検索|![モナコのテキスト アイコン](../../extensibility/ux-guidelines/media/0405-60_monacotext.png "0405 60_MonacoText")<br />テキスト|

|F12|||
|---------|-|-|
|![F12 再フォーマット コード アイコン](../../extensibility/ux-guidelines/media/0405-61_f12prettycode.png "0405 61_F12PrettyCode")<br />再フォーマット コード|![F12 警告アイコン](../../extensibility/ux-guidelines/media/0405-62_f12warning.png "0405 62_F12Warning")<br />警告|![F12 エミュレート アイコン](../../extensibility/ux-guidelines/media/0405-63_f12emulate.png "0405 63_F12Emulate")<br />エミュレート|