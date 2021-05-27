---
title: dotnet-restore
description: devinit ツール dotnet-restore。
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
ms.openlocfilehash: 5beea84edce408acda7fc157f530c4a5f3253835
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635341"
---
# <a name="dotnet-restore"></a>dotnet-restore

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`dotnet-restore` ツールでは、依存関係と、プロジェクト ファイルに指定されているプロジェクト固有のツールを復元します。 dotnet restore の詳細については、[こちら](/dotnet/core/tools/dotnet-restore)をご覧ください。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略できるプロパティです。 使用しません。                                                |
| [**input**](#input)                              | string | No       | 復元するプロジェクトまたはソリューション ファイルのパス。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[その他のオプション](#additional-options)」を参照してください。                     |

### <a name="input"></a>入力

復元するプロジェクトまたはソリューション ファイルのパス。

### <a name="additional-options"></a>追加オプション

追加オプションは、dotnet restore コマンドにそのまま渡されます。

### <a name="default-behavior"></a>既定の動作

`dotnet-restore` ツールの既定の動作では、現在のディレクトリで `dotnet restore` を実行します。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `dotnet-restore` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-restore-dependencies-and-tools-of-a-project"></a>プロジェクトの依存関係とツールを復元する .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "dotnet-restore",
            "input": "C:\\app1\\app1.csproj"
        }
    ]
}
```