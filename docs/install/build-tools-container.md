---
title: Visual Studio Build Tools をコンテナーにインストールする
titleSuffix: ''
description: Visual Studio Build Tools を Windows コンテナーにインストールして、継続的インテグレーションと継続的デリバリー (CI/CD) のワークフローをサポートする方法を説明します。
ms.date: 03/25/2020
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: d5c038e2-e70d-411e-950c-8a54917b578a
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e29e780d146fec63bc1375ed16f72067f9b4ccee
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307636"
---
# <a name="install-build-tools-into-a-container"></a>Build Tools をコンテナーにインストールする

Visual Studio Build Tools を Windows コンテナーにインストールして、継続的インテグレーションと継続的デリバリー (CI/CD) のワークフローをサポートできます。 この記事では、必要な Docker 構成の変更と、コンテナーにインストールできる[ワークロードとコンポーネント](workload-component-id-vs-build-tools.md)について説明します。

[コンテナー](https://www.docker.com/what-container)は一貫性のあるビルド システムをパッケージ化する優れた手段であり、CI/CD サーバー環境でだけでなく、開発環境でも使うことができます。 たとえば、カスタマイズされた環境でビルドされるようにコンテナーにソース コードをマウントしながら、Visual Studio や他のツールを使って引き続きコードを記述することができます。 お使いの CI/CD ワークフローが同じコンテナー イメージを使っている場合、コードのビルドの一貫性を心配する必要はありません。 実行時の一貫性を保つためにコンテナーを使うこともでき、これはオーケストレーション システムで複数のコンテナーを使っているマイクロサービスでは一般的なことですが、この記事ではそれについては説明しません。

ご自分のソース コードのビルドに必要な機能が Visual Studio Build Tools にない場合は、他の Visual Studio 製品に対して同じ手順を使うことができます。 ただし、Windows コンテナーは対話型のユーザー インターフェイスをサポートしていないため、すべてのコマンドを自動化する必要があることに注意してください。

## <a name="before-you-begin"></a>始める前に

以下では、[Docker](https://www.docker.com/what-docker) に関するある程度の知識をお持ちであることが想定されています。 Windows 上での Docker の実行にまだ慣れていない場合は、[Windows 上での Docker エンジンのインストールと構成](/virtualization/windowscontainers/manage-docker/configure-docker-daemon)方法をご確認ください。

以下の基本イメージはサンプルであり、お客様のシステムでは機能しない場合があります。 ご自身の環境に対してどの基本イメージを使うべきか判断するには、「[Windows コンテナーバージョンの互換性](/virtualization/windowscontainers/deploy-containers/version-compatibility)」をご覧ください。

## <a name="create-and-build-the-dockerfile"></a>Dockerfile を作成してビルドする

次の Dockerfile の例を新しいファイルとしてディスクに保存します。 ファイル名を単に "Dockerfile" にすると、既定で認識されます。

> [!WARNING]
> この例の Dockerfile では、コンテナーにインストールできない以前の Windows SDK のみを除外します。 以前のリリースはビルド コマンドが失敗する原因になります。

1. コマンド プロンプトを開きます。

1. 新しいディレクトリを作成します (推奨)。

   ```shell
   mkdir C:\BuildTools
   ```

1. この新しいディレクトリに移動します。

   ```shell
   cd C:\BuildTools
   ```

1. 次の内容を C:\BuildTools\Dockerfile に保存します。
 
   ::: moniker range="vs-2017"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.7.2.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   RUN `
       # Download the Build Tools bootstrapper.
       curl -SL --output vs_buildtools.exe https://aka.ms/vs/15/release/vs_buildtools.exe `
       `
       # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
       && (start /w vs_buildtools.exe --quiet --wait --norestart --nocache `
           --installPath C:\BuildTools `
           --add Microsoft.VisualStudio.Workload.AzureBuildTools `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
           --remove Microsoft.VisualStudio.Component.Windows81SDK `
           || IF "%ERRORLEVEL%"=="3010" EXIT 0) `
       `
       # Cleanup
       && del /q vs_buildtools.exe

   # Define the entry point for the Docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > ワークロードとコンポーネントの一覧については、「[Visual Studio Build Tools のコンポーネント ディレクトリ](workload-component-id-vs-build-tools.md)」を参照してください。
   >

   > [!WARNING]
   > 自分のイメージを microsoft/windowsservercore または mcr.microsoft.com/windows/servercore に直接基づくようにする場合 ([Microsoft によるコンテナー カタログのシンジケート](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/)に関するページを参照)、.NET Framework が正しくインストールされない可能性があり、インストール エラーは示されません。 インストールが完了した後、マネージド コードが実行されない可能性があります。 代わりに、イメージを [microsoft/dotnet-framework:4.7.2](https://hub.docker.com/r/microsoft/dotnet-framework) 以降に基づくようにします。 また、バージョン 4.7.2 以降のタグが付いたイメージでは、既定の `SHELL` として PowerShell が使用されている可能性があり、その場合 `RUN` および `ENTRYPOINT` 命令は失敗することに注意してください。
   >
   > Visual Studio 2017 バージョン 15.8 以前 (すべての製品) は、mcr.microsoft.com/windows/servercore:1809 以降には適切にインストールされません。 エラーは表示されません。
   >
   > どのコンテナー OS バージョンがどのホスト OS バージョン上でサポートされているかについては「[Windows コンテナーのバージョンの互換性](/virtualization/windowscontainers/deploy-containers/version-compatibility)」を、既知の問題については「[コンテナーの既知の問題](build-tools-container-issues.md)」をご覧ください。
   
   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.8.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   RUN `
       # Download the Build Tools bootstrapper.
       curl -SL --output vs_buildtools.exe https://aka.ms/vs/16/release/vs_buildtools.exe `
       `
       # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
       && (start /w vs_buildtools.exe --quiet --wait --norestart --nocache modify `
           --installPath "%ProgramFiles(x86)%\Microsoft Visual Studio\2019\BuildTools" `
           --add Microsoft.VisualStudio.Workload.AzureBuildTools `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
           --remove Microsoft.VisualStudio.Component.Windows81SDK `
           || IF "%ERRORLEVEL%"=="3010" EXIT 0) `
       `
       # Cleanup
       && del /q vs_buildtools.exe

   # Define the entry point for the docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > ワークロードとコンポーネントの一覧については、「[Visual Studio Build Tools のコンポーネント ディレクトリ](workload-component-id-vs-build-tools.md)」を参照してください。
   >

   > [!WARNING]
   > microsoft/windowsservercore に直接基づくイメージの場合は、.NET Framework が正しくインストールされない可能性があり、インストール エラーは示されていません。 インストールが完了した後、マネージド コードが実行されない可能性があります。 代わりに、イメージを [microsoft/dotnet-framework:4.8](https://hub.docker.com/r/microsoft/dotnet-framework) 以降に基づくようにします。 また、バージョン 4.8 以降のタグが付いたイメージでは、既定の `SHELL` として PowerShell が使用されている可能性があり、その場合 `RUN` および `ENTRYPOINT` 命令は失敗することに注意してください。
   >
   > どのコンテナー OS バージョンがどのホスト OS バージョン上でサポートされているかについては「[Windows コンテナーのバージョンの互換性](/virtualization/windowscontainers/deploy-containers/version-compatibility)」を、既知の問題については「[コンテナーの既知の問題](build-tools-container-issues.md)」をご覧ください。

   ::: moniker-end
   
   > [!NOTE]
   > エラー コード `3010` は、再起動が必要な成功を示すために使用されます。詳細については、[MsiExec.exe のエラー メッセージ](/windows/win32/msi/error-codes)に関する記事を参照してください。

1. そのディレクトリで次のコマンドを実行します。

   ::: moniker range="vs-2017"

   ```shell
   docker build -t buildtools2017:latest -m 2GB .
   ```

   このコマンドは、2 GB のメモリを使って現在のディレクトリに Dockerfile をビルドします。 ワークロードを何かインストールするときは、既定の 1 GB では不十分です。ただし、ビルドの要件によっては、1 GB のメモリだけでもビルドできる場合があります。

   最後のイメージには "buildtools2017:latest" というタグが付きます。"latest" タグはタグが指定されていない場合の既定値なので、コンテナー内では "buildtools2017" として簡単に実行できます。 さらに[高度なシナリオ](advanced-build-tools-container.md)で特定のバージョンの Visual Studio Build Tools 2017 を使いたい場合は、"latest" 意外にも特定の Visual Studio ビルド番号でコンテナーにタグを付けて、コンテナーが特定のバージョンを一貫して使用できるようにします。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ```shell
   docker build -t buildtools2019:latest -m 2GB .
   ```

   このコマンドは、2 GB のメモリを使って現在のディレクトリに Dockerfile をビルドします。 ワークロードを何かインストールするときは、既定の 1 GB では不十分です。ただし、ビルドの要件によっては、1 GB のメモリだけでもビルドできる場合があります。

   最後のイメージには "buildtools2019:latest" というタグが付きます。"latest" タグはタグが指定されていない場合の既定値なので、コンテナー内では "buildtools2019" として簡単に実行できます。 さらに[高度なシナリオ](advanced-build-tools-container.md)で特定のバージョンの Visual Studio Build Tools 2019 を使いたい場合は、"latest" 意外にも特定の Visual Studio ビルド番号でコンテナーにタグを付けて、コンテナーが特定のバージョンを一貫して使用できるようにできます。

   ::: moniker-end

## <a name="using-the-built-image"></a>ビルドされたイメージを使う

イメージができたので、それをコンテナーで実行して対話型と自動の両方のビルドを行うことができます。 この例では開発者コマンド プロンプトを使うので、PATH および他の環境変数は既に構成されています。

1. コマンド プロンプトを開きます。

1. コンテナーを実行し、すべての開発者環境変数が設定された状態で PowerShell 環境を開始します。

   ::: moniker range="vs-2017"

   ```shell
   docker run -it buildtools2017
   ```

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ```shell
   docker run -it buildtools2019
   ```

   ::: moniker-end

このイメージを CI/CD ワークフローで使うには、独自の [Azure Container Registry](https://azure.microsoft.com/services/container-registry) または他の内部 [Docker レジストリ](https://docs.docker.com/registry/deploying)に発行して、サーバーがそれを取得するだけで済むようにします。

   > [!NOTE]
   > Docker コンテナーを起動できない場合は、Visual Studio のインストールに問題がある可能性があります。 Dockerfile を更新して、Visual Studio のバッチ コマンドを呼び出すステップを削除できます。 これにより、Docker コンテナーを起動し、インストールのエラー ログを読み取ることができます。
   >
   > Dockerfile ファイルで、`ENTRYPOINT` コマンドから `C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat` と `&&` パラメーターを削除します。 コマンドは `ENTRYPOINT ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]` のようになります。 次に、Dockerfile をリビルドし、`run` コマンドを実行してコンテナー ファイルにアクセスします。 インストールのエラー ログを見つけるには、`$env:TEMP` ディレクトリに移動し、`dd_setup_<timestamp>_errors.log` ファイルを見つけます。
   >
   > インストールの問題を特定して修正したら、`C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat` と `&&` パラメーターを `ENTRYPOINT` コマンドに追加して戻し、Dockerfile をリビルドできます。
   >
   > 詳細については、「[コンテナーの既知の問題](build-tools-container-issues.md)」をご覧ください。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [コンテナーの高度な例](advanced-build-tools-container.md)
* [コンテナーの既知の問題](build-tools-container-issues.md)
* [Visual Studio Build Tools のワークロード ID とコンポーネント ID](workload-component-id-vs-build-tools.md)
