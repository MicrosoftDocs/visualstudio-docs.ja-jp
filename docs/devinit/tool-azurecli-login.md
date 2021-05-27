---
title: azurecli-login
description: devinit ツール azurecli-login。
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
ms.openlocfilehash: 64b215912c21a405c2b2c3a0feb3720a4ab16c44
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635309"
---
# <a name="azurecli-login"></a>azurecli-login

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`azurecli-login` ツールは、[Azure CLI](/cli/azure/authenticate-azure-cli?preserve-view=true&view=azure-cli-latest) 経由で Azure Active Directory にサインインするために使用されます。 このツールでは Azure CLI コマンド `az login --use-device-code` を使用し、コンソールに出力された指示にユーザーが従うために必要なログインを完了します。

## <a name="usage"></a>使用方法

両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                          |
|--------------------------------------------------|--------|----------|--------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略できるプロパティです。 使用しません。                                          |
| [**input**](#input)                              | string | No       | 使用しません。 詳細については、下の「[入力](#input)」を参照してください。                               |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。 詳細については、下の「[その他のオプション](#additional-options)」を参照してください。     |

### <a name="input"></a>入力

使用しません。

### <a name="additional-options"></a>追加オプション

使用しません。

### <a name="default-behavior"></a>既定の動作

`azurecli-login` ツールの既定の動作では、Azure CLI の最新バージョンがインストールされ、`PATH` に追加されます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `azurecli-login` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-trigger-azure-login"></a>Azure ログインをトリガーする .devinit.json:

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "azurecli-login"
        }
    ]
}
```