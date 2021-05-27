---
title: require-vcpkg
description: devinit ツール require-vcpkg。
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
ms.openlocfilehash: f2a03c64da74a323a0554a64faf3482d224aede8
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635377"
---
# <a name="require-vcpkg"></a>require-vcpkg

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-vcpkg` ツールは [vcpkg](https://github.com/microsoft/vcpkg) のインストールに使用されます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                      |
|--------------------------------------------------|--------|----------|----------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略できるプロパティです。 使用しません。                                      |
| [**input**](#input)                              | string | No       | 使用しません。 詳細については、下の「[入力](#input)」を参照してください。                           |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。 詳細については、下の「[その他のオプション](#additional-options)」を参照してください。 |

### <a name="input"></a>入力

使用しません。

### <a name="additional-options"></a>追加オプション

使用しません。

### <a name="default-behavior"></a>既定の動作

`require-vcpkg` ツールの既定の動作では、vcpkg をインストールし、それを `PATH` に追加します。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-vcpkg` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-vcpkg"></a>vcpkg をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-vcpkg"
        }
    ]
}
```
