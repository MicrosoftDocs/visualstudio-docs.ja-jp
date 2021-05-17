---
title: require-dotnetframeworksdk
description: devinit ツール require-dotnetframeworksdk。
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
ms.openlocfilehash: 0c40ebfd2a8b665a1421ba70c0f785774e97d3df
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635329"
---
# <a name="require-dotnetframeworksdk"></a>require-dotnetframeworksdk

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-dotnetframeworksdk` ツールを使用すると、[提供されているインストーラ](https://dotnet.microsoft.com/download/visual-studio-sdks)を介して [.NET Framework SDK](https://dotnet.microsoft.com/) をインストールできます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須  | 値                                                                                    |
|--------------------------------------------------|--------|-----------|------------------------------------------------------------------------------------------|
| **コメント**                                     | string | No        | comments は省略可能なプロパティです。 使用しません。                                                    |
| [**input**](#input)                              | string | No        | インストールする .NET Framework SDK のバージョン。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No        | 使用しません。 詳細については、下の「[追加オプション](#additional-options)」を参照してください。               |

### <a name="input"></a>入力

`input` プロパティは、インストールする .NET Framework SDK のバージョンを指定するために使用されます。 バージョンの一覧については、[dotnet-framework のサイト](https://dotnet.microsoft.com/download/visual-studio-sdks)を参照してください。

### <a name="additional-options"></a>追加オプション

使用しません。

### <a name="default-behavior"></a>既定の動作

`require-dotnetframeworksdk` ツールの既定の動作では、最新リリースがインストールされます。 最新バージョンについては、[提供されているインストーラ](https://dotnet.microsoft.com/download/visual-studio-sdks)を参照してください。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-dotnetframeworksdk` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-latest-net-framework"></a>最新の .NET Framework をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetframeworksdk"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-the-net-framework"></a>特定のバージョンの .NET Framework をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetframeworksdk",
            "input": "4.8.0"
        }
    ]
}
```