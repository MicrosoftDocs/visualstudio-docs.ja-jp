---
title: UWP アプリのアプリケーション プロパティ ページ
ms.date: 01/23/2018
ms.topic: reference
f1_keywords:
- AppPackage.Properties.Application
helpviewer_keywords:
- Application page [UWP project]
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 416661a39f54429f24cca66a0ec1be7b6c87629d
ms.sourcegitcommit: 87d7123c09812534b7b08743de4d11d6433eaa13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57222715"
---
# <a name="application-property-page-uwp-projects"></a>アプリケーション プロパティ ページ (UWP プロジェクト)

**[アプリケーション]** プロパティ ページを使用して、ユニバーサル Windows プラットフォーム (UWP) プロジェクトのアセンブリとパッケージの情報、およびターゲットの Windows 10 バージョンを指定します。

![アプリケーション プロパティ ページ](media/application-page-uwp.png)

**[アプリケーション]** ページにアクセスするには、**ソリューション エクスプローラー**のプロジェクト ノードを選択します。 その後、メニュー バーで **[プロジェクト]**  >  **[プロパティ]** を選択します。 **[アプリケーション]** タブで、プロパティ ページが開きます。

## <a name="general-section"></a>[全般] セクション

**アセンブリ マニフェスト**&mdash;アセンブリ マニフェストを保持する出力ファイルの名前を指定します。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.AssemblyName%2A>」を参照してください。

**既定の名前空間**&mdash;プロジェクトに追加されるファイルの基本の名前空間を指定します。 名前空間の詳細については、「[名前空間 (C# プログラミング ガイド)](/dotnet/csharp/programming-guide/namespaces/)」、「[名前空間 (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/namespaces)」、または「[名前空間 (C++)](/cpp/cpp/namespaces-cpp)」を参照してください。

プログラムを使用してこのプロパティにアクセスする方法については、「<xref:VSLangProj.ProjectProperties.RootNamespace%2A>」を参照してください。

**アセンブリ情報**&mdash;このボタンをクリックすると、[[アセンブリ情報] ダイアログ ボックス](../../ide/reference/assembly-information-dialog-box.md)が表示されます。

**パッケージ マニフェスト**&mdash;このボタンを選択すると、マニフェスト デザイナーが表示されます。 マニフェスト デザイナーには、**ソリューション エクスプローラー**で _Package.appxmanifest_ ファイルを選択して、アクセスすることもできます。 詳細については、「[マニフェスト デザイナーを使ってパッケージを構成する](/windows/uwp/packaging/packaging-uwp-apps#configure-an-app-package)」を参照してください。

## <a name="targeting-section"></a>[ターゲット] セクション

このセクションのドロップダウン リストを使用して、自分のアプリに対して Windows 10 のターゲット バージョンと最小バージョンを設定できます。 エンタープライズ アプリを開発している場合、古い最小バージョンもサポートする、最新バージョンの Windows 10 をターゲットにすることをお勧めします。 選択する Windows 10 のバージョンの詳細については、「[UWP バージョンの選択](/windows/uwp/updates-and-versions/choose-a-uwp-version)」を参照してください。

Visual Studio のプラットフォーム ターゲットの詳細については、「[対象となるプラットフォーム](/visualstudio/productinfo/vs2017-compatibility-vs#platform-targeting)」を参照してください。

## <a name="see-also"></a>関連項目

- [初めてのアプリの作成](/windows/uwp/get-started/your-first-app)
- [UWP バージョンの選択](/windows/uwp/updates-and-versions/choose-a-uwp-version)