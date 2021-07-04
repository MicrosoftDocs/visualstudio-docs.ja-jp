---
title: UWP アプリを配置する | Microsoft Docs
description: Visual Studio からユニバーサル Windows プラットフォーム (UWP) アプリを展開します。 展開に対してローカルまたはリモートのターゲット デバイスを指定します。 展開オプションを理解します。
ms.custom: SEO-VS-2020
ms.date: 01/16/2018
ms.topic: conceptual
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
ms.openlocfilehash: 0a1c1802d92beb436bbd2ac87bd1e7a39f6086f1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387867"
---
# <a name="deploy-uwp-apps-from-visual-studio"></a>Visual Studio から UWP アプリを展開する

Visual Studio の配置機能では、Visual Studio を使ってターゲット デバイスに作成した UWP アプリをビルドおよび登録します。 アプリの厳密な登録方法は、ターゲット デバイスがローカルかリモートかによって違います。

- ターゲットがローカルの Visual Studio コンピューターの場合、Visual Studio はアプリをビルド フォルダーから登録します。

- ターゲットがリモート デバイスの場合、Visual Studio は必要なファイルをリモート コンピューターにコピーしてから、そのデバイス上でアプリを登録します。

Visual Studio から **[デバッグの開始]** オプション (キーボード: F5) または **[デバッグなしで開始]** オプション (キーボード: CTRL + F5) を使用してアプリをデバッグすると、配置は自動的に行われます。 アプリを手動で配置することも可能です。 次のシナリオでは、手動の配置は有効です。

- ローカル コンピューターまたはリモート コンピューターで行う臨時のテスト。

- デバッグ対象のアプリを起動するためのアプリを配置する場合。

- 別のアプリまたはメソッドによって起動される、デバッグ対象のアプリを配置します。

## <a name="how-to-deploy-a-uwp-app"></a><a name="BKMK_How_to_deploy_a_Windows_Store_app"></a> UWP アプリを配置する方法
 アプリを手動で配置する手順はシンプルです。

1. リモート デバイスへ配置する場合は、アプリのスタートアップ プロジェクトのプロパティ プロジェクト ページに、デバイスの名前または IP アドレスを指定します。 (指定するステップはこのトピック内で後述)。

2. デバッガーの Visual Studio ツールバーで、 **[デバッグの開始]** ボタンの横のドロップダウン リストから配置ターゲットを選択します。

     ![ローカル コンピューターでの実行](../debugger/media/vsrun_f5_local.png "VSRUN_F5_Local")

3. **[ビルド]** メニューで **[配置]** を選択

## <a name="how-to-specify-a-remote-device"></a><a name="BKMK_How_to_specify_a_remote_device"></a> リモート デバイスの指定方法

**必須コンポーネント**

Windows 10 のリモート デバイスで有効にする必要があります[開発者モード](/windows/uwp/get-started/enable-your-device-for-development)します。 Creator の更新プログラムを実行する Windows 10 デバイスで以降、リモート ツールが自動的にインストールされているアプリを展開するときにします。 詳細については、次を参照してください。 [インストールされているアプリ パッケージをデバッグ](../debugger/debug-installed-app-package.md)します。

> [!NOTE]
> Windows 10 の Creator's Update より前のバージョンでは、Remote Tools for Visual Studio がリモート デバイスにインストールされ、リモート デバッガーが実行されている必要があります。

配置では、リモート デバッガーのネットワーク チャネルを使用して、アプリのファイルをリモート デバイスに送信します。

#### <a name="to-specify-a-remote-device"></a>リモート デバイスを指定するには

1. スタートアップ プロジェクトのデバッグ プロパティ ページで、リモートの配置ターゲットの名前または IP アドレスを指定します。

2. デバッグ プロパティ ページを開くには、ソリューション エクスプローラーでプロジェクトを選択してから、ショートカット メニューで **[プロパティ]** を選択します。

3. 次に、プロパティ ページ ウィンドウで **[デバッグ]** ノードを選択します。

4. **[ターゲット デバイス]** には **[リモート コンピューター]** を選択します。

5. **[リモート コンピューター]** で **[検索]** をクリックします。

6. リモート デバイスの名前または IP アドレスを入力するか、 **[リモート接続]** ダイアログ ボックスからデバイスを選択することができます。

    ![リモート デバッガーの接続の選択ダイアログ ボックス](../debugger/media/vsrun_selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

    **[リモート接続]** ダイアログ ボックスは、ローカル ネットワークのサブネットにあるデバイスと、Visual Studio コンピューターにイーサネット ケーブルで直接接続されているデバイスを表示します。

   **C++ プロジェクト ページでのリモート デバイスの指定**

   ![リモート デバッグ用の C&#43;&#43; プロジェクト プロパティ](../debugger/media/vsrun_cpp_projprop_remote.png "VSRUN_CPP_ProjProp_Remote")

7. **[起動するデバッガー]** ボックスの一覧の **[リモート デバッガー]** をクリックします。

8. **[コンピューター名]** ボックスのリモート デバイスにネットワーク名を入力します。 あるいはボックス内の下向き矢印をクリックして、[リモート デバッガー接続の選択] ダイアログ ボックスからデバイスを選択します。

   **Visual C# および Visual Basic のプロジェクト ページにあるリモート デバイスを指定**

   ![リモート デバッグ用のマネージド プロジェクト プロパティ](../debugger/media/vsrun_managed_projprop_remote.png "VSRUN_Managed_ProjProp_Remote")

9. **[ターゲット デバイス]** ボックスの一覧の **[リモート コンピューター]** をクリックします。

10. リモート デバイスのネットワーク名を **[リモート コンピューター]** ボックスに入力するか、 **[検索]** をクリックし、 **[リモート デバッガー接続の選択]** ダイアログ ボックスでデバイスを選択します。

## <a name="deployment-options"></a><a name="BKMK_Deployment_options"></a> 配置オプション

次の配置オプションを、スタートアップ プロジェクトのデバッグ プロパティ ページに設定できます。

**ネットワーク ループバックの許可**

セキュリティ上の理由から、標準的な方法でインストールされた UWP または [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] アプリは、インストール先のデバイスに対してネットワーク呼び出しを行うことはできません。 既定では、Visual Studio による配置では、配置されたアプリに対するこの規則の適用は免除されます。 この免除によって、1 台のコンピューター上で通信プロシージャをテストできます。 アプリを [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)]に送信する前に、アプリを適用除外せずにテストする必要があります。

アプリからネットワーク ループバックの適用除外を削除するには

- C# および Visual Basic のデバッグ プロパティ ページで、 **[Allow Network Loopback]\(ネットワーク ループバックの許可\)** チェック ボックスをオフにします。

- C++ のデバッグ プロパティ ページで、 **[Allow Network Loopback]\(ネットワーク ループバックの許可\)** 値を **[いいえ]** に設定します。

**[起動はしないが、開始時にコードをデバッグする] (C# と Visual Basic) または [アプリケーションの起動] (C++)**

アプリが起動した場合はデバッグ セッションを自動駅に開始するように、配置を構成するには

- C# および Visual Basic のデバッグ プロパティ ページで、 **[起動はしないが、開始時にコードをデバッグする]** チェック ボックスをオンにします。

- C++ のデバッグ プロパティ ページで、 **[アプリケーションの起動]** の値を **[はい]** に設定します。

## <a name="see-also"></a>関連項目

- [高度なリモート配置オプション](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [インストールされているアプリケーション パッケージをデバッグする](../debugger/debug-installed-app-package.md)
- [Visual Studio からアプリを実行](debugging-windows-store-and-windows-universal-apps.md)
