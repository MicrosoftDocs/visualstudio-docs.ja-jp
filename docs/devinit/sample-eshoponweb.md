---
title: eShopOnWeb
description: dotnet-architecture/eShopOnWeb リポジトリの devinit を使用するカスタマイズの例。
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
ms.openlocfilehash: 1356cf2654adfb78fcff61c9f9dab95f1fdbe913
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635353"
---
# <a name="eshoponweb"></a>eShopOnWeb

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

この例では dotnet アーキテクチャ サンプル [eShopOnWeb](https://github.com/dotnet-architecture/eShopOnWeb) をカスタマイズし、[GitHub Codespaces](https://github.com/features/codespaces) で自動プロビジョニングする方法を示しています。

## <a name="postclonesetupps1"></a>PostCloneSetup.ps1

このスクリプトは _PostCloneSetup.ps1_ から呼び出され、リポジトリを設定します。ローカルで実行することもできます。 このファイルは、 _.devcontainer.json_ と同じフォルダーに存在する必要があります。

```console
devinit init
dotnet ef database update -c catalogcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
dotnet ef database update -c appidentitydbcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
```

## <a name="devinitjson"></a>.devinit.json

[`.devinit.json`](devinit-json.md) ファイルの内容。 このファイルは、 _.devcontainer.json_ と同じフォルダーに存在する必要があります。

```json
{
    "run": [
        {
            "tool": "require-dotnetcoresdk"
        },
        {
            "tool": "require-mssql"
        },
        {
            "tool": "dotnet-toolinstall",
            "input": "dotnet-ef",
            "additionalOptions": "--global"
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
