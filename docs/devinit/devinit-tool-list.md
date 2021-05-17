---
title: 使用可能なツール
description: 開発環境のカスタマイズに使用できるすべての devinit ツールの一覧。
ms.date: 02/08/2021
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 482e838edf47d63235f60f013bd18eff586f83e8
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635332"
---
# <a name="available-tools"></a>使用可能なツール

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

次の表に、devinit で現在使用できるツールの一覧を示します。

| ツール                                                                                             | 説明                                                                                                 |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| [**azurecli-login**](tool-azurecli-login.md)                                                     | Azure CLI コマンド `az login --device-code` を実行するツール。                                             |
| [**choco-install**](tool-choco-install.md)                                                       | chocolatey パッケージをインストールするツール。                                                                        |
| [**choco-upgrade**](tool-choco-upgrade.md)                                                       | chocolatey パッケージをアップグレードするツール。                                                                        |
| [**dotnet-restore**](tool-dotnet-restore.md)                                                     | .NET プロジェクトの依存関係とツールを復元するツール。                                               |
| [**dotnet-toolinstall**](tool-dotnet-toolinstall.md)                                             | .NET Core ツールをインストールするツール (たとえば、 dotnet-ef)                                                |
| [**enable-iis**](tool-enable-iis.md)                                                             | IIS の機能を有効にし、最新の ASP.NET ホスティング バンドルをインストールするツール。                                  |
| [**msi-install**](tool-msi-install.md)                                                           | パスまたは URL を指定して MSI ファイルをインストールするツール。                                                              |
| [**npm-install**](tool-npm-install.md)                                                           | NPM パッケージをインストールするツール。                                                                               |
| [**nuget-restore**](tool-nuget-restore.md)                                                       | NuGet パッケージを復元するツール。                                                                         |
| [**require-azureartifactscredentialprovider**](tool-require-azureartifactscredentialprovider.md) | Azure Artifacts 資格情報プロバイダーをインストールします。                                                           |
| [**require-azurecli**](tool-require-azurecli.md)                                                 | Azure CLI をインストールするツール。                                                                              |
| [**require-dotnetcoresdk**](tool-require-dotnetcoresdk.md)                                       | .NET Core SDK と共有ランタイムをインストールするツール。                                                       |
| [**require-dotnetframeworksdk**](tool-require-dotnetframeworksdk.md)                             | .NET Framework SDK をインストールするツール。                                                                     |
| [**require-mssql**](tool-require-mssql.md)                                                       | MS SQL Server 2019 をインストールするツール。                                                                         |
| [**require-nodejs**](tool-require-nodejs.md)                                                     | Nodejs と NPM をインストールするツール。                                                                             |
| [**require-nuget**](tool-require-nuget.md)                                                       | NuGet をインストールするツール。                                                                                      |
| [**require-npm**](tool-require-npm.md)                                                           | NPM をインストールするツール。                                                                                        |
| [**require-psmodule**](tool-require-psmodule.md)                                                 | ギャラリーから PowerShell モジュールをインストールするツール。                                                        |
| [**require-vcpkg**](tool-require-vcpkg.md)                                                       | vcpkg をインストールするツール。                                                                                      |
| [**require-vscomponent**](tool-require-vscomponent.md)                                           | `.vsconfig` ファイルに基づいて VS のインストールを変更するツール。                                                |
| [**require-winget**](tool-require-winget.md)                                                     | winget をインストールするツール。                                                                                     |
| [**windowsfeature-enable**](tool-windowsfeature-enable.md)                                       | Windows の機能を有効にするツール セット。                                                                           |
| [**windowsfeature-disable**](tool-windowsfeature-disable.md)                                     | Windows の機能を無効にするツール セット。                                                                          |
| [**windowsfeature-list**](tool-windowsfeature-list.md)                                           | すべての Windows 機能の有効/無効の状態を一覧表示するツール。                                              |
| [**set-env**](tool-set-env.md)                                                                   | 環境変数を表示および設定するツール。                                                                 |
| [**vcpkg-install**](tool-vcpkg-install.md)                                                       | vcpkg を使用してパッケージをインストールするツール。                                                                         |
| [**winget-install**](tool-winget-install.md)                                                     | winget を使用してパッケージをインストールするツール。                                                                        |
| [**wsl-install**](tool-wsl-install.md)                                                           | Linux 用 Windows サブシステム向けの Linux ディストリビューションをインストールして構成するツール。                             |
