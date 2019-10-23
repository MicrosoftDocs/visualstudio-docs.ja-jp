---
title: 管理者として実行
ms.date: 06/05/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, user permissions
- user permissions
- administrative privileges
- permissions
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6086485ef20330de7971297f52a112d5183ee4a2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72647347"
---
# <a name="user-permissions-and-visual-studio"></a>ユーザー アクセス許可と Visual Studio

セキュリティ上の理由により、Visual Studio はできる限り通常のユーザーとして実行してください。

> [!WARNING]
> また、信頼できる人または信頼できる場所以外から入手した Visual Studio ソリューションをコンパイル、起動、またはデバッグしないでください。

Visual Studio IDE のほぼすべての機能は、通常のユーザーとして実行できます。 次のタスクを完了するには、管理者アクセス許可が必要です。

|区分|タスク|詳細情報|
|----------|----------| - |
|インストール|Visual Studio をインストールする。|[Visual Studio のインストール](../install/install-visual-studio.md)|
||ローカル ヘルプ コンテンツをインストール、更新、または削除する。|[ローカル ヘルプ コンテンツのインストールと管理](../help-viewer/install-manage-local-content.md)|
|ツールボックス|**ツールボックス**にクラシック COM コントロールを追加する。|[ツールボックス](../ide/reference/toolbox.md)|
|ビルド|コンポーネントを登録するビルド後のイベントを使用する。|[カスタム ビルド ステップとビルド イベントについて](/cpp/build/understanding-custom-build-steps-and-build-events)|
||C++ プロジェクトのビルド時に登録手順を含める。||
|デバッグ|昇格されたアクセス許可で実行されたアプリケーションをデバッグする。|[デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)|
||ASP.NET Web サイトなど、別のユーザー アカウントで実行されたアプリケーションをデバッグする。|[ASP.NET アプリケーションおよび AJAX アプリケーションのデバッグ](../debugger/how-to-enable-debugging-for-aspnet-applications.md)|
||XAML ブラウザー アプリケーション (XBAP) をゾーンでデバッグする。|[WPF ホスト (PresentationHost.exe)](/dotnet/framework/wpf/app-development/wpf-host-presentationhost-exe)|
||エミュレーターを使用して、Microsoft Azure クラウド サービス プロジェクトをデバッグする。|[Visual Studio でのクラウド サービスのデバッグ](/azure/vs-azure-tools-debug-cloud-services-virtual-machines)|
||リモート デバッグ用にファイアウォールを構成する。|[リモート デバッグ](../debugger/remote-debugging.md)|
|パフォーマンス ツール|昇格されたアプリケーションにアタッチする。|[パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-performance-profiling.md)|
||GPU プロファイラーを使用する。|[GPU プロファイル](../profiling/gpu-usage.md)|
|配置|ローカル コンピューターでインターネット インフォメーション サービス (IIS) に Web アプリケーションを配置する。|[Visual Studio を使用して ASP.NET Core Web アプリを配置する](/aspnet/web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/)|

## <a name="run-visual-studio-as-an-administrator"></a>Visual Studio を管理者として実行する

Visual Studio を管理者として実行する必要がある場合は、次の手順に従って IDE を開きます。

> [!NOTE]
> ここで説明する手順は Windows 10 用です。 これらの手順は、Windows のその他のバージョンの場合と似ています。

::: moniker range="vs-2017"

1. **[スタート]** メニューを開き、Visual Studio 2017 にスクロールします。

1. 右クリックして、つまり **Visual Studio 2017** のコンテキスト メニューから **[その他]** > **[管理者として実行]** を選択します。

   Visual Studio の起動時には、 **[(管理者)]** がタイトル バーの製品名の後に表示されます。

::: moniker-end

::: moniker range=">=vs-2019"

1. **[スタート]** メニューを開き、Visual Studio 2019 にスクロールします。

1. 右クリックして、つまり **Visual Studio 2019** のコンテキスト メニューから **[その他]** > **[管理者として実行]** を選択します。

   Visual Studio の起動時には、 **[(管理者)]** がタイトル バーの製品名の後に表示されます。

::: moniker-end

アプリケーションのショートカットを変更して、常に管理者アクセス許可で実行することもできます。

## <a name="see-also"></a>関連項目

- [Visual Studio プロジェクトのポート、移行、アップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [Visual Studio のインストール](../install/install-visual-studio.md)