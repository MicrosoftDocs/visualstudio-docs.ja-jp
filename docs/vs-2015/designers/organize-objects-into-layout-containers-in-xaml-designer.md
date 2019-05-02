﻿---
title: XAML デザイナーでレイアウト コンテナーにオブジェクトを編成する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 29c80c38-0fa3-48d6-b3a8-3b864f482e44
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5c2aef08695d2cea04d23a343d318680bc53f44c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432600"
---
# <a name="organize-objects-into-layout-containers-in-xaml-designer"></a>XAML デザイナーでレイアウト コンテナーにオブジェクトを編成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

イメージ、ボタン、ビデオなどのオブジェクトをどこに表示させたいか想像してください。 縦か横の単一行の行列、または固定位置に表示させたいのではないでしょうか。  
  
 ページをどのように表示するかについて考える機会が得られたら、レイアウト パネルを選択します。 オブジェクトを追加するための何かが必要になるため、すべてのページはあるものから開始します。 これは既定では**グリッド**ですが、変更しても構いません。  
  
 レイアウト パネルでは、ページ上にオブジェクトを配置できますが、それ以上のことができます。 さまざまな画面サイズと解像度で設計するのに役立ちます。 ユーザーが自分のアプリを実行する際、デバイスの実際の画面と一致させるためにレイアウト パネル内のすべてのものがサイズ変更されます。 もちろん、レイアウトのサイズ変更をしたくない場合は、レイアウトの一部または全体の動作をオーバーライドできます。 これを制御するには、高さと幅のプロパティを使用します。  
  
 このページでは、レイアウト パネルとコントロールについて説明した後、パネルとコントロールの使用を開始する助けとなる短いビデオに移ります。  
  
> [!NOTE]
> 一部のビデオでは Blend や Expression Blend に言及していることがありますが、それらのツールでは Visual Studio および Blend for Visual Studio と同じ XAML デザイナーを使用します。  
  
## <a name="layout-panels"></a>レイアウト パネル  
 いずれかのレイアウト パネルを選択して、ページを開始します。 ページは、複数にすることができます。 たとえば、**グリッド** レイアウト パネルで開始してから **StackPanel** を**グリッド**内の領域に追加することがあります。そうすることで、その要素内でコントロールを縦方向に配置できます。  
  
 次のレイアウト パネルは最もよく使用されますが、他にもレイアウト パネルがあります。 すべてのレイアウト コントロールは **[アセット]** パネルにあります。  
  
- [グリッド](#Grid)  
  
- [UniformGrid](#Uniform)  
  
- [Canvas](#Canvas)  
  
- [StackPanel](#Stack)  
  
- [WrapPanel](#Wrap)  
  
- [DockPanel](#Dock)  
  
### <a name="Grid"></a> グリッド  
 行と列にオブジェクトを配置します。  
  
 ![](../designers/media/98b234b2-ac3b-441f-9136-98375fee87b7.png "98b234b2-ac3b-441f-9136-98375fee87b7")  
  
 **短いビデオを見る:**![インストールされている機能を構成する](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [グリッドの使用](http://www.popscreen.com/v/6A4hj/Microsoft-Expression-Blend-Using-Grids)  
  
### <a name="Uniform"></a> UniformGrid  
 オブジェクトを等しい、統一されたグリッド領域に配置します。 このパネルは、イメージの一覧を配置するのに適しています。  
  
 ![](../designers/media/928b9284-a7e8-4678-875a-656b80b78076.png "928b9284-a7e8-4678-875a-656b80b78076")  
  
 (WPF プロジェクトでのみ使用可能)  
  
 **短いビデオを見る:**![インストールされている機能を構成する](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [UniformGrid での作業](http://www.popscreen.com/v/6A4iq/Microsoft-Expression-Blend-Working-with-a-UniformGrid)  
  
### <a name="Canvas"></a> キャンバス  
 任意の方法でオブジェクトを配置します。 ユーザーがアプリを実行しているとき、これらの要素は画面上の固定位置にあります。  
  
 ![](../designers/media/e1ae27f0-3a57-454e-b580-877dcea8836d.png "e1ae27f0-3a57-454e-b580-877dcea8836d")  
  
 **短いビデオを見る:**![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [キャンバスでの作業](http://www.popscreen.com/v/6A4hT/Microsoft-Expression-Blend-Working-with-the-Canvas)  
  
### <a name="Stack"></a> StackPanel  
 横方向または縦方向の単一行にオブジェクトを配置します。  
  
 ![](../designers/media/a85a7b57-b0a8-495e-b985-f0291e41d093.png "a85a7b57-b0a8-495e-b985-f0291e41d093")  
  
 **短いビデオを見る:**![インストールされている機能を構成する](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [StackPanel と WrapPanel での操作](http://www.popscreen.com/v/6A4i5/Microsoft-Expression-Blend-Using-the-StackPanel-and-WrapPanel)  
  
### <a name="Wrap"></a> WrapPanel  
 左から右へ順番にオブジェクトを配置します。 パネルの右端に余地がない場合、コンテンツを次の行に*折り返し*ます。同様に左から右、上から下へ実行します。 上から下、左から右へオブジェクトが流れるよう、[折り返し] パネルの向きを縦方向にすることもできます。  
  
 (WPF プロジェクトでのみ使用可能)  
  
 ![](../designers/media/b1c415fb-9a32-4a18-aa0b-308fca994ac9.png "b1c415fb-9a32-4a18-aa0b-308fca994ac9")  
  
 **短いビデオを見る:**![インストールされている機能を構成する](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [StackPanel と WrapPanel での操作](http://www.popscreen.com/v/6A4i5/Microsoft-Expression-Blend-Using-the-StackPanel-and-WrapPanel)  
  
### <a name="Dock"></a> DockPanel  
 オブジェクトをパネルの 1 辺に沿うように (*ドッキング*して) 整列します。  
  
 (WPF プロジェクトでのみ使用可能)  
  
 ![](../designers/media/72d46b58-9a49-4dd5-8af7-6843c0440226.png "72d46b58-9a49-4dd5-8af7-6843c0440226")  
  
 **短いビデオを見る:**![インストールされている機能を構成する](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [WPF - DockPanel](https://www.youtube.com/watch?v=EBH_OIM-zPo)  
  
## <a name="layout-controls"></a>レイアウト コントロール  
 オブジェクトをレイアウト コントロールに追加することもできます。 レイアウト パネルほど機能が豊富ではありませんが、特定のシナリオで役立つことがあります。  
  
 次のレイアウト コントロールは最もよく使用されますが、他にもレイアウト コントロールがあります。 すべてのレイアウト コントロールは **[アセット]** パネルにあります。  
  
- [Border](#Border)  
  
- [Popup](#Popup)  
  
- [ScrollViewer](#Scroll)  
  
- [UniformGrid](#Uniform)  
  
- [Viewbox](#View)  
  
### <a name="Border"></a> 境界線  
 罫線、背景、またはその両方をオブジェクトの周りに作成します。 **境界線**に対して追加できるオブジェクトは 1 つのみです。 複数のオブジェクトに境界線や背景を適用する場合は、レイアウト パネルを**境界線**に追加します。 次に、オブジェクトをそのパネルまたはコントロールに追加します。  
  
 ![](../designers/media/e761238b-99fd-43c5-bbc4-57538b8289ff.png "e761238b-99fd-43c5-bbc4-57538b8289ff")  
  
 **短いビデオを見る:**![インストールされている機能を構成する](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [境界線での作業](http://www.popscreen.com/v/6A4hB/Microsoft-Expression-Blend-Working-with-Borders)  
  
### <a name="Popup"></a> ポップアップ  
 ウィンドウで情報またはオプションをユーザーに表示します。 **ポップアップ**に対して追加できるオブジェクトは 1 つのみです。 既定では、**ポップアップ**には**グリッド**が含まれていますが、これは変更することができます。  
  
### <a name="Scroll"></a> ScrollViewer  
 ページまたはページの領域を下にスクロールできるようになります。 **ScrollViewer** に追加できるオブジェクトは 1 つのみであるため、**グリッド**や **StackPanel** などのレイアウト パネルを追加することには大きな意味があります。  
  
 ![](../designers/media/06b326d4-f23d-41a6-b26b-e1aff37572a7.png "06b326d4-f23d-41a6-b26b-e1aff37572a7")  
  
### <a name="View"></a> Viewbox  
 ズーム コントロールのようにオブジェクトを拡大または縮小します。 **ViewBox** に対して追加できるオブジェクトは 1 つのみです。 複数のオブジェクトにその効果を適用する場合は、レイアウト パネルを **ViewBox** に追加してから、コントロールをそのレイアウト パネルに追加します。  
  
 (WPF プロジェクトでのみ使用可能)  
  
 ![](../designers/media/f5b13c66-d918-4141-8a16-bd8f8628687a.png "f5b13c66-d918-4141-8a16-bd8f8628687a")  
  
## <a name="see-also"></a>関連項目
 [Working with elements in XAML Designer](../designers/working-with-elements-in-xaml-designer.md)   
 [XAML デザイナーを使用した UI の作成](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
