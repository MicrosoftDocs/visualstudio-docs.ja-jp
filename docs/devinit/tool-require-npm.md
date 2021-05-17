---
title: require-npm
description: devinit ツール require-npm。
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
ms.openlocfilehash: 93723ee50fd718c5abb7c86f0f3b986ed9832abd
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635344"
---
# <a name="require-npm"></a>require-npm

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-npm` ツールは [NPM](https://www.npmjs.com/) のインストールに使用されます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                       |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                       |
| [**input**](#input)                              | string | はい      | NPM のバージョンを指定します。 詳細については、下の「[入力](#input)」を参照してください。                           |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。 詳細については、下の「[追加オプション](#additional-options)」を参照してください。                  |

### <a name="input"></a>入力

`input` プロパティは、npm のバージョンを指定するために使用されます。

### <a name="additional-options"></a>追加オプション

未使用。

### <a name="default-behavior"></a>既定の動作

`require-nodejs` ツールの既定の動作では、npm の最新の LTS バージョンがインストールされます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-npm` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-lts-of-npm"></a>npm の LTS をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-npm"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-npm"></a>特定のバージョンの npm をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-npm",
            "input": "6.14.6"
        }
    ]
}
```