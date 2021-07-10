---
title: 複数バージョンの Visual Studio をインストールする
description: 以前のバージョンまたは最新バージョンの Visual Studio が既にインストールされたコンピューターに Visual Studio をインストールする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/29/2021
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: j-martens
ms.author: jmartens
manager: jmartens
ms.openlocfilehash: c8d1da5f8cb5c237fe02a41197825d5086fc6471
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307022"
---
# <a name="install-visual-studio-versions-side-by-side"></a>複数バージョンの Visual Studio をインストールする

Visual Studio は、以前のバージョンまたは最新バージョンの Visual Studio が既にインストールされたコンピューターにもインストールできます。

::: moniker range="vs-2017"

複数のバージョンを並行してインストールする前に、次の条件を確認してください。

* Visual Studio 2015 で作成されたソリューションを Visual Studio 2017 を使用して開く場合、Visual Studio 2017 に固有の機能が実装されていない限り、後で以前のバージョンのソリューションを開き、再度変更することができます。

* Visual Studio 2015 以前のバージョンで作成されたソリューションを Visual Studio 2017 を使用して開こうとする場合、ご利用のプロジェクトとファイルを Visual Studio 2017 に対応するように変更することが必要な場合があります。 詳細については、[Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true)に関するページを参照してください。

::: moniker-end

::: moniker range="vs-2019"

複数のバージョンを並行してインストールする前に、次の条件を確認してください。

* Visual Studio 2017 で作成されたソリューションを Visual Studio 2019 を使用して開く場合、Visual Studio 2019 に固有の機能が実装されていない限り、後で以前のバージョンのソリューションを開き、再度変更することができます。

* Visual Studio 2017 以前のバージョンで作成されたソリューションを Visual Studio 2019 を使用して開こうとする場合、ご利用のプロジェクトとファイルを Visual Studio 2019 に対応するように変更することが必要な場合があります。 詳細については、[Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)に関するページを参照してください。

::: moniker-end

::: moniker range=">=vs-2022"

複数のバージョンを並行してインストールする前に、次の条件を確認してください。

* Visual Studio 2017 または Visual Studio 2019 で作成されたソリューションを Visual Studio 2022 を使用して開く場合、Visual Studio 2022 に固有の機能が実装されていない限り、後で以前のバージョンのソリューションを開き、再度変更することができます。

* Visual Studio 2019 以前のバージョンで作成されたソリューションを Visual Studio 2022 を使用して開こうとする場合、ご利用のプロジェクトとファイルを Visual Studio 2022 に対応するように変更することが必要な場合があります。 詳細については、[Visual Studio プロジェクトの移植、移行、およびアップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)に関するページを参照してください。

::: moniker-end

* 複数のバージョンの Visual Studio がコンピューターにインストールされている場合、そのうちの 1 つのバージョンをアンインストールすると、すべてのバージョンの Visual Studio のファイルの関連付けが削除されます。

* すべての拡張機能に互換性があるわけではないので、Visual Studio は拡張機能を自動的にアップグレードしません。 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) またはソフトウェア発行者から入手した拡張機能を再インストールする必要があります。

## <a name="install-minor-visual-studio-versions-side-by-side"></a>複数のマイナー バージョンの Visual Studio をサイドバイサイドでインストールする

Visual Studio のあるマイナー バージョンから次のバージョンにアップグレードする場合、既定では、Visual Studio インストーラーによって、現在のインストールがそのチャネルの最新のバージョンに更新されます。 たとえば、16.9.4 がちょうどリリースされたとします。 インストーラーによって、現在のインストール 16.9.3 (以前) と 16.9.4 の置換が試行されます。どちらのバージョンも [Visual Studio 2019 リリース チャネル](/visualstudio/productinfo/release-rhythm)に含まれるためです。 更新中、新しいリリースが古いリリースに取って代わることで、古いバージョンの Visual Studio によりコンピューター上の領域が占められないようになります。 ただし、Visual Studio のマイナー リリース バージョンを複数、並列インストールしておくと便利な場合もあります。 たとえば、16.9.3 と16.9.4 の両方を同じコンピューター上にインストールします。

::: moniker range="vs-2017"

1. 既存の Visual Studio バージョンと並列インストールするバージョンのために、[Visual Studio の以前のバージョン](https://visualstudio.microsoft.com/vs/older-downloads/)のページから、Visual Studio 2017 バージョン 15.9 の最新ブートストラップをダウンロードします。

1. 管理者モードでコマンド プロンプトを開きます。 これを行うには、Windows のスタート メニューを開き、「cmd」と入力し、コマンド プロンプトの検索結果を右クリックし、 **[管理者として実行]** を選択します。 コマンド プロンプトで、Visual Studio ブートストラップ ファイルが配置されているフォルダーにディレクトリを変更します。

1. 次のコマンドを実行して、インストール場所に新しいフォルダーのパスを指定し、.exe ファイル名を、インストールするバージョンの Visual Studio の適切なブートストラップ名に置き換えます。 .exe ファイル名は、以下のファイルと同じか、同様の名前にすることをお勧めします。

   * Visual Studio Enterprise の場合は vs_enterprise.exe
   * Visual Studio Professional の場合は vs_professional.exe

1. インストーラーのダイアログに従って、インストールに必要なコンポーネントを選択します。 詳細については、「[Visual Studio のインストール](install-visual-studio.md#step-4---choose-workloads)」を参照してください。

::: moniker-end

::: moniker range="vs-2019"

1. 既存の Visual Studio バージョンと並列インストールするマイナー バージョンのために、[Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/downloads)または [Visual Studio 2019 リリース](/visualstudio/releases/2019/history#installing-an-earlier-release) ページから、Visual Studio 2019 ブートストラップ ファイルをダウンロードします。

1. 管理者モードでコマンド プロンプトを開きます。 これを行うには、Windows のスタート メニューを開き、「cmd」と入力し、コマンド プロンプトの検索結果を右クリックし、 **[管理者として実行]** を選択します。 コマンド プロンプトで、Visual Studio ブートストラップ ファイルが配置されているフォルダーにディレクトリを変更します。

1. 次のコマンドを実行して、インストール場所に新しいフォルダーのパスを指定し、.exe ファイル名を、インストールするバージョンの Visual Studio の適切なブートストラップ名に置き換えます。 .exe ファイル名は、以下のファイルと同じか、同様の名前にすることをお勧めします。

   * Visual Studio Enterprise の場合は vs_enterprise.exe
   * Visual Studio Professional の場合は vs_professional.exe
   * Visual Studio Community の場合は vs_community.exe

   ```shell
   vs_Enterprise.exe --installPath "C:\Program Files (x86)\Microsoft Visual Studio\<AddNewPath>"
   ```

1. インストーラーのダイアログに従って、インストールに必要なコンポーネントを選択します。 詳細については、「[Visual Studio のインストール](install-visual-studio.md#step-4---choose-workloads)」を参照してください。

::: moniker-end

::: moniker range=">=vs-2022"

1. 既存の Visual Studio バージョンと並列インストールするマイナー バージョンのために、[Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/downloads)または [Visual Studio 2022 リリース](/visualstudio/releases/2022/history) ページから、Visual Studio 2022 ブートストラップ ファイルをダウンロードします。

1. 管理者モードでコマンド プロンプトを開きます。 これを行うには、Windows のスタート メニューを開き、「cmd」と入力し、コマンド プロンプトの検索結果を右クリックし、 **[管理者として実行]** を選択します。 コマンド プロンプトで、Visual Studio ブートストラップ ファイルが配置されているフォルダーにディレクトリを変更します。

1. 次のコマンドを実行して、インストール場所に新しいフォルダーのパスを指定し、.exe ファイル名を、インストールするバージョンの Visual Studio の適切なブートストラップ名に置き換えます。 .exe ファイル名は、以下のファイルと同じか、同様の名前にすることをお勧めします。

   * Visual Studio Enterprise の場合は vs_enterprise.exe
   * Visual Studio Professional の場合は vs_professional.exe
   * Visual Studio Community の場合は vs_community.exe

   ```shell
   vs_Enterprise.exe --installPath "C:\Program Files\Microsoft Visual Studio\<AddNewPath>"
   ```

1. インストーラーのダイアログに従って、インストールに必要なコンポーネントを選択します。 詳細については、「[Visual Studio のインストール](install-visual-studio.md#step-4---choose-workloads)」を参照してください。
   
::: moniker-end

## <a name="net-framework-versions-and-side-by-side-installations"></a>.NET Framework のバージョンと複数バージョンのインストール

Visual Basic、Visual C#、および Visual F# のプロジェクトでは、**プロジェクト デザイナー** の **[ターゲット フレームワーク]** オプションを使用して、プロジェクトで使用する .NET Framework のバージョンを指定します。 C++ プロジェクトでは、.vcxproj ファイルを変更すると、ターゲット フレームワークを手動で変更できます。 詳細については、「[.NET Framework のバージョンの互換性](/dotnet/framework/migration-guide/version-compatibility)」ページを参照してください。

プロジェクトを作成するときは、プロジェクトが対象とする .NET Framework のバージョンを **[新しいプロジェクト]** ダイアログ ボックスの **[.NET Framework]** の一覧で指定できます。

言語固有の情報については、次の表の適切なトピックを参照してください。

::: moniker range="vs-2017"

| 言語     | トピック                                                                                                                                                   |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Basic | [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md?view=vs-2017&preserve-view=true) |
| Visual C#    | [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md?view=vs-2017&preserve-view=true)                 |
| Visual F#    | [Visual Studio で Visual F# を使用して開発する](../ide/fsharp-visual-studio.md?view=vs-2017&preserve-view=true)                                               |
| C++          | [方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/)                         |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md?view=vs-2017&preserve-view=true)
* [Visual Studio プロジェクトのポート、移行、アップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true)
* [C/C++ 分離アプリケーションおよび side-by-side アセンブリのビルド](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end

::: moniker range=">= vs-2019"

| 言語     | トピック                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------|
| Visual Basic | [[アプリケーション] ページ (プロジェクト デザイナー)](../ide/reference/application-page-project-designer-visual-basic.md)         |
| Visual C#    | [[アプリケーション] ページ (プロジェクト デザイナー) (C#)](../ide/reference/application-page-project-designer-csharp.md)                         |
| Visual F#    | [Visual Studio で Visual F# を使用して開発する](../ide/fsharp-visual-studio.md)                                                       |
| C++          | [方法: ターゲット フレームワークおよびプラットフォームのツールセットを変更する](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio プロジェクトのポート、移行、アップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
* [C/C++ 分離アプリケーションおよび side-by-side アセンブリのビルド](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end
