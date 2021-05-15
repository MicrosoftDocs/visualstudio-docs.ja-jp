---
title: windowsfeature-disable
description: devinit ツール windowsfeature-disable。
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
ms.openlocfilehash: cd06b3a3d063a2c209a901bbed1600570c31cd8e
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635372"
---
# <a name="windowsfeature-disable"></a>windowsfeature-disable

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`windowsfeature-disable` ツールは Windows 機能を取得するために使用されます。

## <a name="usage"></a>使用法

| 名前                                             | Type   | 必須 | 値                                                                  |
|--------------------------------------------------|--------|----------|------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略できるプロパティです。 使用しません。                                  |
| [**input**](#input)                              | string | はい      | インストールする Windows 機能。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[その他のオプション](#additional-options)」を参照してください。       |

### <a name="input"></a>入力

`input` プロパティは、無効にする `windows feature` の `name` になります。

### <a name="additional-options"></a>その他のオプション

なし。

### <a name="default-behavior"></a>既定の動作

`input` は必須であり、`windowsfeature-disable` ツールの既定の動作はエラーを出すことになります。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `windowsfeature-disable` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-disable-a-specified-feature"></a>指定の機能を無効にする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-windowsfeature",
            "input": "web-server",
        }
    ]
}
```
