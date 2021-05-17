---
title: vcpkg-install
description: devinit ツール vcpkg-install。
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
ms.openlocfilehash: 8a4cbe6bd1da12985da87d2f872dc74f988ef213
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635373"
---
# <a name="vcpkg-install"></a>vcpkg-install

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`vcpkg-install` ツールは、[vcpkg](https://github.com/microsoft/vcpkg) を使用して C/C++ ライブラリ (ポートと呼ばれる) を取得するために使用されます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                   |
| [**input**](#input)                              | string | はい      | インストールするパッケージ。 詳細については、下の「[入力](#input)」を参照してください。                       |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。                        |

### <a name="input"></a>入力

`input` プロパティは、インストールする `vcpkg` の `name` か、または複数のパッケージをインストールする場合は名前をスペースで区切った一覧である必要があります。 使用可能なポートの一覧については、[vcpkg GitHub リポジトリ](https://github.com/microsoft/vcpkg/tree/master/ports)を参照してください。

### <a name="additional-options"></a>追加オプション

追加のオプションは [vcpkg](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true) コマンドに直接渡され、[vcpkg GitHub リポジトリ](https://github.com/microsoft/vcpkg/blob/master/docs/examples/installing-and-using-packages.md)に記載されています。

### <a name="default-behavior"></a>既定の動作

`input` は必須であり、`vcpkg-install` ツールの既定の動作はエラーを出すことになります。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `vcpkg-install` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-sdl2-port"></a>sdl2 ポートをインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "vcpkg-install",
            "input": "sdl2",
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-multiple-ports"></a>複数のポートをインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [

        {
            "tool": "vcpkg-install",
            "input": "sdl2 sqlite3"
        }
    ]
}
```