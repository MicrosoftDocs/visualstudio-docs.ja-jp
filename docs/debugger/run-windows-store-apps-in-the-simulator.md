---
title: シミュレーターで UWP アプリの実行 |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 81b69bf8-ec87-4bb6-9ad4-1fa7b7802d16
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: fd0aa403e702a591a0b09d0891116063a3ed9ff2
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2018
ms.locfileid: "44281053"
---
# <a name="run-uwp-apps-in-the-simulator"></a>シミュレーターで UWP アプリを実行する
UWP アプリ用の Visual Studio シミュレーターは、UWP アプリをシミュレートするデスクトップ アプリケーションです。 通常は、接続されたデバイス、またはリモート コンピューターのローカル コンピューター上でデバッグします。 ただし、一部のシナリオでの Visual Studio シミュレーターを使用して、別の物理的な画面サイズと解像度をエミュレートすることがあります。 また、一般的なタッチと回転イベントのシミュレートし、ネットワーク接続のプロパティをシミュレートできます。
  
 シミュレーターをすることができますを設計、開発、デバッグ、および UWP アプリをテスト環境を提供します。 ただし、Microsoft Store にアプリを発行する前に、実際のデバイスでアプリをテストする必要があります。  
  
 UWP アプリ用の Visual Studio シミュレーターはローカル コンピューターに分離された環境で実行されません。 したがって、シミュレーターで発生したエラー (回復できないシステム エラーなど) がコンピューター全体に影響を与える場合があります。  
  
> [!IMPORTANT]
>  Visual Studio 2015 シミュレーターには、位置情報ボタンがありません。 これは、Windows 10 シミュレーターに位置情報シミュレーションが含まれていないためです。
  
##  <a name="BKMK_Set_the_simulator_as_the_target"></a> シミュレーターをターゲットとして設定する  
 シミュレーターで UWP アプリを実行するには、選択**シミュレーター**横にドロップダウン リストからリスト、**デバッグの開始**ボタン、デバッガーを**標準**ツールバー。 このオプションは使用可能な場合、アプリの**ターゲット プラットフォームの最小値。バージョン**が開発用コンピューターにオペレーティング システム未満です。 
  
 ![シミュレーターで実行されている](../debugger/media/vsrun_f5_simulator.png "VSRUN_F5_Simulator")  
  
##  <a name="BKMK_Choose_an_interaction_mode"></a> 対話モードを選択する  
 次の対話モードを選択できます。  
  
-   ![マウス モード ボタン](../debugger/media/simulator_mousemodebtn.png "SIMULATOR_MouseModeBtn")マウス モード: 対話モードをマウス ジェスチャに設定します。 マウス ジェスチャには、クリック、ダブルクリック、およびドラッグがあります。  
  
-   ![タッチ エミュレーション [スタート] ボタン](../debugger/media/simulator_starttouchemulationbtn.png "SIMULATOR_StartTouchEmulationBtn")タッチ エミュレーションの開始: 対話モードを 1 本の指のタッチ ジェスチャに設定します。 1 本指のイベントには、タップ、ドラッグ、およびスワイプがあります。  
  
     ![シミュレーターの 1 本の指のターゲット](../debugger/media/simulator_onefinger.png "SIMULATOR_OneFinger")シングル ターゲット アイコンは、シミュレーター内のイベントの場所を示します。 ポインターを配置するには、マウスを使用します。  
  
     ![1 本指タッチのターゲット](../debugger/media/simulator_onefingerengaged.png "SIMULATOR_OneFingerEngaged")タッチ モードをアクティブにマウスの左ボタンを押します。 たとえば、タップをシミュレートする場合はボタンをクリックし、ドラッグまたはスワイプする場合はボタンを長押しします。  
  
## <a name="pinch-and-zoom"></a>ピンチとズーム  
 対話モードを、2 本の指によるピンチ ジェスチャとズーム ジェスチャに設定します。  
  
-   ![シミュレーターの 2 本指のターゲット](../debugger/media/simulator_twofinger.png "SIMULATOR_TwoFinger")  
  
     ダブル ターゲット アイコンは、デバイス画面上の 2 本の指の位置を示します。  
  
    -   デバイス画面上のオブジェクトの上にアイコンを配置するには、マウスを移動します。  
  
    -   ピンチまたはズームを実行する前の 2 本の指のシミュレートされる距離を変更するは、マウス ホイールを前方または後方に回転させます。  
  
-   -   ![ピンチ、ズーム、およびターゲットを回転](../debugger/media/simulator_twofingerengaged.png "SIMULATOR_TwoFingerEngaged")  
  
         縮小 (ピンチ) する場合は、左ボタンを押し、ホイールを後方 (手前) に回転させます。  
  
    -   拡大 (ズーム) する場合は、左ボタンを押し、マウス ホイールを前方 (奥) に回転させます。  
  
## <a name="object-rotation"></a>オブジェクトの回転  
 **[タッチ エミュレーションの回転]** ボタンは、対話モードを、2 本の指による回転ジェスチャに設定します。  
  
-   -   デバイス画面上のオブジェクトの上にアイコンを配置するには、マウスを移動します。  
  
    -   オブジェクトの回転を実行する前の 2 本の指のシミュレートされる方向を変更するは、マウス ホイールを前方または後方に回転させます。  
  
-   -   オブジェクトを反時計回りに回転させる場合は、左ボタンを押し、ホイールを後方 (手前) に回転させます。 マウス ホイールを回転させると、回転の相対サイズを示すために、2 つのターゲット アイコンのいずれかが他方のアイコンを中心として回転します。  
  
    -   オブジェクトを時計回りに回転させる場合は、左ボタンを押し、マウス ホイールを前方 (奥) に回転させます。  
  
##  <a name="BKMK_Enable_or_disable_Always_on_top_mode"></a> [常に手前に表示] モードを有効または無効にする  
 シミュレーター ウィンドウが常に他のウィンドウの上に表示されるように設定できます。 **[最前面に表示するウィンドウの切り替え]** ボタンは、シミュレーター ウィンドウの **[常に手前に表示]** モードを有効または無効にします。  
  
##  <a name="BKMK_Change_the_device_orientation"></a> デバイスの方向を変更する  
 シミュレーターを任意の方向に 90 度回転させることで、デバイスの方向を縦長と横長の間で切り替えることができます。  
  
> [!NOTE]
>  シミュレーターでは、プロジェクトのプロパティ [DisplayProperties.AutoRotationPreferences](http://go.microsoft.com/fwlink/?LinkId=249460) は考慮されません。 たとえば、プロジェクトで方向が `Landscape`に設定されている場合でも、シミュレーターの方向を回転させて縦向きにすると、シミュレーターに表示されるイメージも回転され、サイズが変更されます。 実際のデバイスでこれらの設定をテストしてください。  
  
> [!NOTE]
>  シミュレーターを回転させたときに、シミュレーターの 1 つの辺がシミュレーターを表示している画面よりも大きくなる場合、シミュレーターのサイズは画面に収まるように自動的に変更されます。 シミュレーターは、再度回転させた場合でも、元のサイズに戻ることはありません。  
  
##  <a name="BKMK_Change_the_simulated_screen_size_and_resolution"></a> シミュレートされる画面のサイズと解像度を変更する  
 シミュレートされる画面のサイズと解像度を変更するには、パレットの **[解像度の変更]** ボタンをクリックし、一覧から新しいサイズと解像度を選択します。  
  
 画面サイズと解像度は *画面の幅 (インチ)、ピクセル幅 X ピクセル高さ*で一覧表示されます。 画面のサイズと解像度の両方がシミュレートされます。 シミュレーター上の位置座標は、選択したデバイスのサイズと解像度の座標に変換されます。  
  
> [!NOTE]
>  ビットマップ イメージのスケーリングされたバージョンをアプリに保存できます。Windows は、現在のスケールで正しいイメージを読み込みます。 詳細については、次を参照してください。[デザインと UI の概要](/windows/uwp/layout/design-and-ui-intro)します。 ただし、Windows によって解像度に合ったイメージが選択されるようにシミュレーターの解像度を変更した場合、新しいイメージを表示するにはデバッグ セッションを停止して再度開始する必要があります。  
  
##  <a name="BKMK_Capture_a_screenshot_of_your_app_for_submission_to_the_Microsoft_Store"></a> Microsoft Store に送信するアプリのスクリーン ショットをキャプチャします。  
 Microsoft Store にアプリを送信するときに、アプリのスクリーン ショットを含める必要があります。  
  
> [!NOTE]
>  スクリーンショットは、シミュレーターの現在の解像度で保存されます。 解像度を変更するには、 **[解像度の変更]** ボタンをクリックします。  
  
-   シミュレーターからアプリのスクリーンショットを作成するには、 **[クリップボードにスクリーンショットをキャプチャします]** ボタンをクリックします。  
  
-   スクリーンショットの配置場所を設定するには、 **[スクリーンショットの設定]** ボタンをクリックし、ショートカット メニューから場所を選択します。  
  
     ![設定のコンテキスト メニューのスクリーン ショット](../debugger/media/simulator_screenshotsettingscntxmnu.png "SIMULATOR_ScreenShotSettingsCntxMnu")  
  
##  <a name="BKMK_Simulate_network_connection_properties"></a> ネットワーク接続のプロパティをシミュレートする  
 アプリのユーザーが従量制ネットワーク接続のコストを管理するには、ネットワーク接続コストやデータ プランの状態の変更の認識を維持し、この情報を使用して、ローミングや超過のための追加コストの発生を避けるためにアプリを有効にすることができます、指定したデータ転送の制限。 [Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity) Api に応答できます。 [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation)と[TriggerType](/uwp/api/windows.applicationmodel.background.systemtrigger)署名を行うイベント。 参照してください[クイック スタート: 従量制課金接続の管理のコスト制約](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)します。  
  
 シミュレーターをデバッグまたは、ネットワーク コストを認識するコードをテスト、を通じて公開されているネットワークのプロパティを模倣できます、 [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile)によって返されるオブジェクト[GetInternetConnectionProfile](/uwp/api/windows.networking.connectivity.networkinformation)します。
  
 ネットワークのプロパティをシミュレートするには、次のようにします。  
  
1.  シミュレーターのツール バーの **[ネットワーク プロパティの変更]** ボタンをクリックします。  
  
2.  **[ネットワーク プロパティの設定]** ダイアログ ボックスの **[シミュレートされたネットワーク プロパティの使用]** をクリックします。  
  
     チェック ボックスをオフにしてシミュレーションを削除し、現在接続されているインターフェイスのネットワーク プロパティに戻ります。  
  
3.  シミュレートされたネットワークの **[プロファイル名]** を入力します。 シミュレーションを識別するために使用できる一意の名前を使用することをお勧めします。、 [ProfileName](/uwp/api/windows.networking.connectivity.connectionprofile)のプロパティ、 [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile)オブジェクト。  
  
4.  選択、 [NetworkCostType](/uwp/api/windows.networking.connectivity.networkcosttype)からプロファイルの値、**ネットワーク コストの種類**一覧。  
  
5.  **データの限度の状態フラグ**] ボックスの一覧を設定できます、 [ApproachingDataLimit](/uwp/api/windows.networking.connectivity.connectioncost)プロパティまたは[OverDataLimit](/uwp/api/windows.networking.connectivity.connectioncost)プロパティを true を選択または**データの制限 [** 両方の値を false に設定します。  
  
6.  **ローミングの状態**一覧で、設定、[ローミング](/uwp/api/windows.networking.connectivity.connectioncost)プロパティ。  
  
7.  選択**プロパティの設定**、前景をトリガーすることによって、ネットワークのプロパティをシミュレートするために[NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation)イベントとバック グラウンド[SystemTrigger](/uwp/api/windows.applicationmodel.background.systemtrigger)型の**NetworkStateChange**します。  
  
 **ネットワーク接続の管理の詳細について**  
  
 [クイック スタート:、ネットワーク コストの制約が従量制課金を管理します。](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)  
  
 [ネットワーク情報のサンプル](https://code.msdn.microsoft.com/windowsapps/Network-Information-Sample-63aaa201)  
  
 [エネルギー使用の分析](../profiling/analyze-energy-use-in-store-apps.md)  
  
 [Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity)  
  
 [バック グラウンド タスクでシステム イベントに応答する方法](/previous-versions/windows/apps/hh977058(v=win.10))  
  
 [UWP アプリで中断イベント、再開イベント、およびバックグラウンド イベントをトリガーする方法](/visualstudio/debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio)  
  
##  <a name="BKMK_Navigate_the_simulator_with_the_keyboard"></a> キーボードを使用してシミュレーター内を移動する  
 キーを押して、シミュレーター ツールバーをナビゲートできます**CTRL + ALT + ↑**シミュレーター ウィンドウからシミュレーター ツールバーにフォーカスを移動します。 ツール バーのボタンの間を移動するには、 **上向きの矢印** と **下向きの矢印** を使用します。  
  
 シミュレーターを終了するには、キーを押して**CTRL + ALT + F4**します。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio からアプリを実行](../debugger/run-store-apps-from-visual-studio.md)