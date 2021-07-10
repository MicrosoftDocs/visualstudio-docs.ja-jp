---
title: コンテナーの既知の問題
description: Windows コンテナーに Visual Studio Build Tools をインストールするときに発生する可能性がある既知の問題について説明します。
ms.date: 02/18/2020
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 140083f1-05bc-4014-949e-fb5802397c7a
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: a56d820805fa97f3672480c063ebfcc0fdc96fb6
ms.sourcegitcommit: 0499d813d5c24052c970ca15373d556a69507250
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2021
ms.locfileid: "113046093"
---
# <a name="known-issues-for-containers"></a>コンテナーの既知の問題

Docker コンテナーに Visual Studio をインストールする場合、いくつかの問題があります。

## <a name="windows-container"></a>Windows コンテナー

Windows コンテナーに Visual Studio Build Tools をインストールすると、以下の既知の問題が発生します。

::: moniker range="vs-2017"

* Visual Studio は、mcr.microsoft.com/windows/servercore:10.0.14393.1593 のイメージに基づくコンテナーにはインストールできません。 10.0.14393 より前または後の Windows バージョンでタグ付けされたイメージでは動作します。

* 10.0.14393 以前の Windows SDK バージョンをインストールすることはできません。 一部のパッケージはインストールに失敗し、そのようなパッケージに依存するワークロードは動作しません。

::: moniker-end

* イメージを構築するときに `-m 2GB` (またはそれ以上) を渡します。 一部のワークロードではインストール時の既定の 1 GB よりも多くのメモリを必要とします。
* Docker で既定の 20 GB よりも多くのディスクを使用するように構成します。
* コマンド ラインで `--norestart` を渡します。 現時点では、コンテナー内から Windows コンテナーを再起動しようとすると、ホストに `ERROR_TOO_MANY_OPEN_FILES` が返されます。
* 自分のイメージが mcr.microsoft.com/windows/servercore に直接基づいている場合、.NET Framework が正常にインストールされず、インストール エラーが示されない場合があります。 インストールが完了した後、マネージド コードが実行されない可能性があります。 代わりに、イメージを [microsoft/dotnet-framework:4.7.1](https://hub.docker.com/r/microsoft/dotnet-framework) 以降に基づくようにします。 たとえば、次のような MSBuild を使用して構築するときにエラーが表示する場合があります。

  > C:\BuildTools\MSBuild\15.0\bin\Roslyn\Microsoft.CSharp.Core.targets(84,5): エラー MSB6003: 指定されたタスク実行可能ファイル "csc.exe" を実行できませんでした。 ファイルまたはアセンブリ 'System.IO.FileSystem, Version=4.0.1.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'、またはその依存関係の 1 つが読み込めませんでした。 指定されたファイルが見つかりません。

::: moniker range="vs-2017"

* Visual Studio 2017 バージョン 15.8 以前 (すべての製品) を、mcr.microsoft.com/windows/servercore:1809 以降にインストールすることはできません。 詳細については、「 https://aka.ms/setup/containers/servercore1809 」を参照してください。

::: moniker-end

## <a name="build-tools-container"></a>ビルド ツール コンテナー

ビルド ツール コンテナーを使用すると、以下の既知の問題が発生する場合があります。 問題が修正されているどうか、その他の既知の問題があるかどうかについては、[Developer Community](https://aka.ms/feedback/suggest?space=8) を参照してください。

* IntelliTrace はコンテナー内の[一部のシナリオ](https://github.com/Microsoft/vstest/issues/940)では動作しない場合があります。
* 以前のバージョンの Docker for Windows では、コンテナー イメージの既定のサイズは 20 GB のみで、Build Tools に適合しません。 127 GB 以上に[イメージのサイズを変更する手順](/virtualization/windowscontainers/manage-containers/container-storage#storage-limits)に従ってください。
ディスク領域の問題を確認するには、ログ ファイルで詳細を確認してください。 ディスク領域が不足した場合、`vslogs\dd_setup_<timestamp>_errors.log` ファイルには次のものが含まれます。 
```
Pre-check verification: Visual Studio needs at least 91.99 GB of disk space. Try to free up space on C:\ or change your target drive.
Pre-check verification failed with error(s) :  SizePreCheckEvaluator.
```
[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>参照

* [コンテナーにビルド ツールをインストールする](build-tools-container.md)
* [コンテナーの高度な例](advanced-build-tools-container.md)
* [Visual Studio Build Tools のワークロード ID とコンポーネント ID](workload-component-id-vs-build-tools.md)
