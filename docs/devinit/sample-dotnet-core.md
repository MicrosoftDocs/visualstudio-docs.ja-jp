---
title: .NET Core アプリ
description: devinit を使用して特定の .NET Core SDK をインストールするリポジトリの例。
ms.date: 11/04/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: b3e25835f305a96b2205fc96cc0200d68ad033af
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635355"
---
# <a name="net-core-app"></a>.NET Core アプリ

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

devinit を使用して必要な .NET Core SDK バージョンを Codespaces にインストールする例については、[devinit-example-dotnet-core](https://github.com/microsoft/devinit-example-dotnet-core) リポジトリを参照してください。

## <a name="devinitjson"></a>.devinit.json

リポジトリのルートにある _.devinit.json_ ファイルの内容。

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": [
    {
      "comments": "Installs the .NET Core SDK specified in the global.json file.",
      "tool": "require-dotnetcoresdk"
    }
  ]
}
```

## <a name="devcontainerjson"></a>.devcontainer.json

リポジトリのルートにある _.devinit.json_ ファイルの内容。

```json
{
  "postCreateCommand": "devinit init"
}
```

## <a name="globaljson"></a>global.json

リポジトリのルートにある _global.json_ ファイルの内容。

```json
{
  "sdk": {
    "version": "3.1.302"
  }
}
```
