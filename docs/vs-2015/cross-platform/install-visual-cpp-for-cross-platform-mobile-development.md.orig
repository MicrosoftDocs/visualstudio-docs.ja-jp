---
title: Visual C++ for Cross-Platform Mobile Development のインストール | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: aaea6b8d-55eb-4427-8185-c050f855c257
caps.latest.revision: 17
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 47285fe9fb57b9c4d5d80c60f9e626f394e11934
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54762860"
---
# <a name="install-visual-c-for-cross-platform-mobile-development"></a>Visual C++ for Cross-Platform Mobile Development のインストール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Visual C++ for Cross-Platform Mobile Development](http://go.microsoft.com/fwlink/p/?LinkId=536383) は、Visual Studio 2015 付属のインストール可能なコンポーネントです。 クロス プラットフォームの Visual Studio テンプレートが含まれており、クロス プラットフォーム ツールおよび SDK をインストールしてすぐに開始できるようにします。それらを自分で検索、ダウンロード、構成する必要はありません。 これらのツールを Visual Studio で使用することで、クロス プラットフォーム プロジェクトを簡単に作成、編集、デバッグ、テストできます。 このトピックでは、Visual Studio を使用してクロス プラットフォーム アプリを開発するために必要なツールとサード パーティのソフトウェアをインストールする方法について説明します。 コンポーネントの概要については、「 [Visual C++ クロスプラットフォーム モバイル](http://go.microsoft.com/fwlink/p/?LinkId=536387)」をご覧ください。  
  
 [要件](#Requirements)   
 [ツールの取得](#GetTheTools)   
 [ツールのインストール](#InstallTheTools)   
 [Install tools for iOS](#InstallForiOS)   
 [手動による依存関係のインストールまたは更新](#ThirdParty)  
  
##  <a name="Requirements"></a> 要件  
  
- インストール要件については、「 [Visual Studio 2015 のシステム要件](https://www.visualstudio.com/visual-studio-2015-system-requirements-vs)」をご覧ください。  
  
  > [!IMPORTANT]
  >  Windows 7 または Windows Server 2008 R2 を使用している場合は、従来の Windows アプリケーション、Android Native Activity アプリおよびライブラリ、iOS 用のアプリとコード ライブラリのためのコードを開発できますが、Windows ストア アプリまたはユニバーサル Windows アプリのコードは開発できません。  
  
  特定のデバイス プラットフォームのアプリをビルドするには、いくつかの追加要件があります。  
  
- Windows Phone エミュレーターおよび Microsoft Visual Studio Emulator for Android には、Hyper-V を実行できるコンピューターが必要です。 エミュレーターをインストールして実行する前に、Windows の Hyper-V 機能を有効にする必要があります。 詳細については、エミュレーターの[システム要件](http://msdn.microsoft.com/4d5bb438-231a-4cd2-84b7-e9660b0e3baf)をご覧ください。  
  
- Android SDK に付属している x86 Android エミュレーターは、Intel HAXM ドライバーを実行できるコンピューター向けに最適化されています。 このドライバーには、VT-x および Execute Disable Bit をサポートしている Intel x64 プロセッサが必要です。 詳しくは、「 [Intel® Hardware Accelerated Execution Manager のインストール手順 - Microsoft Windows](http://go.microsoft.com/fwlink/p/?LinkId=536385)」をご覧ください。  
  
- iOS 用のコードをビルドするには、Apple ID、iOS Developer Program アカウント、[Xcode 6](http://go.microsoft.com/fwlink/p/?LinkId=536387) 以降を OS X Mavericks 以降のバージョンで実行できる Mac コンピューターが必要です。 簡単なインストール手順については、「 [Install tools for iOS](#InstallForiOS)」をご覧ください。  
  
##  <a name="GetTheTools"></a> ツールの取得  
 Visual C++ for Cross-Platform Mobile Development は、Visual Studio の Community、Professional、Enterprise エディションに付属しているインストール可能なコンポーネントです。 Visual Studio を入手するには、「[Visual Studio 2015 のダウンロード](http://go.microsoft.com/fwlink/p/?linkid=517106)」のページにアクセスして、Visual Studio 2015 with Update 2 以降をインストールしてください。  
  
##  <a name="InstallTheTools"></a> ツールのインストール  
 Visual Studio 2015 のインストーラーには、Visual C++ for Cross-Platform Mobile Development をインストールするオプションが含まれています。 このオプションを選択すると、必要な C++ 言語ツール、Visual Studio 用のテンプレートとコンポーネント、Android のビルドとデバッグに必要な GCC および Clang ツールセット、iOS 開発用の Mac と通信するためのコンポーネントがインストールされます。 また、iOS および Android アプリの開発をサポートするために必要なサードパーティ製のツールとソフトウェア開発キットもすべてインストールされます。 これらのサードパーティ製ツールのほとんどは、Android プラットフォームのサポートに必要なオープン ソースのソフトウェアです。  
  
-   Android Native Development Kit (NDK) は、Android プラットフォームを対象にした C++ コードをビルドする場合に必要になります。  
  
-   Android のビルド プロセスには、Android SDK、Apache Ant、および Java SE Development Kit が必要です。  
  
-   Microsoft Visual Studio Emulator for Android は、コードをテストおよびデバッグするのに役立つ、オプションの高パフォーマンス エミュレーターです。  
  
#### <a name="to-install-visual-c-for-cross-platform-mobile-development-and-the-third-party-tools"></a>Visual C++ for Cross-Platform Mobile Development とサードパーティ製ツールをインストールするには  
  
1.  「 [ツールの取得](#GetTheTools)」のリンクに従ってダウンロードした Visual Studio 2015 インストーラーを実行します。 オプションのコンポーネントをインストールするために、インストールの種類として **[カスタム]** を選びます。 **[次へ]** を選んで、インストールするオプションのコンポーネントを選びます。  
  
2.  [機能の選択] で、 **[クロス プラットフォームのモバイル開発]** を展開し、 **[Visual C++ モバイル開発]** を選択します。  
  
     ![[Visual C&#43;&#43; モバイル開発] を選択する](../cross-platform/media/cppmdd-install-vcmdd.png "CPPMDD_Install_VCMDD")  
  
     既定では、**[Visual C++ モバイル開発]** を選ぶと、**[プログラミング言語]** オプションは **[Visual C++]** をインストールするように設定され、**[共通ツールおよびソフトウェア開発キット]** オプションは必要なサード パーティ製コンポーネントをインストールするように設定されます。 必要な場合、その他のコンポーネントを選択することができます。 既定では、**[Microsoft Visual Studio Emulator for Android]** も選ばれます。 既にインストールされているコンポーネントは、一覧では非アクティブとして表示されます。  
  
     ユニバーサル Windows アプリをビルドし、Android および iOS プロジェクトとの間でコードを共有するには、**[機能の選択]** で、**[Windows 開発と Web 開発]** を展開し、**[ユニバーサル Windows アプリ開発ツール]** をオンにします。 ユニバーサル Windows アプリをビルドする予定がない場合は、このオプションを省略できます。  
  
     **[次へ]** を選択して続行します。  
  
3.  サードパーティ製コンポーネントには、それぞれ独自のライセンス条項があります。 ライセンス条項を表示するには、各コンポーネントの横にある **[ライセンス条項]** リンクを選びます。 **[インストール]** を選択して、コンポーネントを追加し、Visual Studio と、Visual C++ for Cross-Platform Mobile Development をインストールします。  
  
4.  インストールが完了したら、インストーラーを閉じて、コンピューターを再起動します。 サード パーティ製コンポーネントの一部の設定操作は、コンピューターを再起動するまで有効になりません。  
  
    > [!IMPORTANT]
    >  確実にすべてを正しくインストールするには、再起動する必要があります。  
  
     Microsoft Visual Studio Emulator for Android コンポーネントのインストールが失敗した場合は、お使いのコンピューターで Hyper-V が有効になっていない可能性があります。 **[Windows の機能の有効化または無効化]** コントロール パネル アプリを使って Hyper-V を有効にしてから、Visual Studio インストーラーをもう一度実行ます。  
  
    > [!NOTE]
    >  お使いのコンピューターまたは Windows のバージョンで Hyper-V がサポートされていない場合は、Microsoft Visual Studio Emulator for Android コンポーネントを使用できません。 Windows の Home エディションには、Hyper-V のサポートが含まれていません。  
  
5.  Visual Studio を開きます。 Visual Studio を実行するのが初めての場合は、構成してサインインするまでに時間がかかることがあります。 Visual Studio の準備が完了したら、 **[ツール]** メニューで **[拡張機能と更新プログラム]**、 **[更新プログラム]** の順に選びます。 Visual C++ for Cross-Platform Mobile Development または Microsoft Visual Studio Emulator for Android 用の利用可能な Visual Studio の更新プログラムがある場合は、それらをインストールします。  
  
##  <a name="InstallForiOS"></a> Install tools for iOS  
 Visual C++ for Cross-Platform Mobile Development を使用して、iOS コードを編集およびデバッグし、iOS シミュレーターまたは iOS デバイスに配置することができます。ただし、ライセンスの制限により、コードのビルドはリモートの Mac 上で行わなければなりません。 Visual Studio を使用して iOS アプリをビルドおよび実行するには、Mac 上にリモート エージェントをセットアップして構成する必要があります。 インストール方法、前提条件、構成オプションについて詳しくは、「 [Install And Configure Tools to Build using iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md)」をご覧ください。 iOS 用にビルドするのでない場合は、この手順を省略できます。  
  
##  <a name="ThirdParty"></a> 手動による依存関係のインストールまたは更新  
 Visual C++ のモバイル開発オプションをインストールする際に、サードパーティの 1 つ以上の依存関係を Visual Studio インストーラーでインストールしないことにした場合、それらの依存関係は、後で「 [Install the tools](#InstallTheTools)」の手順に従ってインストールできます。 また、Visual Studio とは別にインストールまたは更新することもできます。  
  
> [!CAUTION]
>  Java 以外の依存関係は、任意の順序でインストールできます。 JDK は、Android SDK をインストールする前にインストールして構成する必要があります。  
  
 次の情報を参照し、リンクを使用して、従属関係を手動でインストールします。  
  
- [Java SE 開発キット](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  
  
   既定では、インストーラーによって Java のツールが C:\Program Files (x86)\Java に格納されます。  
  
- [Android SDK](https://developer.android.com/sdk/index.html#Other)  
  
   インストール中に、推奨されたとおりに API を更新します。 最低でも Android 5.0 Lollipop (API レベル 21) の SDK がインストールされていることを確認します。 既定では、インストーラーによって Android SDK が C:\Program Files (x86)\Android\android-sdk に格納されます。  
  
   Android SDK ディレクトリにある SDK Manager アプリをもう一度実行すると、SDK を更新したり、オプション ツールや追加の API レベルをインストールしたりできます。 **[管理者として実行]** を使用して SDK Manager アプリを実行しなければ、更新のインストールが失敗する可能性があります。 Android アプリのビルドで問題が発生した場合は、SDK Manager を確認して、インストール済み SDK の更新プログラムの有無を調べてください。  
  
   Android SDK に付属している Android エミュレーターのいくつかを使用するには、オプションの Intel HAXM ドライバーをインストールする必要があります。 Intel HAXM ドライバーを正常にインストールするには、Windows から Hyper-V 機能を削除する必要がある場合があります。 Windows Phone エミュレーターおよび Microsoft Visual Studio Emulator for Android を使用するには、Hyper-V 機能を復元する必要があります。  
  
- [Android NDK](https://developer.android.com/tools/sdk/ndk/index.html)  
  
   既定では、インストーラーによって Android NDK が C:\ProgramData\Microsoft\AndroidNDK に格納されます。 Android NDK をもう一度ダウンロードしてインストールすると、NDK のインストールを更新できます。  
  
- [Apache Ant](http://ant.apache.org/bindownload.cgi)  
  
   既定では、インストーラーによって Apache Ant が C:\Program Files (x86)\Microsoft Visual Studio 14.0\Apps に格納されます。  
  
- [Microsoft Visual Studio Emulator for Android](http://go.microsoft.com/fwlink/p/?LinkId=536390)  
  
   Microsoft Visual Studio Emulator for Android は、Visual Studio ギャラリーからインストールおよび更新できます。  
  
  ほとんどの場合、Visual Studio によって、インストールしたサードパーティ製ソフトウェアの構成が検出され、内部環境変数にインストール パスが保持されます。 これらのクロス プラットフォーム開発ツールの既定のパスは、Visual Studio IDE でオーバーライドできます。  
  
#### <a name="to-set-the-paths-for-third-party-tools"></a>サード パーティのツールのパスを設定するには  
  
1.  Visual Studio のメニュー バーで、 **[ツール]**、 **[オプション]** の順に選びます。  
  
2.  **[オプション]** ダイアログ ボックスで、 **[クロス プラットフォーム]**、 **[C++]** の順に展開し、 **[Android]** を選びます。  
  
     ![Android ツールのパス オプション](../cross-platform/media/cppmdd-options-android.PNG "CPPMDD_Options_Android")  
  
3.  ツールが使用するパスを変更するには、パスの横にあるチェック ボックスをオンにして、テキスト ボックスでフォルダー パスを編集します。 参照ボタン (**...**) を使用して **[場所を選択]** ダイアログを開き、フォルダーを選ぶこともできます。  
  
4.  **[OK]** を選んで、カスタム ツール フォルダーの場所を保存します。  
  
## <a name="see-also"></a>関連項目  
 [iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)   
 [Visual C++ クロスプラットフォーム モバイル](https://www.visualstudio.com/explore/cplusplus-mdd-vs.aspx)
