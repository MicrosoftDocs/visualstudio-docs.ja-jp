---
title: XAML デザイナーでの要素の操作
description: Visual Studio または Blend for Visual Studio の XAML デザイナーで要素を操作する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/14/2018
ms.topic: conceptual
ms.assetid: a29690bf-f212-4ac6-a77a-adc53d14102e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 1af793ec7ecd741de1fc1b4bb1cb48dbf2ef32f3
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93047123"
---
# <a name="work-with-elements-in-xaml-designer"></a>XAML デザイナーで要素を操作する

XAML で、コードで、または XAML デザイナーを使用して、アプリに要素 (コントロール、レイアウト、および図形) を追加できます。 このトピックでは、Visual Studio または Blend for Visual Studio で XAML デザイナーを使用して要素を操作する方法について説明します。

## <a name="add-an-element-to-a-layout"></a>レイアウトに要素を追加する

*レイアウト* とは、UI に要素を配置してサイズ変更するプロセスです。 ビジュアル要素を配置するには、それらを [Panel](xref:Windows.UI.Xaml.Controls.Panel) レイアウトに配置する必要があります。 `Panel` には、[FrameworkElement](xref:Windows.UI.Xaml.FrameworkElement) 型のコレクションである子プロパティがあります。 `Panel` のさまざまな子要素 ([Canvas](xref:Windows.UI.Xaml.Controls.Canvas)、[StackPanel](xref:Windows.UI.Xaml.Controls.StackPanel)、[Grid](xref:Windows.UI.Xaml.Controls.Grid) など) をレイアウト コンテナーとして利用し、ページに要素を配置して整列することができます。

既定では、`Grid` パネルをページまたはフォーム内の最上位のレイアウト コンテナーとして使用します。 最上位のページ レイアウト内で、レイアウト パネル、コントロール、またはその他の要素を追加できます。

XAML デザイナーでレイアウトに要素を追加するには、次のいずれかの操作を行います。

- **[ツールボックス]** にある要素をダブルクリックします (または、ツールボックスにある要素を選択して **Enter** キーを押します)。

- 要素を **[ツールボックス]** からアートボードにドラッグします。

- **[ツールボックス]** で、いずれかの描画ツール ( [[楕円]](xref:Windows.UI.Xaml.Shapes.Ellipse) や [[四角形]](xref:Windows.UI.Xaml.Shapes.Rectangle) など) を選択し、アクティブなパネルに要素を描画します。

## <a name="change-the-layering-order-of-elements"></a>要素の重ね順を変更する

XAML デザイナーのアートボード上に要素が 2 つある場合は、重ね順に従って、一方の要素が他方の前に表示されます。 [ドキュメント アウトライン] ウィンドウで要素の一覧の最下位にある要素が最前面の要素です (要素の **[ZIndex]** プロパティが設定されている場合を除く)。 ページ、フォーム、またはレイアウト コンテナーに要素を挿入するとき、自動的に要素はアクティブなコンテナー要素内の他の要素より前面に配置されます。 要素の順序を変更するには、 **[順序]** コマンドを使用するか、[ドキュメント アウトライン] ウィンドウのオブジェクト ツリーで要素をドラッグします。

重ね順を変更するには、次のいずれかの操作を行います。

- **[ドキュメント アウトライン]** ウィンドウで要素を上下にドラッグして目的の重ね順を作成します。

- 重ね順を変更する要素を [ドキュメント アウトライン] ウィンドウまたはアートボードで右クリックし、 **[順序]** をポイントした後、次のいずれかをクリックします。

  - **[最前面へ移動]** : 要素を重ね順の一番前に移動します。

  - **[前面へ移動]** : 要素を重ね順の 1 つ前に移動します。

  - **[背面へ移動]** : 要素を重ね順の 1 つ後ろに移動します。

  - **[最背面へ移動]** : 要素を重ね順の一番後ろに移動します。

- [プロパティ] ウィンドウの **[レイアウト]** セクションで **[ZIndex]** プロパティを変更します。 要素が重なり合うときは、 **[ZIndex]** プロパティのほうが、[ドキュメント アウトライン] ウィンドウに表示される要素の順序よりも優先されます。 **[ZIndex]** 値が大きい要素ほど、他の要素より前に表示されます。

## <a name="change-the-alignment-of-an-element"></a>要素の配置を変更する

アートボードで要素の配置を調整するには、メニュー コマンドを使用するか、要素をスナップ ガイドラインに沿ってドラッグします。

*スナップ ガイドライン* は、アプリ内の他の要素に対して要素を整列させる場合に役立つ視覚上の手掛かりです。

メニュー コマンドを使用して 2 つ以上の要素の位置を揃えるには

1. 整列させる要素を選択します。 複数の要素を選択するには、 **Ctrl** キーを押したまま、要素を選択します。

2. [プロパティ] ウィンドウの **[レイアウト]** セクションの **[HorizontalAlignment]** で、次のいずれかを選択します: **[Left]** 、 **[Center]** 、 **[Right]** 、または **[Stretch]** 。

3. [プロパティ] ウィンドウの **[レイアウト]** セクションの **[VerticalAlignment]** で、次のいずれかを選択します: **[Top]** 、 **[Center]** 、 **[Bottom]** 、または **[Stretch]** 。

スナップ ガイドラインを使用して 2 つ以上の要素の位置を揃えるには、XAML デザイナーで、レイアウトに少なくとも 2 つの要素が含まれている場合、1 つの要素がもう 1 つの要素の端と揃うようにドラッグしたりサイズを変更したりすることができます。

端が揃うと、合図として *位置揃えライン* が表示されます。 配置境界は、赤い破線です。 位置揃えラインは、 **[スナップ ガイドラインへのスナップ]** が有効に設定されている場合にのみ表示されます。 位置揃えラインが表示されたアートボードの図解は、「[XAML デザイナーを使用した UI の作成](../xaml-tools/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)」をご覧ください。

## <a name="change-an-elements-margins"></a>要素の余白を変更する

XAML デザイナーの余白によって、アートボード上の要素の周囲にある空白領域の量が決まります。 たとえば、要素の外側の端と、その要素を格納している `Grid` パネルの境界との間の領域の大きさが、余白によって指定されます。 または、余白によって、`StackPanel` に含まれる各要素間の領域の大きさが指定されます。

プロパティ ウィンドウで要素の余白を変更するには

1. 余白を変更する要素を選択します。

2. [プロパティ] ウィンドウの **[レイアウト]** で、いずれかの **[Margin]** プロパティ ( **[Top]** 、 **[Left]** 、 **[Right]** 、 **[Bottom]** ) の値 (単位はピクセル。デバイスに依存しない単位。約 1/96 インチ) を変更します。

アートボードで、要素のレイアウト コンテナーを基準として要素の余白を変更するには、レイアウト コンテナー内にある要素を選択したときに要素の周りに表示される *余白ガイド* をクリックします。 余白ガイドを示す図解は、「[XAML デザイナーを使用した UI の作成](../xaml-tools/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)」をご覧ください。

余白ガイドが縦または横に開いている場合は、余白が設定されていません。 余白ガイドが閉じている場合は、余白が設定されています。

余白ガイドを開いた場合に、反対側の余白が設定されていないと、アートボード上での要素の位置に従って正しい値が反対側の余白に設定されます。 **[Left]** と **[Right]** の余白のような向かい側の余白の場合は、少なくとも一方のプロパティが常に設定されます。

> [!IMPORTANT]
> 一部のレイアウト コンテナー([Canvas](xref:Windows.UI.Xaml.Controls.Canvas) など) に配置する要素には、空白ガイドがありません。 [StackPanel](xref:Windows.UI.Xaml.Controls.StackPanel) の内部に配置された要素には、`StackPanel` の向きに応じて、左右の余白または上下の余白に余白ガイドがあります。

## <a name="group-and-ungroup-elements"></a>要素のグループ化とグループ化解除

XAML デザイナーの複数の要素をグループ化すると、新しいレイアウト コンテナーが作成され、そのコンテナー内にそれらの要素が配置されます。 複数の要素を 1 つのレイアウト コンテナーにまとめて配置すると、そのグループ内の複数の要素を、単一の要素のように簡単に選択、移動、および変換できます。 グループ化は、相互に関係のある複数の要素 (1 つのナビゲーション要素を構成する各ボタンなど) をまとめて扱う場合も便利です。 要素のグループ化を解除する場合は、それらの要素を含むレイアウト コンテナーを削除するだけです。

要素を新しいレイアウト コンテナーに入れてグループ化するには

1. グループ化する要素を選択します。 (複数の要素を選択するには、 **Ctrl** キーを押しながらクリックします。)

2. 選択した要素を右クリックし、 **[グループ (パネル) に含める]** をポイントし、そのグループを配置するレイアウト コンテナーの種類をクリックします。

    > [!TIP]
    > [[Viewbox]](xref:Windows.UI.Xaml.Controls.Viewbox)、[[Border]](xref:Windows.UI.Xaml.Controls.Border)、または [[ScrollViewer]](xref:Windows.UI.Xaml.Controls.ScrollViewer) を選択して要素をグループ化する場合、要素は [Viewbox](xref:Windows.UI.Xaml.Controls.Viewbox)、[Border](xref:Windows.UI.Xaml.Controls.Border)、[ScrollViewer](xref:Windows.UI.Xaml.Controls.ScrollViewer) 内の新しい [[グリッド]](xref:Windows.UI.Xaml.Controls.Grid) パネルに配置されます。 これらのレイアウト コンテナーのいずれかの要素のグループ化を解除すると、[Viewbox](xref:Windows.UI.Xaml.Controls.Viewbox)、[Border](xref:Windows.UI.Xaml.Controls.Border)、[ScrollViewer](xref:Windows.UI.Xaml.Controls.ScrollViewer) のみが削除され、[[グリッド]](xref:Windows.UI.Xaml.Controls.Grid) パネルは削除されません。 `Grid` パネルを削除するには、要素のグループ化を再度解除します。

要素のグループ化を解除してレイアウトを削除するには、グループ化を解除するグループを右クリックして、 **[グループ化解除]** をクリックします。 要素のグループ化やグループ解除を行うには、[ドキュメント アウトライン] ウィンドウで選択したアイテムを右クリックして、 **[グループ (パネル) に含める]** または **[グループ解除]** をクリックします。

## <a name="reset-the-element-layout"></a>要素のレイアウトをリセットする

要素の特定のレイアウト プロパティを既定値に戻すには、レイアウトのリセットのコマンドを使用します。 このコマンドを使用すると、要素の余白、配置、幅、高さ、およびサイズを、個別に、またはまとめてリセットできます。

要素のレイアウトをリセットするには、[ドキュメントアウトライン] ウィンドウまたはアートボードで要素を右クリックし、[ **レイアウト** ]  >  **reset** *PropertyName* を選択します。ここで、 *PropertyName* はリセットするプロパティです (または、[ **レイアウト** のリセット] を選択して  >  **Reset All** 要素のすべてのレイアウトプロパティをリセットします)。

## <a name="see-also"></a>関連項目

- [XAML デザイナーを使用して UI を作成する](../xaml-tools/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
