---
title: DPI の問題 2 への対処 | Microsoft Docs
description: コンテンツの拡大、レイアウトの問題、DPI スケール API の使用など、高解像度画面のプログラミングに伴う問題について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9cf7b4fe19cdefe11b77de1418b16454089f45c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097514"
---
# <a name="address-dpi-issues"></a>DPI の問題に対処する
"高解像度" 画面を備えたデバイスの出荷数がますます増加しています。 これらの画面は、一般に、1 インチあたりのピクセル数 (ppi) が 200 を超えています。 これらのコンピューターでアプリケーションを操作するときには、そのデバイスの通常の表示距離でコンテンツを表示するニーズを満たすために、コンテンツをスケール アップする必要があります。 2014 年時点で、高密度ディスプレイの主要ターゲットは、モバイル コンピューティング デバイス (タブレット、クラムシェル ラップトップ、携帯電話) です。

Windows 8.1 以降には、これらのマシンが、マシンが接続されているディスプレイと環境を使用して、高密度と標準密度のどちらもディスプレイでも同時に動作できるようにする機能がいくつか用意されています。

- Windows では、[テキストやその他の項目の大きな変更] 設定 (Windows XP 以降で使用可能) を使用して、デバイスに合わせてコンテンツを拡大縮小することができます。

- Windows 8.1 以降では、ほとんどのアプリケーションについて、異なるピクセル密度のディスプレイ間を移動したときに一貫性が保たれるようにコンテンツが自動的に拡大縮小されます。 プライマリ ディスプレイが高密度 (200% スケール) で、セカンダリ ディスプレイが標準密度 (100%) の場合、アプリケーション ウィンドウのコンテンツは、Windows により、セカンダリ ディスプレイでは自動的に縮小されます (アプリケーションによってレンダリングされる 4 ピクセルごとに 1 ピクセルが表示されます)。

- Windows では、既定で、ディスプレイのピクセル密度と表示距離に対する適切な拡大縮小が設定されます (Windows 7 以降は OEM が構成可能)。

- Windows では、280 ppi を超える新しいデバイスで、最大 250% までコンテンツを自動的に拡大できます (Windows 8.1 S14 時点)。

  Windows には、ピクセル数の増加を活用するために、UI の拡大を処理する方法が用意されています。 アプリケーションは、それ自体が "システム DPI 対応" であると宣言することで、このシステムに加わります。 これを行わないアプリケーションは、システムによって拡大されます。 これにより、アプリケーション全体でピクセルが一様に引き伸ばされた、"ぼやけた" ユーザー エクスペリエンスとなる可能性があります。 次に例を示します。

  ![DPI 問題 (ファジー)](../extensibility/media/dpi-issues-fuzzy.png "DPI 問題 (ファジー)")

  Visual Studio は DPI スケール対応になっているため、"仮想化" されません。

  Windows (および Visual Studio) では、いくつかの UI テクノロジを利用しています。これらは、システムによって設定される倍率を処理するさまざまな方法を備えています。 次に例を示します。

- WPF では、デバイスに依存しない方法 (ピクセルではなく単位) でコントロールが測定されます。 WPF UI は、現在の DPI に合わせて自動的に拡大されます。

- すべてのテキスト サイズは、UI フレームワークとは無関係にポイント単位で表現されます。そのため、システムでは DPI 依存として扱われます。 Win32、WinForms、WPF のテキストは、ディスプレイ デバイスに描画される時点で既に適切に拡大されています。

- Win32/WinForms のダイアログとウィンドウには、テキストのあるレイアウトのサイズ変更を可能にする手段が用意されます (たとえばグリッド、フロー、テーブル レイアウト パネルによって)。 これにより、フォント サイズが拡大されたときに拡大されない、ピクセル位置のハードコーディングをしないで済みます。

- システム メトリックに基づいてシステムまたはリソースによって提供されるアイコン (SM_CXICON や SM_CXSMICON など) は、既に拡大されています。

## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>以前の Win32 (GDI、GDI+) と WinForms ベースの UI
WPF は既に高 DPI に対応していますが、Win32/GDI ベースのコードの多くは、当初 DPI 対応を考慮して記述されてはいませんでした。 Windows では、DPI スケーリング API が提供されてきました。 Win32 の問題に対する修正プログラムでは、製品全体で一貫してこれらを使用する必要があります。 Visual Studio では、機能の重複を回避し、製品全体の一貫性を確保するため、ヘルパー クラス ライブラリが提供されてきました。

## <a name="high-resolution-images"></a>高解像度画像
このセクションは主に、Visual Studio 2013 の拡張を行う開発者を対象としています。 Visual Studio 2015 の場合は、Visual Studio に組み込まれているイメージ サービスを使用します。 多くのバージョンの Visual Studio をサポートしたりターゲットとしたりする必要もある場合が考えられるため、2015 のイメージ サービスを使用することは選択肢ではありません。このサービスは以前のバージョンには存在しないためです。 このセクションも参考にしてください。

## <a name="scaling-up-images-that-are-too-small"></a>小さすぎる画像の拡大
小さすぎる画像は、いくつかの一般的な方法を使用して、GDI や WPF で拡大とレンダリングを行うことができます。 アイコン、ビットマップ、イメージストリップ、イメージリストの拡大に対応するため、マネージド DPI ヘルパー クラスが内部および外部の Visual Studio インテグレーターに提供されています。 HICON、HBITMAP、HIMAGELIST、VsUI::GdiplusImage の拡大には、Win32 ベースのネイティブ C/C++ ヘルパーを使用できます。 ビットマップを拡大するために必要なのは、通常、ヘルパー ライブラリへの参照を含めた後の 1 行の変更だけです。 次に例を示します。

```cpp
(Unmanaged) VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);
```

```csharp
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);
```

イメージリストの拡大は、読み込み時にイメージリストが完成しているか、実行時に追加されるかによって異なります。 読み込み時に完成している場合は、ビットマップの場合と同様に、イメージリストを使用して `LogicalToDeviceUnits()` を呼び出します。 イメージリストを作成する前に個々のビットマップをコードで読み込む必要がある場合は、イメージリストの画像サイズを必ず拡大します。

```csharp
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);
```

ネイティブ コードでは、イメージリストの作成時に次のようにディメンションを拡大できます。

```cpp
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);
```

ライブラリの関数を使用すると、サイズ変更アルゴリズムを指定できます。 イメージリストに置かれる画像を拡大するときは、透明度に使用する背景色を必ず指定するか、NearestNeighbor の拡大を使用します (この場合は 125% と 150% でゆがみが発生します)。

MSDN で <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> のドキュメントを参照してください。

次の表は、対応する DPI スケール ファクターでどのように画像を拡大する必要があるかの例を示しています。 オレンジ色で囲まれた画像が、Visual Studio 2013 (100% ～ 200% の DPI スケール) の時点でのベスト プラクティスを示しています。

![DPI 問題 (スケーリング)](../extensibility/media/dpi-issues-scaling.png "DPI 問題 (スケーリング)")

## <a name="layout-issues"></a>レイアウトに関する問題
よくあるレイアウトの問題は、第一に (具体的にはピクセル単位での) 絶対位置を使用するのではなく、UI で拡大された相互に相対的なポイントを維持することで回避できます。 次に例を示します。

- 拡大された画像が考慮されるように、レイアウトやテキストの位置を調整する必要があります。

- グリッド内の列の幅を、拡大されたテキストの幅に合わせて調整する必要があります。

- ハードコーディングされたサイズや要素間のスペースも拡大する必要があります。 フォントは自動的に拡大されるため、テキストのディメンションだけに基づくサイズについては通常は問題がありせん。

  <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> クラスでは、X 軸と Y 軸の拡大縮小を可能にするヘルパー関数を使用できます。

- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (X/Y 軸での拡大縮小を可能にする関数)

- int space = DpiHelper.LogicalToDeviceUnitsX (10);

- int height = VsUI::DpiHelper::LogicalToDeviceUnitsY(5);

  四角形、ポイント、サイズなどのオブジェクトの拡大縮小を可能にする LogicalToDeviceUnits のオーバーロードがあります。

## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>DPIHelper ライブラリ/クラスを使用した画像とレイアウトの拡大縮小
Visual Studio DPI ヘルパー ライブラリは、ネイティブ形式とマネージド形式で使用でき、Visual Studio シェルの外部で、他のアプリケーションによって使用できます。

ライブラリを使用するには、[Visual Studio の VSSDK 拡張機能のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)にアクセスして、High-DPI_Images_Icons サンプルをクローンします。

ソース ファイルに *VsUIDpiHelper.h* をインクルードして、`VsUI::DpiHelper` クラスの静的関数を呼び出します。

```cpp
#include "VsUIDpiHelper.h"

int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);

```

> [!NOTE]
> ヘルパー関数は、モジュール レベルまたはクラス レベルの静的変数では使用しないでください。 このライブラリではスレッドの同期にもスタティックを使用するため、順序の初期化に関する問題が発生する可能性があります。 それらのスタティックを、非静的メンバー変数に変換するか、関数内にラップします (そうすることで最初のアクセス時に構築されます)。

Visual Studio 環境内で実行されるマネージド コードから DPI ヘルパー関数にアクセスするには、次のようにします。

- 使用する側のプロジェクトでは、最新バージョンの Shell MPF を参照する必要があります。 次に例を示します。

    ```csharp
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />
    ```

- プロジェクトで、**System.Windows.Forms**、**PresentationCore**、**PresentationUI** が参照されていることを確認します。

- コードでは、**Microsoft.VisualStudio.PlatformUI** 名前空間を使用して DpiHelper クラスの静的関数を呼び出します。 サポートされている型 (ポイント、サイズ、四角形など) については、拡大された新しいオブジェクトを返す拡張関数が用意されています。 次に例を示します。

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();
    DpiHelper.LogicalToDeviceUnits(ref bitmap);

    ```

## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>ズーム可能な UI での WPF 画像のぼやけの処理
WPF では、現在の DPI ズーム レベルでのビットマップのサイズが、高品質のバイキュービック アルゴリズムを使用して WPF によって自動的に変更されます (既定値)。これは、画像や大きなスクリーンショットに対しては適切に機能しますが、目に見えるぼやけが発生するためメニュー項目アイコンには適していません。

推奨事項:

- ロゴ画像とバナー アートワークの場合、既定の <xref:System.Windows.Media.BitmapScalingMode> サイズ変更モードを使用できます。

- メニュー項目やアイコンの場合、結果としてその他のひずみが発生しないときには、ぼやけを解消するために (200% と 300% では) <xref:System.Windows.Media.BitmapScalingMode> を使用する必要があります。

- 100% の倍数ではない大きなズーム レベル (250% や 350% など) の場合は、アイコン イメージをバイキュービックで拡大すると、ぼやけて不鮮明な UI になります。 最初に NearestNeighbor を使用して画像を 100% の最大倍数 (200% や 300% など) に拡大し、そこからバイキュービックを使用して拡大すると、より良い結果が得られます。 詳細については、「特殊な場合: 高レベル DPI のための WPF 画像の事前拡大」を参照してください。

  Microsoft.VisualStudio.PlatformUI 名前空間の DpiHelper クラスには、バインドに使用できるメンバー <xref:System.Windows.Media.BitmapScalingMode> が用意されています。 これを使用すると、Visual Studio シェルで、DPI スケール ファクターに応じて製品全体のビットマップ拡大モードを均一に制御できるようになります。

  これを XAML で使用するには、次を追加します。

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"

<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />

```

Visual Studio シェルでは、トップレベルのウィンドウとダイアログに対して、このプロパティが既に設定されています。 Visual Studio で実行されている WPF ベースの UI は、それを既に継承しています。 この設定が UI の特定の部分に反映されない場合は、XAML/WPF UI のルート要素に対して、これを設定することができます。 これが発生する場所には、ポップアップ、Win32 の親がある要素、プロセスが不足している Blend などのデザイナー ウィンドウが含まれます。

Visual Studio のテキスト エディターや WPF ベースのデザイナー (WPF デスクトップや Windows ストア) などの一部の UI は、システムで設定された DPI ズーム レベルから独立して拡大できます。 これらの場合は、DpiHelper.BitmapScalingMode を使用しないでください。 エディターでのこの問題を修正するため、IDE チームは RenderOptions.BitmapScalingMode という名前のカスタム プロパティを作成しました。 システムと UI を合わせたズーム レベルに応じて、そのプロパティ値を HighQuality または NearestNeighbor に設定します。

## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特殊な場合: 高レベル DPI のための WPF 画像の事前拡大
100% の倍数ではない非常に大きなズーム レベル (250% や 350% など) の場合は、アイコン イメージをバイキュービックで拡大すると、ぼやけて不鮮明な UI になります。 鮮明なテキストに並んだこれらの画像は、ほとんど錯覚のように見える外観です。 画像は、目により近い場所に、テキストとは焦点が異なるように表示されます。 この高倍率のサイズでの拡大結果は、最初に NearestNeighbor を使用して画像を 100% の最大倍数 (200% や 300% など) に拡大し、残りの倍率 (さらに 50%) までバイキュービックを使用して拡大することで改善できます。

次に、結果の違いの例を示します。最初の画像は、改善された 100%->200%->250% という 2 段階拡大のアルゴリズムで、2 番目の画像は 100%->250% のバイキュービックのみで拡大したものです。

![DPI に関する問題 (2 段階拡大の例)](../extensibility/media/dpi-issues-double-scaling-example.png "DPI に関する問題 (2 段階拡大の例)")

UI でこの 2 段階拡大を使用できるようにするには、各画像要素を表示するための XAML マークアップを変更する必要があります。 以下の例では、Visual Studio で DpiHelper ライブラリと Shell.12/14 を使用して、WPF での 2 段階拡大を使用する方法を示しています。

ステップ 1: NearestNeighbor を使用して、画像を 200%、300% のように事前拡大します。

バインドに適用されるコンバーター、または XAML マークアップ拡張機能のいずれかを使用して、画像を事前拡大します。 次に例を示します。

```xaml
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />

<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />

<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />

```

画像にもテーマを適用する必要がある場合 (すべてではなくてもほとんどの場合)、マークアップでは、最初に画像のテーマ設定を行ってから事前拡大を行う別のコンバーターを使用できます。 マークアップでは、必要な変換出力に応じて、<xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter> または <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter> のいずれかを使用できます。

```xaml
<vsui:DpiPrescaleThemedImageSourceConverter x:Key="DpiPrescaleThemedImageSourceConverter" />

<Image Width="16" Height="16">
  <Image.Source>
    <MultiBinding Converter="{StaticResource DpiPrescaleThemedImageSourceConverter}">
      <Binding Path="Icon" />
      <Binding Path="(vsui:ImageThemingUtilities.ImageBackgroundColor)"
               RelativeSource="{RelativeSource Self}" />
      <Binding Source="{x:Static vsui:Boxes.BooleanTrue}" />
    </MultiBinding>
  </Image.Source>
</Image>
```

ステップ 2: 最終的なサイズが現在の DPI に対して正しいようにします。

WPF では、UIElement に設定された BitmapScalingMode プロパティを使用して、現在の DPI に対して UI が拡大されるため、ソースとして事前拡大された画像を使用する Image コントロールは、あるべきサイズよりも 2 倍または 3 倍大きく表示されます。 以下に、この影響に対処するための方法をいくつか示します。

- 元の画像の 100% でのディメンションがわかっている場合は、Image コントロールの正確なサイズを指定できます。 拡大が適用される前に UI のサイズが、これらのサイズに反映されます。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />
    ```

- 元の画像のサイズが不明な場合は、LayoutTransform を使用して最終的な Image オブジェクトを縮小できます。 次に例を示します。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >
        <Image.LayoutTransform>
            <ScaleTransform
                ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"
                ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />
        </Image.LayoutTransform>
    </Image>
    ```

## <a name="enabling-hdpi-support-to-the-weboc"></a>WebOC に対する HDPI サポートの有効化
既定では、WebOC コントロール (WPF の WebBrowser コントロールや IWebBrowser2 インターフェイスなど) では、HDPI の検出とサポートが有効になりません。 結果として、高解像度ディスプレイでは小さすぎる表示コンテンツが含まれる埋め込みコントロールになります。 以下では、WebOC の特定の Web インスタンスで高 DPI のサポートを有効にする方法について説明します。

IDocHostUIHandler インターフェイスを実装します ([IDocHostUIHandler](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85)) に関する MSDN の記事を参照)。

```idl
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("BD3F23C0-D43E-11CF-893B-00AA00BDCE1A")]
public interface IDocHostUIHandler
{
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowContextMenu(
        [In, MarshalAs(UnmanagedType.U4)] int dwID,
        [In] POINT pt,
        [In, MarshalAs(UnmanagedType.Interface)] object pcmdtReserved,
        [In, MarshalAs(UnmanagedType.IDispatch)] object pdispReserved);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetHostInfo([In, Out] DOCHOSTUIINFO info);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowUI(
        [In, MarshalAs(UnmanagedType.I4)] int dwID,
        [In, MarshalAs(UnmanagedType.Interface)] object activeObject,
        [In, MarshalAs(UnmanagedType.Interface)] object commandTarget,
        [In, MarshalAs(UnmanagedType.Interface)] object frame,
        [In, MarshalAs(UnmanagedType.Interface)] object doc);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int HideUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int UpdateUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int EnableModeless([In, MarshalAs(UnmanagedType.Bool)] bool fEnable);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnDocWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnFrameWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ResizeBorder(
        [In] COMRECT rect,
        [In, MarshalAs(UnmanagedType.Interface)] object doc,
        bool fFrameWindow);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateAccelerator(
        [In] ref MSG msg,
        [In] ref Guid group,
        [In, MarshalAs(UnmanagedType.I4)] int nCmdID);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetOptionKeyPath(
        [Out, MarshalAs(UnmanagedType.LPArray)] string[] pbstrKey,
        [In, MarshalAs(UnmanagedType.U4)] int dw);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetDropTarget(
        [In, MarshalAs(UnmanagedType.Interface)] IOleDropTarget pDropTarget,
        [MarshalAs(UnmanagedType.Interface)] out IOleDropTarget ppDropTarget);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetExternal([MarshalAs(UnmanagedType.IDispatch)] out object ppDispatch);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateUrl(
        [In, MarshalAs(UnmanagedType.U4)] int dwTranslate,
        [In, MarshalAs(UnmanagedType.LPWStr)] string strURLIn,
        [MarshalAs(UnmanagedType.LPWStr)] out string pstrURLOut);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int FilterDataObject(
        IDataObject pDO,
        out IDataObject ppDORet);
    }
```

必要に応じて、ICustomDoc インターフェイスを実装します ([ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85)) に関する MSDN の記事を参照)。

```idl
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler(IDocHostUIHandler pUIHandler);
}
```

IDocHostUIHandler を実装するクラスを、WebOC のドキュメントに関連付けます。 上の ICustomDoc インターフェイスを実装した場合は、WebOC の document プロパティが有効になったらすぐにそれを ICustomDoc にキャストし、SetUIHandler メソッドを呼び出して、IDocHostUIHandler を実装しているクラスを渡します。

```csharp
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;
customDoc.SetUIHandler(this);

```

ICustomDoc インターフェイスを実装していない場合は、WebOC の document プロパティが有効になったらすぐにそれを IOleObject にキャストし、`SetClientSite` メソッドを呼び出して、IDocHostUIHandler を実装しているクラスを渡す必要があります。 `GetHostInfo` メソッドの呼び出しに渡される DOCHOSTUIINFO に、DOCHOSTUIFLAG_DPI_AWARE フラグを設定し ます。

```csharp
public int GetHostInfo(DOCHOSTUIINFO info)
{
    // This is what the default site provides.
    info.dwFlags = (DOCHOSTUIFLAG)0x5a74012;
    // Add the DPI flag to the defaults
    info.dwFlags |=.DOCHOSTUIFLAG.DOCHOSTUIFLAG_DPI_AWARE;
    return S_OK;
}
```

WebOC コントロールで HPDI をサポートするために必要な作業はこれですべてのはずです。

## <a name="tips"></a>ヒント

1. WebOC コントロールの document プロパティが変更された場合は、ドキュメントをもう一度 IDocHostUIHandler クラスに関連付ける必要がある場合があります。

2. 上記の対応で解決しない場合、WebOC で、DPI フラグに対する変更が認識されないという既知の問題があります。 これを解決する最も確実な方法は、WebOC の表示倍率を切り替えることです。これは、ズーム倍率に 2 つの異なる値を使用して 2 回の呼び出しを行うことを意味します。 また、この回避策が必要な場合は、それをすべての navigate 呼び出しに対して実行する必要があります。

    ```csharp
    // browser2 is a SHDocVw.IWebBrowser2 in this case
    // EX: Call the Exec twice with DPI%-1 and then DPI% as the zoomPercent values
    IOleCommandTarget cmdTarget = browser2.Document as IOleCommandTarget;
    if (cmdTarget != null)
    {
        object commandInput = zoomPercent;
        cmdTarget.Exec(IntPtr.Zero,
                       OLECMDID_OPTICAL_ZOOM,
                       OLECMDEXECOPT_DONTPROMPTUSER,
                       ref commandInput,
                       ref commandOutput);
    }
    ```
