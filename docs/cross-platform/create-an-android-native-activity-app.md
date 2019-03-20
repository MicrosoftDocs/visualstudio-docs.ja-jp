---
title: Android Native Activity アプリの作成 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: 884014b1-5208-45ec-b0da-ad0070d2c24d
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: fbe0942226e44e5ca2908f7c13f34595bef34887
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58069698"
---
# <a name="create-an-android-native-activity-app"></a>Android Native Activity アプリの作成

Visual C++ for Cross-Platform Mobile Development オプションをインストールすると、Visual Studio 2015 を使用して、フル機能を持つ Android Native Activity アプリを作成できます。 Android Native Development Kit (NDK) は、純粋な C/C++ コードを使用して Android アプリの大半を実装することを可能にするツールセットです。 いくつかの Java JNI コードはグルーとして機能し、C/C++ コードが Android とやり取りできるようにします。 Android NDK では、Android API レベル 9 を使用して Native Activity アプリを作成する機能が導入されました。 Native Activity コードは、Unreal Engine または OpenGL を使用したゲームやグラフィックス処理の多いアプリを作成できるので人気があります。 このトピックでは、OpenGL を使用した単純な Native Activity アプリの作成方法について説明します。 他のトピックでは、Native Activity コードの編集、ビルド、デバッグ、展開の開発ライフサイクルについて説明します。

## <a name="requirements"></a>要件

Android Native Activity アプリを作成する前に、すべてのシステム要件を満たし、Visual Studio 2015 の Visual C++ for Cross-Platform Mobile Development をインストールしていることを確認します。 詳細については、「 [Install Visual C++ for Cross-Platform Mobile Development](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)」を参照してください。 インストールに必要なサード パーティのツールと SDK が含まれていること、また Microsoft Visual Studio Emulator for Android がインストールされていることを確認してください。

## <a name="create-a-new-native-activity-project"></a>新しいネイティブ アクティビティ プロジェクトを作成する

このチュートリアルでは、まず新しい Android Native Activity プロジェクトを作成します。それから、既定のアプリを Visual Studio Emulator for Android でビルドして実行します。

1. Visual Studio で、**[ファイル]** > **[新規作成]** > **[プロジェクト]** の順に選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** で、**[Visual C++]** > **[クロス プラットフォーム]** の順に選択し、**[Native-Activity Application (Android)]** テンプレートを選択します。

3. アプリに `MyAndroidApp`などの名前を付け、 **[OK]**」を参照してください。

    ![Native Activity プロジェクトの作成](../cross-platform/media/cppmdd_newproject.PNG "CppMDD_NewProject")

    Visual Studio は新しいソリューションを作成し、ソリューション エクスプローラーを開きます。

    ![ソリューション エクスプローラーでの Native Activity プロジェクト](../cross-platform/media/cppmdd_rc_na_solutionexp.PNG "CPPMDD_RC_NA_SolutionExp")

   新しい Android Native Activity アプリのソリューションには、次の 2 つのプロジェクトが含まれています。

-   `MyAndroidApp.NativeActivity` には、アプリが Android 上でネイティブ アクティビティとして動作するための参照とグルー コードが含まれています。 グルー コードからのエントリ ポイントの実装は *main.cpp* にあります。 プリコンパイル済みヘッダーは *pch.h* にあります。 この Native Activity アプリ プロジェクトは、共有ライブラリ (*.so*) ファイルにコンパイルされ、Packaging プロジェクトで使用されます。

-   `MyAndroidApp.Packaging` は、Android デバイスまたはエミュレーターに配置する *.apk* ファイルを作成します。 これには、リソースと、マニフェスト プロパティを設定する *AndroidManifest.xml* ファイルが含まれています。 Ant のビルド プロセスを制御する *build.xml* ファイルも含まれています。 それは既定でスタートアップ プロジェクトとして設定されているため、Visual Studio から直接、配置して実行できます。

## <a name="build-and-run-the-default-android-native-activity-app"></a>既定の Android Native Activity アプリをビルドして実行する

テンプレートによって生成されたアプリをビルドして実行し、インストールとセットアップを確認します。 この初期テストでは、Visual Studio Emulator for Android によってインストールされるデバイス プロファイルのいずれかでアプリを実行します。 別の対象でアプリをテストする場合は、対象のエミュレーターを読み込むか、デバイスをコンピューターに接続してください。

## <a name="to-build-and-run-the-default-native-activity-app"></a>既定の Native Activity アプリをビルドして実行するには

1.  選択されていない場合は、 **[ソリューション プラットフォーム]** ドロップダウン リストから **[x86]** を選択します。

     ![ソリューション プラットフォーム ドロップダウン x86 の選択](../cross-platform/media/cppmdd_rc_na_solution_x86.png "CPPMDD_RC_NA_Solution_x86")

     **[ソリューション プラットフォーム]** リストが表示されない場合は、**[ボタンの追加と削除]** リストから **[ソリューション プラットフォーム]** を選択してから、使用するプラットフォームを選択します。

2.  メニュー バーで、**[ビルド]** > **[ソリューションのビルド]** の順にクリックします。

     ソリューションに含まれる 2 つのプロジェクトのビルド プロセスの出力が [出力] ウィンドウに表示されます。

3.  配置ターゲットとして、いずれかの VS Emulator Android Phone (x86) プロファイルを選択します。

     別のエミュレーターをインストールしてあるか、Android デバイスを接続してある場合は、配置対象のドロップダウン リストからそれらを選択できます。

4.  **F5** キーを押してデバッグを開始するか、Shift + F5 キーを押してデバッグなしで開始します。

     Visual Studio Emulator for Android で、既定のアプリは次のようになります。

     ![アプリを実行するエミュレーター](../cross-platform/media/cppmdd_emulator_running_app.PNG "CppMDD_Emulator_Running_App")

     Visual Studio によってエミュレーターが起動されます。コードを読み込んで配置するのに数秒かかります。 アプリが開始されると、ブレークポイントの設定や、デバッガーを使用したステップ実行、ローカルの確認、値のウォッチができるようになります。

5.  **Shift** + **F5** キーを押してデバッグを停止します。

     エミュレーターは実行され続ける独立したプロセスです。 同じエミュレーターに対して、コードを何度も編集、コンパイル、配置できます。