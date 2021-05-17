---
title: require-nuget
description: devinit ツール require-nuget。
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
ms.openlocfilehash: c49f77fe8b32ce6617b34d522e36cc5988d0c33c
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635343"
---
# <a name="require-nuget"></a>require-nuget

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-nuget` ツールは NuGet CLI をダウンロードし、`PATH` に追加します。 NuGet CLI では、プロジェクト ファイルを変更することなく、パッケージをインストール、作成、公開、および管理するための NuGet 機能がすべて提供されます。 NuGet CLI の詳細については、[こちら](/nuget/reference/nuget-exe-cli-reference)を参照してください。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                |
| [**input**](#input)                              | string | No       | インストールする NuGet CLI のバージョン。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。                     |

### <a name="input"></a>入力

`input` は、インストールする NuGet CLI のバージョンを指定するために使用される省略可能なプロパティです。 `input` を省略した場合、最新バージョンの CLI がインストールされます。

### <a name="additional-options"></a>追加オプション

使用しません。

### <a name="default-behavior"></a>既定の動作

`require-nuget` ツールの既定の動作では、最新の NuGet CLI がインストールされます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-nuget` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-a-specified-version-of-nuget"></a>指定されたバージョンの NuGet をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nuget",
            "input": "5.5.1",
        }
    ]
}
```