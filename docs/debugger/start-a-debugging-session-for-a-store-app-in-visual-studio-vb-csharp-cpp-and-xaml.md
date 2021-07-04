---
title: UWP アプリのデバッグ セッションを開始する | Microsoft Docs
description: ユニバーサル Windows プラットフォーム (UWP) アプリの Visual Studio デバッグ セッションを開始します。 デバッグ セッションを構成し、アプリを起動する方法を選択します。
ms.custom: SEO-VS-2020
ms.date: 11/20/2018
ms.topic: how-to
f1_keywords:
- VC.Project.IVCAppHostRemoteDebugPageObject.MachineName
- VC.Project.IVCAppHostRemoteDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostLocalDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostTetheredDebugPageObject.DebuggerType
- VC.Project.IVCAppHostLocalDebugPageObject.BreakpointBehavior
- VC.Project.IVCAppHostRemoteDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostRemoteDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.DebuggerType
- ImmersiveProjects.Properties.Debug
- VC.Project.IVCAppHostTetheredDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostSimulatorDebugPageObject.GPUDebuggerTargetType
- VC.Project.IVCAppHostLocalDebugPageObject.LaunchApplication
- VC.Project.IVCAppHostLocalDebugPageObject.AllowLocalNetworkLoopback
- AppPackage.Properties.Debug
- VC.Project.IVCAppHostRemoteDebugPageObject.Authentication
- VC.Project.IVCAppHostRemoteDebugPageObject.DebuggerType
- VC.Project.IVCAppHostSimulatorDebugPageObject.BreakpointBehavior
- vs.debug.installedapppackagelauncher
- vs.debug.error.wwahost_scriptdebuggingdisabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- uwp
ms.openlocfilehash: d0669f9838073571018eb762e98aa6d907456f12
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386463"
---
# <a name="start-a-debugging-session-for-a-uwp-app"></a>UWP アプリのデバッグ セッションを開始する

この記事では、ユニバーサル Windows プラットフォーム (UWP) アプリの Visual Studio デバッグ セッションを始める方法について説明します。 UWP アプリは、XAML と C++、XAML と C# または Visual Basic で記述できます。 UWP アプリのデバッグを始めるには、デバッグ セッションを構成し、アプリを起動する方法を選択します。

::: moniker range=">=vs-2019"
> [!NOTE]
> Visual Studio 2019 以降では、HTML および JavaScript 用の UWP アプリはサポートされなくなりました。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio 2017 では、この記事で示されているほとんどのコマンドとオプションは、HTML および JavaScript 用の UWP アプリにも適用されます。 マネージド アプリと C++ アプリでコマンドが異なる場合、JavaScript アプリは通常、C++ UWP アプリのコマンドと同じです。
::: moniker-end

## <a name="start-debugging-from-the-visual-studio-toolbar"></a><a name="BKMK_The_easy_way_to_start_debugging"></a>Visual Studio ツール バーからデバッグを始める

デバッグを構成して開始する最も簡単な方法は、Visual Studio の標準のツール バーからです。

![ツール バーからのデバッグ](../debugger/media/vsrun_select_target_device.png)

1. **[標準]** ツール バーの **[構成]** ドロップダウンで、 **[デバッグ]** を選択します。

1. **[プラットフォーム]** ドロップダウンから、ビルド対象のターゲット プラットフォームを選択します。

1. 緑の矢印の横にあるドロップダウンから、デバッグ ターゲットを選択します。 ローカル コンピューター、直接接続されているデバイス、ローカル環境の Visual Studio シミュレーター、リモート デバイス、またはエミュレーターを選択できます。

1. デバッグを始めるには、ツール バーの緑の **[開始]** 矢印を選択するか、 **[デバッグ]**  >  **[デバッグの開始]** を選択するか、**F5** キーを押します。

   Visual Studio によってアプリがビルドされ、アタッチされたデバッガーが起動します。

デバッグは、ブレークポイントに達するか、実行が手動で中断されるか、ハンドルされない例外が発生するか、アプリが終了するまで続行されます。

### <a name="deployment-target-options"></a><a name="BKMK_Choose_the_deployment_target"></a> 配置ターゲットのオプション

デバッグ ターゲットは、Visual Studio のツール バーまたはプロジェクトのデバッグ プロパティ ページで設定できます。 次のいずれかのオプションを選択します。

|名前|説明|
|-|-|
|**ローカル コンピューター**|ローカル コンピューターの現在のセッションでアプリをデバッグします。|
|**シミュレーター**|UWP アプリ用の Visual Studio シミュレーターでアプリをデバッグします。 シミュレーターは、ローカル コンピューターに存在しない可能性があるタッチ ジェスチャやデバイスのローテーションなどのデバイス機能をシミュレートするデスクトップ ウィンドウです。 このシミュレーター オプションは、アプリの **[ターゲット プラットフォームの最小バージョン]** がローカル コンピューターのオペレーティング システムと同じかそれより前である場合にのみ使用できます。 詳細については、「[シミュレーターで UWP アプリを実行する](../debugger/run-windows-store-apps-in-the-simulator.md)」を参照してください。|
|**リモート コンピューター**|ネットワークまたはイーサネット ケーブル経由でローカル コンピューターに接続されているデバイスでアプリをデバッグします。 リモート デバイス上に Remote Tools for Visual Studio がインストールされ、実行されている必要があります。 詳細については、「[リモート コンピューターで UWP アプリを実行する](../debugger/run-windows-store-apps-on-a-remote-machine.md)」を参照してください。|
|**デバイス**|USB で接続されたデバイスでアプリをデバッグします。 デバイスは、開発者によってロックが解除されていて、画面のロックが解除されている必要があります。|
|**Mobile Emulator (モバイル エミュレーター)**|エミュレーター名で指定されたエミュレーターを起動し、アプリを配置して、デバッグを開始します。 エミュレーターは、Hyper-V が有効になっているコンピューターでのみ使用できます。|

## <a name="configure-debugging-in-the-project-property-page"></a><a name="BKMK_Open_the_debugging_property_page_for_the_project"></a> プロジェクトのプロパティ ページでデバッグを構成する

追加のデバッグ オプションを構成するには、プロジェクトのデバッグ プロパティ ページを使用します。

**デバッグ プロパティを開くには:**

1. **ソリューション エクスプローラー** で、プロジェクトを選択して **[プロパティ]** アイコンを選択するか、プロジェクトを右クリックして **[プロパティ]** を選択します。

1. **[プロパティ]** ペインの左側で、次のようにします。

   - C# アプリと Visual Basic アプリの場合は、 **[デバッグ]** を選択します。

     ![C# および Visual Basic プロジェクトのデバッグ プロパティ ページ](../debugger/media/dbg_csvb_debugpropertypage.png)

   - C++ アプリの場合は、 **[構成プロパティ]**  >  **[デバッグ]** を選択します。

     ![C++ UWP アプリのデバッグ プロパティ ページ](../debugger/media/dbg_cpp_debugpropertypage.png)

### <a name="choose-the-debugger-to-use"></a><a name="BKMK_Choose_the_debugger_to_use"></a> 使用するデバッガーを選択する

C# アプリと Visual Basic アプリの場合、Visual Studio ではマネージド コードが既定でデバッグされます。 他のコードの種類または追加のコードの種類を選択してデバッグできます。 プロジェクトの一部であるバックグラウンド タスクに対して **[デバッガーの種類]** の値を設定することもできます。

C++ アプリの場合、Visual Studio ではネイティブ コードが既定でデバッグされます。 ネイティブ コードの代わりに、またはネイティブ コードに加えて、特定の種類のコードを選択してデバッグできます。

**デバッグするコードの種類を指定するには:**

- C# アプリと Visual Basic アプリの場合は、 **[デバッグ]** プロパティ ページの **[デバッガーの種類]** の **[アプリケーションの種類]** および **[Background process type]\(バックグラウンド プロセスの種類\)** ドロップダウンから、次のいずれかのデバッガーを選択します。

- C++ アプリの場合は、 **[デバッグ]** プロパティ ページの **[デバッガーの種類]** ドロップダウンから、次のいずれかのデバッガーを選択します。

|名前|説明|
|-|-|
|**マネージドのみ**|アプリのマネージド コードをデバッグします。 JavaScript コードとネイティブ C/C++ コードは無視されます。|
|**ネイティブのみ**|アプリのネイティブ コードと C/C++ コードをデバッグします。 マネージド コードと JavaScript コードは無視されます。|
|**混合 (マネージドとネイティブ)**|アプリのネイティブ C/C++ コードとマネージド コードをデバッグします。 JavaScript コードは無視されます。 C++ プロジェクトでは、このオプションは **[マネージドとネイティブ]** という名前になっています。|
|**スクリプト**|アプリの JavaScript コードをデバッグします。 マネージド コードとネイティブ コードは無視されます。|
|**スクリプトを利用したネイティブ コード**|アプリのネイティブ C/C++ コードと JavaScript コードをデバッグします。 マネージド コードは無視されます。 C++ プロジェクトまたはバックグラウンド タスクでのみ使用できます。|
|**GPU のみ (C++ AMP)**|GPU (Graphics Processing Unit) で実行されるネイティブ C++ コードをデバッグします。 C++ プロジェクトでのみ使用できます。|

### <a name="disable-network-loopbacks-optional"></a><a name="BKMK__Optional__Disable_network_loopbacks"></a> ネットワーク ループバックを無効にする (省略可能)

 セキュリティのため、標準的な方法でインストールされた UWP アプリでは、インストール先のデバイスに対してネットワーク呼び出しを行うことはできません。 Visual Studio では、配置されるアプリに対して既定ではこの規則は適用されないので、1 台のコンピューターで通信手順をテストできます。 アプリをリリースする前に、適用を除外しないでアプリをテストする必要があります。

**ネットワーク ループバックの免除を削除するには:**

- C# および Visual Basic アプリでは、 **[デバッグ]** プロパティ ページの **[開始オプション]** で **[ローカル ネットワーク ループバックの許可]** チェック ボックスをオフにします。

- C++ アプリでは、 **[デバッグ]** プロパティ ページの **[ローカル ネットワーク ループバックの許可]** ドロップダウンで **[いいえ]** を選択します。

### <a name="reinstall-the-app-when-you-start-debugging-optional"></a><a name="BKMK__Optional__Reinstall_the_app_when_you_start_debugging"></a> デバッグの開始時にアプリケーションを再インストールする (省略可能)
 C# または Visual Basic アプリでインストールの問題を診断するには、 **[デバッグ]** プロパティ ページで **[Uninstall and then re-install my package]\(パッケージをアンインストールしてから再インストールする\)** を選択します。 このオプションでは、デバッグの開始時に元のインストールが再作成されます。 このオプションは、C++ プロジェクトでは使用できません。

### <a name="set-authentication-options-for-remote-debugging"></a><a name="BKMK__Optional__Disable_authentication_requirement_to_start_the_remote_debugger"></a> リモート デバッグの認証オプションを設定する

既定では、配置ターゲットとして **[リモート コンピューター]** を選択したときは、リモート デバッガーを実行するために Windows 資格情報を指定する必要があります。 認証の要件は変更できます。

**[ユニバーサル (暗号化されていないプロトコル)]** 認証モードは、IoT、Xbox、HoloLens デバイス、および Windows 10 Creators Update 以降の PC 用です。

**認証方法を変更するには:**

- C# アプリと Visual Basic アプリの場合は、 **[デバッグ]** プロパティ ページで、 **[ターゲット デバイス]** として **[リモート コンピューター]** を選択します。 次に、 **[認証モード]** として **[なし]** または **[ユニバーサル (暗号化されていないプロトコル)]** を選択します。

- C++ アプリの場合は、 **[デバッグ]** プロパティ ページの **[起動するデバッガー]** で **[リモート コンピューター]** を選択します。 次に、 **[認証の種類]** として **[認証なし]** または **[ユニバーサル (暗号化されていないプロトコル)]** を選択します。

> [!CAUTION]
> **[なし]** または **[ユニバーサル (暗号化されていないプロトコル)]** モードでリモート デバッガーを実行した場合、ネットワーク セキュリティはありません。 これらのモードは、悪意のあるコードや敵対的なトラフィックのリスクがないことが確実である、信頼されるネットワークに対してのみ選択してください。

## <a name="debugging-start-options"></a><a name="BKMK_Start_the_debugging_session"></a> デバッグ開始のオプション

**[デバッグ]**  >  **[デバッグの開始]** を選択するか、**F5** キーを押すと、Visual Studio によってデバッガーがアタッチされた状態でアプリが起動されます。 実行は、ブレークポイントに達するか、実行が手動で中断されるか、ハンドルされない例外が発生するか、アプリが終了するまで続行されます。

### <a name="start-debugging-but-delay-app-start"></a><a name="BKMK_Start_debugging__F5__but_delay_the_app_start"></a> デバッグは開始するがアプリの起動は遅らせる

既定では、デバッグを開始すると直ちに Visual Studio によってアプリが起動されます。 また、デバッグ モードで実行するが、デバッガーの外部で開始するように、アプリを設定することもできます。 たとえば、Windows の **[スタート]** メニューからのアプリの起動をデバッグしたり、アプリでバックグラウンド プロセスをデバッグしたりする場合です。 このオプションを選択した場合、アプリは起動時にデバッガーで開始されます。

**アプリの自動起動を無効にするには:**

- C# アプリと Visual Basic アプリの場合は、 **[デバッグ]** プロパティ ページの **[開始オプション]** で **[起動はしないが、開始時にコードをデバッグする]** を選択します。

- C++ アプリでは、 **[デバッグ]** プロパティ ページの **[アプリケーションの起動]** ドロップダウンで **[いいえ]** を選択します。

バックグラウンド タスクのデバッグの詳細については、[UWP アプリの一時停止イベント、再開イベント、バックグラウンド イベントのトリガー](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)に関するページを参照してください。

### <a name="debug-an-installed-or-running-uwp-app"></a><a name="BKMK_Start_an_installed_app_in_the_debugger"></a> インストールされている UWP アプリまたは実行中の UWP アプリをデバッグする

**[インストールされているアプリ パッケージのデバッグ]** を使用して、ローカル デバイスまたはリモート デバイスで既にインストールまたは実行されている UWP アプリをデバッグすることができます。 アプリは、Microsoft Store からインストールされている場合、または Visual Studio プロジェクトではない場合があります。 たとえば、Visual Studio を使用しないカスタム ビルド システムがアプリにあるような場合です。

インストールされているアプリをすぐに起動することも、別の方法で起動されたらデバッガーで実行するように設定することもできます。 詳細については、[UWP アプリの一時停止イベント、再開イベント、バックグラウンド イベントのトリガー](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)に関するページを参照してください。

インストール済みまたは実行中の UWP アプリをデバッガーで起動するには、 **[デバッグ]**  >  **[その他のデバッグ ターゲット]**  >  **[インストールされているアプリ パッケージのデバッグ]** を選択します。 詳細については、[インストールされているアプリ パッケージのデバッグ](../debugger/debug-installed-app-package.md)に関するページを参照してください。

### <a name="attach-the-debugger-to-a-running-windows-8x-app"></a><a name="BKMK_Attach_the_debugger_to_a_running_app_"></a> 実行中の Windows 8.x アプリにデバッガーをアタッチする

[!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリにデバッガーをアタッチするには、デバッグ可能パッケージ マネージャーを使用して、デバッグ モードで実行するようにアプリを設定する必要があります。 デバッグ可能パッケージ マネージャーは、Remote Tools for Visual Studio でインストールされます。

1. アプリをインストールするデバイスに Remote Tools for Visual Studio をインストールします。 詳細については、[リモート ツールのインストール](../debugger/remote-debugging.md)に関するページを参照してください。

1. Windows の **[スタート]** 画面で、**デバッグ可能パッケージ マネージャー** を探して起動します。

   AppxDebug コマンドレット用に適切に構成された PowerShell ウィンドウが表示されます。

1. アプリの PackageFullName 識別子を指定します。

   1. すべてのアプリの PackageFullName が含まれる一覧を表示するには、PowerShell プロンプトで「`Get-AppxPackage`」と入力します。

   1. PowerShell プロンプトに「`Enable-AppxDebug <PackageFullName>`」と入力します。\<PackageFullName> はアプリの PackageFullName 識別子です。

1. **[デバッグ]**  >  **[プロセスにアタッチ]** の順に選択します。

1. **[プロセスにアタッチ]** ダイアログ ボックスの **[接続先]** ボックスで、リモート デバイスを指定します。

   デバイス名を入力するか、 **[接続先]** ボックスのドロップダウンから選択するか、 **[検索]** を選択して **[リモート接続]** ダイアログ ボックスでデバイスを検索することができます。

1. デバッグするコードの種類を指定するには、 **[アタッチ先]** ボックスの隣にある **[選択]** を選択します。

1. **[コードの種類の選択]** ダイアログ ボックスで、次のいずれかを選択します。
   - **[デバッグするコードの種類を自動的に判断する]**
   - **[次のコードの種類をデバッグする]** 。その後、一覧からコードの種類を 1 つ以上選択します。

1. **[使用可能なプロセス]** の一覧で、デバッグするアプリのプロセスを選択します。

1. **[接続]** を選択します。

 Visual Studio によって、デバッガーがプロセスにアタッチされます。 実行は、ブレークポイントに達するか、実行が手動で中断されるか、ハンドルされない例外が発生するか、アプリが終了するまで続行されます。

::: moniker range="vs-2017"
> [!NOTE]
> JavaScript アプリは、*wwahost.exe* プロセスのインスタンスで実行されます。 複数の JavaScript アプリが実行されている場合は、アタッチするアプリの *wwahost.exe* プロセスの数字プロセス ID (PID) を知っている必要があります。
>
> 特定の JavaScript アプリにアタッチする最も簡単な方法は、他のすべての JavaScript アプリを閉じることです。 または、アプリを起動する前に、Windows タスク マネージャーで実行中の *wwahost.exe* プロセスの PID を記録しておきます。 起動したアプリの *wwahost.exe* の PID は、先ほど記録したものとは異なる値になります。
::: moniker-end

## <a name="see-also"></a>関連項目

- [Visual Studio でのアプリのデバッグ](../debugger/debugging-windows-store-and-windows-universal-apps.md)