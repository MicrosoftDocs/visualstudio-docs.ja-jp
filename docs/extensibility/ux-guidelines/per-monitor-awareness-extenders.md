---
title: Visual Studio のエクステンダーのモニターごとの対応のサポート
titleSuffix: ''
description: Visual Studio 2019 で使用できる新しいエクステンダーによるモニターごとの対応のサポートについて説明します。
ms.date: 04/10/2019
helpviewer_keywords:
- Visual Studio, PMA, per-monitor-awareness, extenders, Windows Forms
- Per-Monitor Awareness support for extenders
author: rub8n
ms.author: rurios
manager: anthc
monikerRange: vs-2019
ms.topic: reference
dev_langs:
- CSharp
- CPP
ms.openlocfilehash: 90ec038e8f27407ba08633bacbb5576bee2a7883
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902047"
---
# <a name="per-monitor-awareness-support-for-visual-studio-extenders"></a>Visual Studio のエクステンダーのモニターごとの対応のサポート

Visual Studio 2019 より前のバージョンでは、DPI 対応コンテキストがモニターごとの DPI 対応 (PMA) ではなく、システム対応に設定されていました。 システム対応で実行すると、Visual Studio がさまざまなスケール ファクターを使用するモニター間でレンダリングする必要がある場合や、ディスプレイ構成が異なる (例: Windows の拡大縮小の設定が異なる) コンピューターでリモート処理を行う必要がある場合に、視覚的効果が低下していました (例: フォントやアイコンの表示がぼやける)。

Visual Studio 2019 の DPI 対応コンテキストは PMA として設定されます (環境でサポートされている場合)。これにより、Visual Studio では、1 つのシステムで定義された構成ではなく、ホストされているディスプレイの構成に従ってレンダリングできます。 最終的には、PMA モードをサポートする領域用に常に鮮明な UI に変換されます。

このドキュメントで取り上げられている用語と全体的なシナリオの詳細については、「[Windows での高 DPI デスクトップアプリケーション開発](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)」を参照してください。

## <a name="quickstart"></a>クイック スタート

- Visual Studio が PMA モードで実行されていることを確認します (「**PMA を有効にする**」を参照)。

- 一連の一般的なシナリオで拡張機能を正しく使用できることを検証します (「**拡張機能の PMA の問題をテストする**」を参照)。

- 問題が見つかった場合は、このドキュメントで説明されている戦略と推奨事項を使用して、問題を診断および修正できます。 また、必要な API にアクセスするには、新しい [Microsoft.VisualStudio.DpiAwareness](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) NuGet パッケージをプロジェクトに追加する必要があります。

## <a name="enable-pma"></a>PMA を有効にする

Visual Studio で PMA を有効にするには、次の要件を満たす必要があります。

- Windows 10 April 2018 Update (v1803、RS4) 以降
- .NET Framework 4.8 RTM 以上
- [ピクセルの密度が異なる画面のレンダリングを最適化する](../../ide/reference/general-environment-options-dialog-box.md)オプションが有効になっている Visual Studio 2019

これらの要件が満たされていると、Visual Studio ではプロセス全体で PMA モードが自動的に有効になります。

> [!NOTE]
> Visual Studio の Windows フォーム コンテンツ (プロパティ ブラウザーなど) では、Visual Studio 2019 バージョン16.1 以降がインストールされている場合にのみ PMA がサポートされます。

## <a name="test-your-extensions-for-pma-issues"></a>拡張機能の PMA の問題をテストする

Visual Studio では、WPF、Windows フォーム、Win32、および HTML と JS の UI フレームワークが正式にサポートされています。 Visual Studio を PMA モードにすると、それぞれの UI スタックの動作が異なります。 そのため、UI フレームワークに関係なく、テスト パスを実行してすべての UI が PMA モードに対応していることを確認することをお勧めします。

次の一般的なシナリオについて検証することをお勧めします。

- アプリケーションの実行中に 1 つのモニター環境のスケール ファクターを変更する。

  このシナリオでは、UI が Windows DPI の動的な変更に対応していることをテストできます。

- 接続されたモニターがプライマリに設定されていて、アプリケーションの実行時にノート PC とは異なるスケール ファクターがそのモニターに設定されているノート PC をドッキング/ドッキング解除する。

  このシナリオでは、UI がディスプレイ DPI の変更に応答していること、および動的に追加または削除されたディスプレイを処理することをテストできます。

- スケール ファクターが異なる複数のモニターを用意して、それらの間でアプリケーションを移動する。

  このシナリオでは、UI がディスプレイ DPI の変更に対応していることをテストできます。
    
- プライマリ モニターに対するローカル コンピューターとリモート コンピューターのスケール ファクターが異なる場合にコンピューターでリモート処理を行う。

  このシナリオでは、UI が Windows DPI の動的な変更に対応していることをテストできます。

UI に問題があるかどうかを確認する予備テストでは、*Microsoft.VisualStudio.Utilities.Dpi.DpiHelper*、*Microsoft.VisualStudio.PlatformUI.DpiHelper*、または *VsUI::CDpiHelper* の各クラスがコードで使用されているかどうかを確認することをお勧めします。 これらの古い DpiHelper クラスではシステム DPI 対応のみがサポートされ、プロセスが PMA の場合に必ずしも正しく機能するとは限りません。

これらの DpiHelper の一般的な使用法は次のようになります。

```cs
Point screenTopRight = logicalBounds.TopRight.LogicalToDeviceUnits();

POINT screenIntTopRight = new POINT
{
    x = (int)screenTopRIght.X,
    y = (int)screenTopRIght.Y
}

// Declared via P/Invoke
IntPtr monitor = MonitorFromPoint(screenIntTopRight, MONITOR_DEFAULTTONEARST);
```

上の例では、ウィンドウの論理境界を表す四角形がデバイス ユニットに変換され、正確なモニター ポインターを返すためにデバイス座標を要求するネイティブ メソッド MonitorFromPoint に渡すことができます。

### <a name="classes-of-issues"></a>問題のクラス
Visual Studio で PMA モードが有効になっている場合、UI ではいくつかの一般的な方法で問題を再現できます。 これらの問題のほとんどは、Visual Studio でサポートされるいずれかの UI フレームワークで発生する可能性があります。 また、これらの問題は、UI の一部が混合モードの DPI スケールのシナリオでホストされている場合にも発生することがあります (詳細については、Windows の[ドキュメント](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows)を参照)。 

#### <a name="win32-window-creation"></a>Win32 ウィンドウの作成
CreateWindow() または CreateWindowEx() を使用してウィンドウを作成する場合、一般的なパターンとしては、座標 (0,0) (プライマリ ディスプレイの左上隅) にウィンドウを作成してから、最終的な位置に移動します。 ただしその場合、ウィンドウが DPI 変更メッセージまたはイベントをトリガーする可能性があります。これにより、他の UI メッセージやイベントが再トリガーされ、最終的には望ましくない動作やレンダリングを引き起こす可能性があります。

#### <a name="wpf-element-placement"></a>WPF 要素の配置
以前の Microsoft.VisualStudio.Utilities.Dpi.DpiHelper を使用して WPF 要素を移動する場合、要素がプライマリ以外の DPI にあるときは、左上の座標が正しく計算されないことがあります。

#### <a name="serialization-of-ui-element-sizes-or-positions"></a>UI 要素のサイズまたは位置のシリアル化
UI のサイズまたは位置 (デバイス ユニットとして保存されている場合) が格納先とは異なる DPI コンテキストで復元されると、UI の配置とサイズが正しく設定されません。 これは、デバイス ユニットに固有の DPI 関係があるために発生します。

#### <a name="incorrect-scaling"></a>不適切な拡大縮小
プライマリ DPI で作成された UI 要素は正しく拡大縮小されますが、別の DPI を使用するディスプレイに移動された場合は、UI 要素の拡大縮小が再度行われず、大きすぎるコンテンツや小さすぎるコンテンツが生じます。

#### <a name="incorrect-bounding"></a>不適切な境界
拡大縮小の問題と同様に、UI 要素はプライマリ DPI コンテキストで境界を正しく計算しますが、プライマリ以外の DPI に移動された場合、新しい境界は正しく計算されません。 そのため、ホストしている UI と比較してコンテンツ ウィンドウが小さすぎたり大きすぎたりする状態になるため、空白またはクリッピングが発生します。

#### <a name="drag--drop"></a>ドラッグ アンド ドロップ
混合モードの DPI シナリオ (レンダリングする UI 要素ごとに DPI 対応モードが異なる場合など) では、ドラッグ アンド ドロップ座標が正しく計算されない可能性があるため、最終的なドロップ位置が不正確になります。

#### <a name="out-of-process-ui"></a>アウトプロセス UI
一部の UI はアウトプロセスで作成されます。作成元の外部プロセスが Visual Studio とは異なる DPI 対応モードになっている場合は、前述のレンダリングの問題が発生する可能性があります。

#### <a name="windows-forms-controls-images-or-layouts-rendered-incorrectly"></a>Windows フォームのコントロール、画像、またはレイアウトが正しくレンダリングされない
すべての Windows フォーム コンテンツで PMA モードがサポートされているわけではありません。 そのため、レイアウトや拡大縮小の設定が正しくないことによるレンダリングの問題が発生する可能性があります。 この場合に考えられる解決策としては、Windows フォーム コンテンツを "システム対応" の DpiAwarenessContext に明示的にレンダリングします (「[コントロールを特定の DpiAwarenessContext に強制的に配置する](#force-a-control-into-a-specific-dpiawarenesscontext)」を参照)。

#### <a name="windows-forms-controls-or-windows-not-displaying"></a>Windows フォームのコントロールまたはウィンドウが表示されない
この問題の主な原因の 1 つは、開発者が DpiAwarenessContext を使用するコントロールまたはウィンドウの親を、別の DpiAwarenessContext を使用するウィンドウに再指定しようとするためです。

次の図は、ウィンドウの親指定における現在の **既定** の Windows オペレーティング システムの制限事項を示しています。

![正しい親指定の動作のスクリーンショット](media/PMA-parenting-behavior.PNG)

> [!Note]
> この動作を変更するには、スレッド ホスティング動作を設定します (「[Dpi_Hosting_Behavior 列挙型](/windows/desktop/api/windef/ne-windef-dpi_hosting_behavior)」を参照)。

結果として、サポートされていないモード間の親子関係の設定は失敗し、コントロールまたはウィンドウが想定どおりにレンダリングされない可能性があります。

### <a name="diagnose-issues"></a>問題の診断

PMA 関連の問題を特定する場合は、以下に示す多くの要素を考慮する必要があります。 

- UI または API は論理値とデバイス値のどちらを想定していますか。
    - 通常、WPF の UI と API では論理値を使用します (常に使用するわけではありません)。
    - 通常、Win32 の UI と API ではデバイス値を使用します。

- 値はどこから取得しますか。
    - 他の UI または API から値を受け取る場合は、デバイス値と論理値のどちらを渡しますか。
    - 複数のソースから値を受け取る場合は、同じ型の値を使用または想定しますか。また、変換を組み合わせて使用する必要はありますか。

- UI 定数は使用されていますか。また、それはどのような形式ですか。

- 受け取る値に適した DPI コンテキストにスレッドがありますか。

  通常、ミックス DPI ホスティングを有効にするための変更では、適切なコンテキストにコード パスを配置する必要がありますが、メイン メッセージ ループやイベント フローの外部で行われる作業は、間違った DPI コンテキストで実行される可能性があります。

- 値は DPI コンテキストの境界を越えますか。

  ドラッグ アンド ドロップは、座標が DPI コンテキストを越える可能性のある一般的な状況です。 ウィンドウは正しい処理を実行しようとしますが、ホスト UI ではコンテキスト境界を一致させるための変換作業が必要になる場合があります。

### <a name="pma-nuget-package"></a>PMA NuGet パッケージ
新しい DpiAwarness ライブラリは、[Microsoft.VisualStudio.DpiAwareness](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) NuGet パッケージにあります。

### <a name="recommended-tools"></a>推奨されるツール
以下のツールを使用すると、Visual Studio でサポートされているさまざまな UI スタックで PMA 関連の問題をデバッグできます。

#### <a name="snoop"></a>Snoop
Snoop は、組み込みの Visual Studio XAML ツールにない機能が追加された XAML デバッグ ツールです。 また、Snoop では、WPF UI を表示および調整できるようにするための Visual Studio のアクティブなデバッグが必要がありません。 Snoop による PMA の問題の診断に役立つ 2 つの主な方法は、論理配置座標またはサイズの境界の検証、および UI の DPI が適切であるかの検証を目的としています。
 
#### <a name="visual-studio-xaml-tools"></a>Visual Studio XAML ツール
Visual Studio の XAML ツールは、Snoop と同様に PMA の問題の診断に役立ちます。 原因が見つかった場合は、ブレークポイントを設定し、[ライブ ビジュアル ツリー] ウィンドウとデバッグ ウィンドウを使用して、UI の境界と現在の DPI を調べることができます。

## <a name="strategies-for-fixing-pma-issues"></a>PMA の問題を修正するための戦略

### <a name="replace-dpihelper-calls"></a>DpiHelper の呼び出しを置き換える

ほとんどの場合、PMA モードにおける UI の問題の修正では、結局のところマネージド コード内の古い *Microsoft.VisualStudio.Utilities.Dpi.DpiHelper* クラスと *Microsoft.VisualStudio.PlatformUI.DpiHelper* クラスの呼び出しを新しい *Microsoft.VisualStudio.Utilities.DpiAwareness* ヘルパー クラスの呼び出しに置き換えることになります。 

```cs
// Remove this kind of use:
Point deviceTopLeft = new Point(window.Left, window.Top).LogicalToDeviceUnits();

// Replace with this use:
Point deviceTopLeft = window.LogicalToDevicePoint(new Point(window.Left, window.Top));
```

ネイティブ コードの場合は、古い *VsUI::CDpiHelper* クラスの呼び出しを新しい *VsUI::CDpiAwareness* クラスの呼び出しに置き換える必要があります。 

```cpp
// Remove this kind of use:
int cx = VsUI::DpiHelper::LogicalToDeviceUnitsX(m_cxS);
int cy = VsUI::DpiHelper::LogicalToDeviceUnitsY(m_cyS);

// Replace with this use:
int cx = m_cxS;
int cy = m_cyS;
VsUI::CDpiAwareness::LogicalToDeviceUnitsX(m_hwnd, &cx);
VsUI::CDpiAwareness::LogicalToDeviceUnitsY(m_hwnd, &cy);
```

新しい DpiAwareness クラスと CDpiAwareness 度クラスは DpiHelper クラスと同じユニット変換ヘルパーを提供しますが、追加の入力パラメーター (変換操作の参照として使用する UI 要素) が必要になります。 画像の拡大縮小ヘルパーは新しい DpiAwareness ヘルパーまたは CDpiAwareness ヘルパーに存在しないことに注意してください。また、必要に応じて、[ImageService](../image-service-and-catalog.md) を代わりに使用する必要があります。

マネージド クラス DpiAwareness は、WPF ビジュアル、Windows フォーム コントロール、Win32 の HWND と HMONITOR (どちらも IntPtr の形式) 用のヘルパーを提供します。一方、ネイティブ クラス CDpiAwareness は HWND ヘルパーと HMONITOR ヘルパーを提供します。

### <a name="windows-forms-dialogs-windows-or-controls-displayed-in-the-wrong-dpiawarenesscontext"></a>Windows フォームのダイアログ、ウィンドウ、またはコントロールが間違った DpiAwarenessContext に表示される
DpiAwarenessContext が異なる (Windows の既定の動作のため) ウィンドウの親を正常に指定した後でも、DpiAwarenessContext が異なるウィンドウでは拡大縮小の処理方法が異なるため、拡大縮小の問題が発生することがあります。 そのため、テキストや画像の配置の問題またはテキストや画像の表示がぼやける問題が UI で発生する可能性があります。

解決策としては、アプリケーション内のすべてのウィンドウとコントロールに DpiAwarenessContext の正しいスコープを設定します。

### <a name="top-level-mixed-mode-tlmm-dialogs"></a>トップ レベルの混合モード (TLMM) ダイアログ
モーダル ダイアログなどのトップ レベルのウィンドウの作成時には、ウィンドウ (およびそのハンドル) が作成される前に、スレッドが正しい状態であることを確認することが重要です。 CDpiScope ヘルパー (ネイティブ コードの場合) または DpiAwareness.EnterDpiScope ヘルパー (マネージド コードの場合) を使用して、スレッドをシステム対応にすることができます (通常、TLMM は WPF 以外のダイアログまたはウィンドウで使用する必要があります)。

### <a name="child-level-mixed-mode-clmm"></a>子レベルの混合モード (CLMM)
既定では、子ウィンドウは、親を指定せずに作成された場合は現在のスレッドの DPI 対応コンテキストを受け取り、親を指定して作成された場合は親の DPI 対応コンテキストを受け取ります。 DPI 対応コンテキストが親と異なる子を作成するために、スレッドを目的の DPI 対応コンテキストに配置できます。 これで、親を指定せずに子を作成し、手動で親ウィンドウに親を再指定できます。

#### <a name="clmm-issues"></a>CLMM の問題
メイン メッセージ ループやイベント チェーンの一部として発生する UI 計算作業のほとんどは、適切な DPI 対応コンテキストで既に実行されている必要があります。 ただし、このようなメイン ワークフローの外部 (アイドル時間のタスク、UI スレッドが関連付けられていない場合など) で座標やサイズ設定の計算が行われると、現在の DPI 対応コンテキストが UI の配置やサイズ設定の間違いを引き起こす可能性があります。 通常、スレッドを UI 作業に適した状態にすることで問題が修正されます。
 
#### <a name="opt-out-of-clmm"></a>CLMM のオプトアウト
PMA を完全にサポートするために WPF 以外のツール ウィンドウを移行する場合は、CLMM をオプトアウトする必要があります。 そのためには、新しいインターフェイス (IVsDpiAware) を実装する必要があります。

```cs
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IVsDpiAware
{
    [ComAliasName("Microsoft.VisualStudio.Shell.Interop.VSDPIMode")]
    uint Mode {get;}
}
```

```cpp
IVsDpiAware : public IUnknown
{
    public:
        HRRESULT STDMETHODCALLTYPE get_Mode(__RCP__out VSDPIMODE *dwMode);
};
```

マネージド言語の場合、*Microsoft.VisualStudio.Shell.ToolWindowPane* から派生するのと同じクラスにこのインターフェイスを実装することをお勧めします。 C++ の場合、vsshell.h から *IVsWindowPane* を実装するのと同じクラスにこのインターフェイスを実装することをお勧めします。

このインターフェイスで Mode プロパティによって返される値は __VSDPIMODE です (マネージド コードで uint にキャストされます)。

```cs
enum __VSDPIMODE
{
    VSDM_Unaware    = 0x01,
    VSDM_System     = 0x02,
    VSDM_PerMonitor = 0x03,
}
```

- Unaware は、ツール ウィンドウで 96 DPI を処理する必要があることを意味します。他のすべての DPI の拡大縮小は Windows で処理されます。 結果として、コンテンツの表示が少しぼやけます。
- System は、ツール ウィンドウでプライマリ ディスプレイ DPI の DPI を処理する必要があることを意味します。 DPI が一致するディスプレイの表示は鮮明ですが、DPI が異なる場合や、セッション中に変更された場合は、拡大縮小が Windows で処理され、表示が少しぼやけます。
- PerMonitor は、すべてのディスプレイで DPI が変更されるたびに、すべての DPI をツール ウィンドウで処理する必要があることを意味します。

> [!NOTE]
> Visual Studio でサポートされているのは PerMonitorV2 対応のみであるため、PerMonitor 列挙値は DPI_AWARENESS_CONTEXT_PER_MONITOR_AWARE_V2 の Windows 値に変換されます。

#### <a name="force-a-control-into-a-specific-dpiawarenesscontext"></a>コントロールを特定の DpiAwarenessContext に強制的に配置する

PMA モードをサポートするために更新されないレガシ UI であっても、Visual Studio が PMA モードで実行されている間は軽微な調整が必要になる場合があります。 このような修正の 1 つとして、正しい DpiAwarenessContext で UI が作成されていることを確認する必要があります。 UI を特定の DpiAwarenessContext に強制的に配置するには、次のコードを使用して DPI スコープに入ります。

```cs
using (DpiAwareness.EnterDpiScope(DpiAwarenessContext.SystemAware))
{
    Form form = new MyForm();
    form.ShowDialog();
}
```

```cpp
void MyClass::ShowDialog()
{
    VsUI::CDpiScope dpiScope(DPI_AWARENESS_CONTEXT_SYSTEM_AWARE);
    HWND hwnd = ::CreateWindow(...);
}
```

> [!NOTE]
> DpiAwarenessContext の強制は、WPF 以外の UI とトップ レベルの WPF ダイアログでのみ機能します。 ツール ウィンドウまたはデザイナー内でホストされる WPF UI を作成する場合は、コンテンツが WPF UI ツリーに挿入されるとすぐに、現在のプロセスである DpiAwarenessContext に変換されます。

## <a name="known-issues"></a>既知の問題

### <a name="windows-forms"></a>Windows フォーム

新しい混合モードのシナリオに合わせた最適化のため、Windows フォームでは、親が明示的に設定されていない場合のコントロールとウィンドウの作成方法が変更されました。 以前は、明示的に親が設定されていないコントロールでは、作成対象のコントロールまたはウィンドウに対する一時的な親として内部の "パーキング ウィンドウ" を使用していました。 

.NET 4.8 より前のバージョンでは、ウィンドウの作成時に現在のスレッドの DPI 対応コンテキストから DpiAwarenessContext を取得する "パーキング ウィンドウ" が 1 つ用意されていました。 親が未設定のコントロールは、そのコントロールのハンドルの作成時にパーキング ウィンドウと同じ DpiAwarenessContext を継承し、最終的な親または想定される親がアプリケーション開発者によって再指定されます。 これにより、"パーキング ウィンドウ" の DpiAwarenessContext が最終的な親ウィンドウよりも高い場合に、タイミングに基づくエラーが発生します。

.NET 4.8 以降では、検出される DpiAwarenessContext ごとに 1 つの "パーキング ウィンドウ" があります。 もう 1 つの大きな違いは、コントロールに使用される DpiAwarenessContext がハンドルの作成時ではなく、コントロールの作成時にキャッシュされる点です。 つまり、全体的な終了動作は同じですが、タイミングに基づく問題であったものが一貫した問題に変わる可能性があります。 また、UI コードを記述して正しくスコープを設定するための確定的な動作がアプリケーション開発者に提供されます。
