---
title: dotnet-toolinstall
description: devinit ツール dotnet-toolinstall。
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
ms.openlocfilehash: 4daa3722abd169c03656adec39aafc29d5e7e435
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635307"
---
# <a name="dotnet-toolinstall"></a>dotnet-toolinstall

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`dotnet-toolinstall` ツールを使用すると、`dotnet tool update` コマンドを介して [.NET Core ツール](https://dotnet.microsoft.com/)をインストールできます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                 |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                 |
| [**input**](#input)                              | string | はい      | インストールする .NET Core ツール。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。      |

### <a name="input"></a>入力

`input` プロパティは、インストールする .NET Core ツールを指定するために使用されます。 [https://github.com/natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) にツールの非公式な一覧があります。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、`additionalOptions` の値として渡すことができます。 これらの引数は、[`dotnet tool update`](/dotnet/core/tools/global-tools#update-a-tool) コマンドで使用される引数にそのまま渡されます。

`dotnet tool update` コマンドを使用すると、ツールが既にインストールされている場合も安全に処理できます。

### <a name="default-behavior"></a>既定の動作

`input` は必須であり、`dotnet-toolinstall` ツールの既定の動作はエラーを出すことになります。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `dotnet-toolinstall` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-dotnet-trace-tool"></a>dotnet-trace ツールをインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "dotnet-toolinstall",
            "input": "dotnet-trace"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-dotnet-trace-tool-as-a-global-tool"></a>dotnet-trace ツールをグローバル ツールとしてインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "dotnet-toolinstall",
            "input": "dotnet-trace",
            "additionalOptions": "--global"
        }
    ]
}
```