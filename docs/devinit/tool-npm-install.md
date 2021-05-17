---
title: npm-install
description: devinit ツール npm-install。
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
ms.openlocfilehash: 011364e851670362ecaa9f4bdbfff965782ed706
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635304"
---
# <a name="npm-install"></a>npm-install

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`npm-install` ツールを使用すると、[NPM](https://www.npmjs.com/) パッケージをインストールできます。

## <a name="usage"></a>使用方法

`input` プロパティと `additionalOptions` プロパティの両方が省略されているか空の場合、ツールは何も行いません。

| 名前                                             | Type   | 必須 | 値                                                                                                          |
|--------------------------------------------------|--------|----------|----------------------------------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                                          |
| [**input**](#input)                              | string | No       | インストールするパッケージ。 詳細については、下の「[入力](#input)」を参照してください。                                                 |
| [**additionalOptions**](#additional-options)     | string | No       | ツールに渡す追加オプション。 詳細については、下の「[追加オプション](#additional-options)」を参照してください。       |

### <a name="input"></a>入力

`input` プロパティは、インストールするパッケージの名前を指定するために使用されます ("mongo" など)。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、`additionalOptions` の値として渡すことができます。 これらの引数は、[npm install](https://docs.npmjs.com/cli/install) で使用される引数にそのまま渡されます。

### <a name="default-behavior"></a>既定の動作

`npm-install` ツールの既定の動作では、`npm install` が引数なしで実行されます。 この動作の詳細については、[npm のドキュメント](https://docs.npmjs.com/cli/v6/commands/npm-install)を参照してください。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `npm-install` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-mongo"></a>mongo をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "npm-install",
            "input": "mongo",
        }
    ]
}
```
