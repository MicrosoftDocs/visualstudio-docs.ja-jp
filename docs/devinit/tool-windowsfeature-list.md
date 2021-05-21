---
title: windowsfeature-list
description: devinit ツール windowsfeature-list。
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
ms.openlocfilehash: 3225e67db734e02abce96820d44ca1515ddc348f
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635371"
---
# <a name="windowsfeature-list"></a>windowsfeature-list

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`windowsfeature-list` ツールは、すべての Windows 機能の有効/無効の状態を一覧表示するために使用されます。

| 名前                                             | Type   | 必須 | 値                                      |
|--------------------------------------------------|--------|----------|--------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。      |
| [**input**](#input)                              | string | No       | 使用しません。 無視されます。                         |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。 無視されます。                         |

### <a name="input"></a>入力

使用しません。 無視されます。

#### <a name="additional-options"></a>追加オプション

使用しません。 無視されます。

### <a name="default-behavior"></a>既定の動作

`windowsfeature-list` ツールの既定の動作では、すべての Windows 機能の有効/無効の状態が一覧表示されます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `windowsfeature-list` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-list-the-state-of-all-windows-features"></a>すべての Windows 機能の状態を一覧表示する .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0.json",
    "run": [
        {
            "tool": "windowsfeature-list"
        }
    ]
}
```
