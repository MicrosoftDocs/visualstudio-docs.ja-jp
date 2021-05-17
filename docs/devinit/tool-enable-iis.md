---
title: enable-iis
description: devinit ツール enable-iis。
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: eecdc2a020117b7345682068cb27509df805ff9b
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635306"
---
# <a name="enable-iis"></a>enable-iis

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`enable-iis` ツールを使用すると、IIS の機能を有効にし、IIS を使用した ASP.NET 開発のために [ASP.NET Core モジュール](/aspnet/core/host-and-deploy/aspnet-core-module)をインストールできます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                               |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                               |
| [**input**](#input)                              | string | No       | 使用しません。                                                                           |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。                                                                           |

### <a name="input"></a>入力

使用しません。

### <a name="additional-options"></a>追加オプション

使用しません。

### <a name="default-behavior"></a>既定の動作

`enable-iis` ツールの既定の動作では、IIS の機能 (IIS-WebServer、IIS-WebServerRole、IIS-WebSockets、および IIS-WebAuthentication) が有効化された後、ASP.NET Core モジュールを含む最新バージョンの ASP.NET ホスティング バンドルがインストールされます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `enable-iis` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-enable-iis-development"></a>IIS 開発を有効にする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0.json",
    "run": [
        {
            "tool": "enable-iis"
        },
    ]
}
```