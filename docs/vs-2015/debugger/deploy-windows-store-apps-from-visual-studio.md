---
title: Windows ストア アプリをデプロイします。
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: ef3a0f36-bfc9-4ca0-aa61-18261f619bff
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 73b4350a2e7f277a11f4d6650d8089df0f87fe4d
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60116395"
---
# <a name="deploy-windows-store-apps-from-visual-studio"></a>Visual Studio からの Windows ストア アプリの配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Applies to Windows only](../Image/windows_only_content.png "windows_only_content")

 Visual Studio の配置機能では、Visual Studio を使ってターゲット デバイスに作成した Windows ストア アプリをビルドおよび登録します。 アプリの厳密な登録方法は、ターゲット デバイスがローカルかリモートかによって違います。

- ターゲットがローカルの Visual Studio コンピューターの場合、Visual Studio はアプリをビルド フォルダーから登録します。

- ターゲットがリモート デバイスの場合、Visual Studio は必要なファイルをリモート コンピューターにコピーしてから、そのデバイス上でアプリを登録します。

  使用して Visual Studio からアプリをデバッグするときに、展開は自動、**デバッグの開始**オプション (キーボード。F5 キーを押して)、または**デバッグなしで開始**オプション (キーボード。CTRL キーを押しながら F5 キー)。 アプリを手動で配置することも可能です。 次のシナリオでは、手動の配置は有効です。

- ローカル コンピューターまたはリモート コンピューターで行う臨時のテスト。

- デバッグ対象のアプリを起動するためのアプリを配置する場合。

- 別のアプリまたはメソッドによって起動される、デバッグ対象のアプリを配置します。

## <a name="BKMK_In_this_topic"></a> このトピックの内容
 このトピックでは、次について説明します。

 [Windows ストア アプリの配置方法](#BKMK_How_to_deploy_a_Windows_Store_app)

 [リモート デバイスの指定方法](#BKMK_How_to_specify_a_remote_device)

 [配置オプション](#BKMK_Deployment_options)

## <a name="BKMK_How_to_deploy_a_Windows_Store_app"></a> Windows ストア アプリの配置方法
 アプリを手動で配置する手順はシンプルです。

1. リモート デバイスへ配置する場合は、アプリのスタートアップ プロジェクトのプロパティ プロジェクト ページに、デバイスの名前または IP アドレスを指定します。 (指定するステップはこのトピック内で後述)。

2. デバッガーの Visual Studio ツールバーで、 **[デバッグの開始]** ボタンの横のドロップダウン リストから配置ターゲットを選択します。

     ![ローカル コンピューターで実行](../debugger/media/vsrun-f5-local.png "VSRUN_F5_Local")

3. **[ビルド]** メニューで **[配置]** を選択

## <a name="BKMK_How_to_specify_a_remote_device"></a> リモート デバイスの指定方法
 **必要条件**

 アプリをリモート デバイスに配置するには

- リモート デバイスに開発者ライセンスがインストールされている必要があります。

- リモート デバイスには、Visual Studio リモート ツールをインストールする必要があり、リモート デバッグ モニターが動作している必要があります。

     配置では、リモート デバッガーのネットワーク チャネルを使用して、アプリのファイルをリモート デバイスに送信します。

#### <a name="to-specify-a-remote-device"></a>リモート デバイスを指定するには

1. スタートアップ プロジェクトのデバッグ プロパティ ページで、リモートの配置ターゲットの名前または IP アドレスを指定します。

2. デバッグ プロパティ ページを開くには、ソリューション エクスプローラーでプロジェクトを選択してから、ショートカット メニューで **[プロパティ]** を選択します。

3. 次に、プロパティ ページ ウィンドウで **[デバッグ]** ノードを選択します。

4. リモート デバイスの名前または IP アドレスを入力するか、 **[リモート デバッガー接続の選択]** ダイアログ ボックスからデバイスを選択します。

    ![リモート デバッガー接続 ダイアログ ボックスをオン](../debugger/media/vsrun-selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

    **[リモート デバッガー接続の選択]** ダイアログ ボックスは、ローカル ネットワークのサブネットにあるデバイスと、Visual Studio コンピューターにイーサネット ケーブルで直接接続されているデバイスを表示します。

   **JavaScript または Visual C++ のプロジェクト ページにあるリモート デバイスを指定**

   ![C&#43; &#43;リモート デバッグのプロパティをプロジェクト](../debugger/media/vsrun-cpp-projprop-remote.png "VSRUN_CPP_ProjProp_Remote")

5. **[起動するデバッガー]** ボックスの一覧の **[リモート デバッガー]** をクリックします。

6. **[コンピューター名]** ボックスのリモート デバイスにネットワーク名を入力します。 あるいはボックス内の下向き矢印をクリックして、[リモート デバッガー接続の選択] ダイアログ ボックスからデバイスを選択します。

   **Visual C# および Visual Basic のプロジェクト ページにあるリモート デバイスを指定**

   ![リモート デバッグ用のプロジェクトのプロパティを管理](../debugger/media/vsrun-managed-projprop-remote.png "VSRUN_Managed_ProjProp_Remote")

7. **[ターゲット デバイス]** ボックスの一覧の **[リモート コンピューター]** をクリックします。

8. リモート デバイスのネットワーク名を **[リモート コンピューター]** ボックスに入力するか、 **[検索]** をクリックし、 **[リモート デバッガー接続の選択]** ダイアログ ボックスでデバイスを選択します。

## <a name="BKMK_Deployment_options"></a> 配置オプション
 次の配置オプションを、スタートアップ プロジェクトのデバッグ プロパティ ページに設定できます。

 **ネットワーク Loopback を許可する**セキュリティ上の理由から、[!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]にインストールされたデバイスへのネットワーク呼び出しを実行する標準的な方法でインストールされているアプリが許可されていません。 既定では、Visual Studio による配置では、配置されたアプリに対するこの規則の適用は免除されます。 この免除によって、1 台のコンピューター上で通信プロシージャをテストできます。 アプリを [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)]に送信する前に、アプリを適用除外せずにテストする必要があります。

 アプリからネットワーク ループバックの適用除外を削除するには

- C# および VB のデバッグ プロパティ ページで、 **[ネットワーク ループバックの許可]** チェック ボックスをクリアします。

- JavaScript およびデバッグ プロパティ ページで、 **[ネットワーク ループバックの許可]** の値を **[いいえ]** に設定します。

  **起動しないが、開始時に、コードをデバッグ (C#および VB)/アプリケーションを起動 (JavaScript および C++)** 、アプリが起動したときに、デバッグ セッションを自動的に起動する展開を構成します。

- C# および VB のデバッグ プロパティ ページで、 **[起動しないが、開始時にコードをデバッグ]** チェック ボックスをオンにします。

- JavaScript およびデバッグ プロパティ ページで、 **[アプリケーションの起動]** の値を **[はい]** に設定します。

## <a name="see-also"></a>関連項目
 [Visual Studio からアプリを実行](../debugger/run-store-apps-from-visual-studio.md)
