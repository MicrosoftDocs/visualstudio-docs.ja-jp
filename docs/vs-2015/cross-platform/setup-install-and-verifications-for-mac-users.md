---
title: Mac ユーザー向けのセットアップ、インストール、および 検証 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 22725520-59ba-4f6f-80e4-097b1287a34b
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: 751cf3c05841be39c961544b7cedba95ca64b808
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49940387"
---
# <a name="setup-install-and-verifications-for-mac-users"></a>Mac ユーザー向けのセットアップ、インストール、および 検証
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
このトピックは、主に Mac で作業し、Mac で Windows 仮想マシン内部の Visual Studio を必要に応じて使用する開発者を対象としています。 主に Windows コンピューターで作業する開発者であり、かつ iOS をターゲットとするためにセカンダリの Mac を設定する必要がある場合は、メインの「[Setup and install](../cross-platform/setup-and-install.md)」トピックをご覧ください。  
  
 Mac で Xamarin を操作するには、次の条件が必要です。  
  
- Xamarin アカウント。 移動[ https://www.xamarin.com/ ](https://www.xamarin.com/) をクリック**サインイン**、ページの右上にあるをクリックし、**新しいアカウントを作成**表示されるページ。 Xamarin アカウントの電子メール アドレスとパスワードを選択します。  
  
- Xcode 7 および Xamarin 4 がインストールされた、OSX Yosemite (10.10) 以降を搭載した Mac。  
  
- 次の構成のいずれか。  
  
  -   **Mac 上で直接 Xamarin Studio を実行する場合:** Xamarin Studio は、C# を使用した Android、iOS、および Windows のアプリ作成をサポートする Xamarin の開発環境です。  Xamarin Studio の概要をすばやく確認するには、「 [Xamarin Studio の概要](https://xamarin.com/studio) 」(xamarin.com) を参照してください。  
  
  -   **既に Parallels または VMWare がMac に構成されている場合:** Parallels または VMWare 内の Visual Studio 2015 と Xamarin 4 で Windows を実行します。  この構成では、Xamarin は拡張機能であり、C# を使用して Android、iOS、および WinPhone のアプリを作成するための開発環境として Visual Studio を使用する機能を提供する Visual Studio と共にインストールされます。  Visual Studio Developer Essentials プログラムの一部として、3 か月無料の Parallels サブスクリプションを取得できます。 「 [Microsoft Visual Studio Dev Essentials には、Parallels Desktop Pro と Parallels Access が含まれます](http://blog.parallels.com/blog/2015/11/18/visual-studio-dev-essentials/) 」(Parallels ブログ) を参照してください。  
  
  このトピックでは、これらの要件について説明します。  インストール プロセスの実行中に、トピック「[Xamarin を使用したモバイル開発について学習します](../cross-platform/learn-about-mobile-development-with-xamarin.md)」を参照して、必要な背景情報に注目することができます。  
  
  **このトピックの内容:**  
  
- [Mac のセットアップ (Apple ID、Xcode、および Xamarin)](#mac)  
  
- [Parallels (Visual Studio と Xamarin) 内での Windows のセットアップ](#windows)  
  
- [環境の確認](#verify)  
  
##  <a name="mac"></a> Mac のセットアップ (Apple ID、Xcode、および Xamarin)  
  
1.  [My Apple ID](https://appleid.apple.com/) で無料の Apple ID を作成します (まだ作成していない場合)。 これは Xcode をインストールしてサインインするために必要です。  
  
2.  ダウンロードしてから Xcode をインストール[ https://developer.apple.com/xcode/](https://developer.apple.com/xcode/)します。  
  
3.  「 [Xamarin.iOS のダウンロードとインストール](http://developer.xamarin.com/guides/ios/getting_started/installation/mac/) 」(xamarin.com) の手順に従って、Xamarin をダウンロードしてインストールします。  
  
4.  Windows と Mac のコンピューターの両方に Xamarin をインストールしたら、「[XMA を使用した Mac への接続](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/#Connecting_to_the_Mac_Using_XMA)」(xamarin.com) の手順に従って、Windows コンピューター上の Visual Studio から iOS と Mac を扱えるようにします。  
  
##  <a name="windows"></a> Parallels (Visual Studio と Xamarin) 内での Windows のセットアップ  
  
1.  Parallels/VMWare 内に構成した Windows デスクトップを使用して、 [任意のエディションの Visual Studio 2015 のインストーラーをダウンロードして起動します](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) (Community、Professional、または Enterprise)。 Visual Studio 2015 Community は、無償のエディションです。Professional および Enterprise の各エディションは評価版として 30 日間使用できます。  
  
2.  インストーラー内で、 **[カスタム]** インストールを選択します。  
  
     ![Visual Studio のインストールで [カスタム] オプションを選びます](../cross-platform/media/cross-plat-xamarin-setup-1.png "クロスプラットフォームの Xamarin セットアップ 1")  
  
3.  次のチェック ボックスをオン/オフにします。  
  
    1.  **[クロスプラットフォーム モバイル開発] > [C#/.NET (Xamarin)]** を選択します。 これにより、[共通のツールとソフトウェア開発キット] の下のさまざまな Android ツールも自動的に選択されます。  
  
         ![[クロスプラットフォーム モバイル開発] の [Xamarin] オプションを選択します](../cross-platform/media/cross-plat-xamarin-setup-2.png "クロスプラットフォームの Xamarin セットアップ 2")  
  
    2.  **[クロスプラット フォーム モバイル開発] > [Microsoft Visual Studio Emulator for Android]** の選択を解除します。  
  
4.  [インストール] ボタンをクリックし、プロセスを実行します。 このプロセスでも、完了までにしばらく時間がかかります。この間、このトピックの続きを読み、「[Xamarin を使用したモバイル開発について学習します](../cross-platform/learn-about-mobile-development-with-xamarin.md)」を読むことができます。  
  
5.  インストールが完了したら、Visual Studio を起動し、アカウントを求められたら Microsoft アカウントでサインインします (これは Windows で使用するのと同じアカウントです)。 次に、**[ツール] > [オプション] > [Xamarin]** または **[ツール] > [オプション] > [Xamarin] > [その他]** を選択して、Xamarin の更新プログラムを確認します。ここには **[今すぐ確認]** リンクが表示されます。  
  
     ![Visual Studio のオプションで Xamarin の更新プログラムを確認します](../cross-platform/media/cross-plat-xamarin-setup-3.png "クロスプラットフォームの Xamarin セットアップ 3")  
  
    > [!NOTE]
    >  以前の Xamarin でのライセンス問題を回避するために、Xamarin をバージョン 4.0.3.214 以上に更新してください。  更新プログラムを確認しようとして Microsoft ビルド ツールに関するエラーが表示された場合は、[Xamarin のフォーラム](http://forums.xamarin.com/discussion/69015/xamarin-update-on-vs-2013-says-i-need-the-build-tools-for-vs-2015)のスレッドをご覧ください。
  
6.  Windows と Mac のコンピューターの両方に Xamarin をインストールしたら、「[XMA を使用した Mac への接続](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/#Connecting_to_the_Mac_Using_XMA)」(xamarin.com) の手順に従って、Windows コンピューター上の Visual Studio から iOS と Mac を扱えるようにします。  
  
##  <a name="verify"></a> 環境の確認  
 インストーラーが完了したら、数分をかけて、Xamarin 開発を実行するための準備ができているかどうかを確認します。  
  
### <a name="xamarin-studio"></a>Xamarin Studio  
 まず初めに、提供されたリンクへの移動時に、右上隅で **Xamarin Studio** が選択され、適切なバージョンの Xamarin ドキュメントが表示されていることを確認します。  
  
 ![Xamarin Studio を選択して、Xamarin.com で適切なドキュメントを表示します](../cross-platform/media/crossplat-xamarin-mac-1.png "CrossPlat Xamarin Mac 1")  
  
 **Outlook Web Access (OWA)**  
  
1. 「 [Android プロジェクトの作成](http://developer.xamarin.com/recipes/android/general/projects/create_an_android_project/) 」(xamarin.com) の手順に従って、Android プロジェクトの作成を検証します。  
  
2. [Android Player > Xamarin Studio ドキュメントとの統合](https://developer.xamarin.com/guides/android/getting_started/installation/android-player/#Integration_with_Xamarin_Studio) (xamarin.com) を通して、Android Player でのデバッグを検証します。  
  
   **iOS**  
  
3. 「 [iOS の作成](http://developer.xamarin.com/recipes/ios/general/projects/create_an_ios_project/) 」(xamarin.com) の手順に従って、iOS プロジェクトの作成を検証します。  
  
4. 「 [シミュレーターのドキュメントでのデバッグ](https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/#Debugging_on_the_Simulator) 」(xamarin.com) を通して、iOS シミュレーターでのデバッグを検証します。  
  
### <a name="visual-studio"></a>Visual Studio  
 まず初めに、提供されたリンクへの移動時に、右上隅で **Visual Studio** が選択され、適切なバージョンの Xamarin ドキュメントが表示されていることを確認します。  
  
 ![Visual Studio を選択して、Xamarin.com で適切なドキュメントを表示します](../cross-platform/media/crossplat-xamarin-mac-2.png "CrossPlat Xamarin Mac 2")  
  
 **[ツール] > [Xamarin アカウント...]** で Xamarin アカウントにサインインします。  
  
 **Android**  
  
1. 「 [Android プロジェクトの作成](http://developer.xamarin.com/recipes/android/general/projects/create_an_android_project/) 」(xamarin.com) の手順に従って、Android プロジェクトの作成を検証します。  
  
2. Android デザイナーの検証: Android プロジェクトのソリューション エクスプローラーで、**[リソース] > [レイアウト] > [Main.axml]** ファイルを開きます   
  
   -   「インストールされている Android SDK が古すぎます」というエラーが発生した場合は、クリックして**Android SDK を開く**でメッセージし、最新の SDK バージョンを選択します。 SDK を更新するには、管理者として Visual Studio を実行している必要があることに注意してください。  
  
3. Mac にインストールされているエミュレーターに Visual Studio から接続できることを検証します。  この結果、デバッグ用に Visual Studio 内から選択できるエミュレーターの一覧に Xamarin Player が表示されます。  これを行うには、「 [Visual Studio を Xamarin Android Player に接続する](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/android-player-with-visual-studio-in-vm/) 」(xamarin.com) の手順に従います。  
  
   **iOS**  
  
4. 「 [Connecting to the Mac using XMA](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/#Connecting_to_the_Mac_Using_XMA) 」(xamarin.com) で説明されているように、ネットワーク上で Mac が利用でき、Visual Studio とペアになっていることを確認してください。  
  
5. 「 [iOS の作成](http://developer.xamarin.com/recipes/ios/general/projects/create_an_ios_project/) 」(xamarin.com) の手順に従って、iOS プロジェクトの作成を検証します。  
  
6. ストーリーボード デザイナーの検証: ソリューション エクスプローラーの iOS プロジェクトで、 **MainStoryboard.storyboard** ファイルを開きます。 ここでは、Visual Studio が Mac でリモート実行されているデザイナーをホストしています。  
  
7. ビルドとデバッグの検証:  
  
   1.  ソリューション エクスプローラーで iOS プロジェクトを右クリックして **[スタートアップ プロジェクトに設定]** を選択します。  
  
   2.  次に示すように、Visual Studio のビルド ドロップダウン リストで **iPhoneSimulator** のターゲットを選びます。 シミュレーターが表示されていない場合は、Mac で Xcode を起動し、**[Xcode] > [ユーザー設定]** の順に選び、**[ダウンロード]** をクリックします。 **[コンポーネント]** の下に、ダウンロード可能なシミュレーターのバージョンが表示されます。 デバッグに関する詳しい説明については、Xamarin の「 [デバッグ](https://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/#Debugging_on_the_Simulator) 」ページ (xamarin.com) をご覧ください。  
  
        ![iPhoneSimulator ビルド ターゲットを選択しています](../cross-platform/media/crossplat-xamarin-verify-5.png "CrossPlat Xamarin Verify 5")  
  
   3.  次に示すように、Visual Studio のデバッグ ドロップダウン リストで iPhone のターゲットを選び、F5 キーを押してデバッガーを開始します。 これによって、Mac 上のシミュレーターが起動し、Visual Studio でのデバッグ中にアプリを操作できるようになります。  
  
        ![iPhone デバッグ ターゲットを選択しています](../cross-platform/media/crossplat-xamarin-verify-6.png "CrossPlat Xamarin Verify 6")

