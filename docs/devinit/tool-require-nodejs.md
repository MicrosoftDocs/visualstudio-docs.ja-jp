---
title: require-nodejs
description: devinit ツール require-nodejs。
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
ms.openlocfilehash: 75690f85fb627140226242b476d70bfc4dac6ed2
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635345"
---
# <a name="require-nodejs"></a>require-nodejs

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-nodejs` ツールは、Node.js 組織によって配布された MSI を使用して [Node.js](https://nodejs.org/) をインストールするために使用されます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                     |
|--------------------------------------------------|--------|----------|---------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                     |
| [**input**](#input)                              | string | No       | インストールする Node.JS のバージョン。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。          |

### <a name="input"></a>入力

`input` プロパティは、Node.js のバージョンを指定するために使用されます。 バージョンの一覧については、[Node.js のダウンロード ページ](https://nodejs.org/en/download/)を参照してください。 Major.Minor.Path 形式の完全なバージョン番号が必要です (たとえば、14.4.0)。省略されている場合、インストールは失敗します。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、`additionalOptions` の値として渡すことができます。 これらの引数は、Node.js の MSIインストーラーにそのまま渡されます。  

### <a name="default-behavior"></a>既定の動作

`require-nodejs` ツールの既定の動作では、Node.JS [Web サイト](https://nodejs.org/en/download/)の詳細に従って、Node の最新の LTS バージョンがインストールされます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-nodejs` を実行する方法の例を次に示します。 

#### <a name="devinitjson-that-will-install-the-lts-of-nodejs"></a>Node.js の LTS をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nodejs"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-nodejs"></a>特定のバージョンの Node.js をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-nodejs",
            "input": "14.4.0"
        }
    ]
}
```
