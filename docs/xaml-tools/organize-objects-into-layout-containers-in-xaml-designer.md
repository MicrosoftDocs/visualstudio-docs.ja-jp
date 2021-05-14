---
title: オブジェクトのレイアウト コンテナーへの編成
description: XAML デザイナーで、Grid、Canvas、Border、Viewbox など、ページ上のオブジェクトを配置するために使用されるレイアウトのパネルとコントロールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 07/17/2020
ms.topic: conceptual
ms.assetid: 29c80c38-0fa3-48d6-b3a8-3b864f482e44
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: d42a7509ceef03d2e74f470d7d4ab0efb5913e13
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900844"
---
# <a name="organize-objects-into-layout-containers-in-xaml-designer"></a>XAML デザイナーでレイアウト コンテナーにオブジェクトを編成する

この記事では、XAML デザイナーのレイアウト パネルとコントロールについて説明します。

イメージ、ボタン、ビデオなどのオブジェクトをページ上のどこに表示させたいか想像してください。 縦か横の単一行の行列、または固定位置に表示させたいのではないでしょうか。

ページの表示方法について考える段階になったら、レイアウト パネルを選択します。 オブジェクトを追加するための何かが必要になるため、すべてのページはあるものから開始します。 これは既定では **グリッド** ですが、変更しても構いません。

レイアウト パネルでは、ページ上にオブジェクトを配置できますが、それ以上のことができます。 さまざまな画面サイズと解像度で設計するのに役立ちます。 ユーザーが自分のアプリを実行する際、デバイスの実際の画面と一致させるためにレイアウト パネル内のすべてのものがサイズ変更されます。 もちろん、レイアウトのサイズ変更をしたくない場合は、レイアウトの一部または全体の動作をオーバーライドできます。 これを制御するには、高さと幅のプロパティを使用します。

## <a name="layout-panels"></a>レイアウト パネル

いずれかのレイアウト パネルを選択して、ページを開始します。 ページは、複数にすることができます。 たとえば、**グリッド** レイアウト パネルで開始してから **StackPanel** を **グリッド** 内の領域に追加することがあります。そうすることで、その要素内でコントロールを縦方向に配置できます。

次のレイアウト パネルは最もよく使用されますが、他にもレイアウト パネルがあります。 Visual Studio の **ツールボックス** または Blend for Visual Studio の **[資産]** パネルでこれらすべてを見つけることができます。

### <a name="grid"></a>グリッド

行と列にオブジェクトを配置します。

![グリッド レイアウト パネル](../designers/media/98b234b2-ac3b-441f-9136-98375fee87b7.png)

### <a name="uniformgrid"></a>UniformGrid

オブジェクトを等しい、統一されたグリッド領域に配置します。 このパネルは、イメージの一覧を配置するのに適しています。

(WPF プロジェクトでのみ使用可能)

![UniformGrid レイアウト パネル](../designers/media/928b9284-a7e8-4678-875a-656b80b78076.png)

### <a name="canvas"></a>キャンバス

任意の方法でオブジェクトを配置します。 ユーザーがアプリを実行しているとき、これらの要素は画面上の固定位置にあります。

![キャンバス レイアウト パネル](../designers/media/e1ae27f0-3a57-454e-b580-877dcea8836d.png)

### <a name="stackpanel"></a>StackPanel

横方向または縦方向の単一行にオブジェクトを配置します。

![StackPanel レイアウト パネル](../designers/media/a85a7b57-b0a8-495e-b985-f0291e41d093.png)

### <a name="wrappanel"></a>WrapPanel

左から右へ順番にオブジェクトを配置します。 パネルの右端に余地がない場合、コンテンツを次の行に *折り返し* ます。同様に左から右、上から下へ実行します。 上から下、左から右へオブジェクトが流れるよう、[折り返し] パネルの向きを縦方向にすることもできます。

(WPF プロジェクトでのみ使用可能)

![WrapPanel レイアウト パネル](../designers/media/b1c415fb-9a32-4a18-aa0b-308fca994ac9.png)

### <a name="dockpanel"></a>DockPanel

オブジェクトをパネルの 1 辺に沿うように (*ドッキング* して) 整列します。

(WPF プロジェクトでのみ使用可能)

![DockPanel レイアウト パネル](../designers/media/72d46b58-9a49-4dd5-8af7-6843c0440226.png)

**短いビデオを見る:** ![再生ボタン](../designers/media/bldadminconsoleinitialconfigicon.PNG) [WPF - DockPanel](https://www.youtube.com/watch?v=EBH_OIM-zPo)

## <a name="layout-controls"></a>レイアウト コントロール

オブジェクトをレイアウト コントロールに追加することもできます。 レイアウト パネルほど機能が豊富ではありませんが、特定のシナリオで役立つことがあります。

次のレイアウト コントロールは最もよく利用されますが、他にもレイアウト コントロールがあります。 Visual Studio の **ツールボックス** または Blend for Visual Studio の **[資産]** パネルでこれらすべてを見つけることができます。

### <a name="border"></a>境界線

罫線、背景、またはその両方をオブジェクトの周りに作成します。 **境界線** に対して追加できるオブジェクトは 1 つのみです。 複数のオブジェクトに境界線や背景を適用する場合は、レイアウト パネルを **境界線** に追加します。 次に、オブジェクトをそのパネルまたはコントロールに追加します。

![Border レイアウト コントロール](../designers/media/e761238b-99fd-43c5-bbc4-57538b8289ff.png)

### <a name="popup"></a>ポップアップ

ウィンドウで情報またはオプションをユーザーに表示します。 **ポップアップ** に対して追加できるオブジェクトは 1 つのみです。 既定では、**ポップアップ** には **グリッド** が含まれていますが、これは変更することができます。

### <a name="scrollviewer"></a>ScrollViewer

ページまたはページの領域を下にスクロールできるようになります。 **ScrollViewer** に追加できるオブジェクトは 1 つのみであるため、**グリッド** や **StackPanel** などのレイアウト パネルを追加することには意味があります。

![ScrollViewer レイアウト コントロール](../designers/media/06b326d4-f23d-41a6-b26b-e1aff37572a7.png)

### <a name="viewbox"></a>Viewbox

ズーム コントロールのようにオブジェクトを拡大または縮小します。 **ViewBox** に対して追加できるオブジェクトは 1 つのみです。 複数のオブジェクトにその効果を適用する場合は、レイアウト パネルを **ViewBox** に追加してから、コントロールをそのレイアウト パネルに追加します。

![ViewBox レイアウト コントロール](../designers/media/f5b13c66-d918-4141-8a16-bd8f8628687a.png)

## <a name="see-also"></a>関連項目

- [XAML デザイナーで要素を操作する](../xaml-tools/working-with-elements-in-xaml-designer.md)
- [XAML デザイナーを使用して UI を作成する](../xaml-tools/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
