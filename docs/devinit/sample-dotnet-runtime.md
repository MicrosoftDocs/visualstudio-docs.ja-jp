---
title: .NET Core ランタイム
description: devinit を使用した dotnet/runtime リポジトリのカスタマイズ例。
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: d703e71b6f8ab57ab07c4143fdd5435585c6004c
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635354"
---
# <a name="net-core-runtime"></a>.NET Core ランタイム

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

この例は、[GitHub Codespaces](https://github.com/features/codespaces)で自動的にプロビジョニングされるように .Net Core ランタイム [dotnet/runtime](https://github.com/dotnet/runtime) をカスタマイズする方法を示しています。

## <a name="postclonesetupps1"></a>PostCloneSetup.ps1

このスクリプトは _PostCloneSetup.ps1_ から呼び出され、リポジトリを設定します。ローカルで実行することもできます。 このファイルは、 _.devcontainer.json_ と同じフォルダーに存在する必要があります。

```console
devinit init
git config --system core.longpaths true
```

## <a name="packagesconfig"></a>packages.config

_packages.config_ ファイルは、インストールする Chocolatey パッケージの一覧を定義する [Chocolatey](https://chocolatey.org/) ファイルです。 このファイルは、 _.devcontainer.json_ と同じフォルダーに存在する必要があります。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="python" version="3.8.3"  />
    <package id="cmake" version="3.17.3"  />
</packages>
```

## <a name="devinitjson"></a>.devinit.json

[`.devinit.json`](devinit-json.md) ファイルの内容。 このファイルは、 _.devcontainer.json_ ファイルと同じフォルダーに存在する必要があります。

```json
{
    "run": [
        {
            "tool": "require-dotnetcoresdk"
        },
        {
            "tool": "choco-install",
            "input": "packages.config"
        },
        {
            "tool": "require-vscomponent"
        }
    ]
}
```

## <a name="devcontainerjson"></a>.devcontainer.json

リポジトリのルートにある _.devinit.json_ ファイルの内容。

```json
{
  "postCreateCommand": "Powershell.exe -ExecutionPolicy unrestricted -File .\\PostCloneSetup.ps1"
}
```
