---
title: require-vscomponent
description: devinit ツール require-vscomponent。
ms.date: 02/08/2021
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 7d6609c49efb9f77c9823ca3f703b8843ddb753e
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635376"
---
# <a name="require-vscomponent"></a>require-vscomponent

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-vscomponent` ツールは、Visual Studio の構成を既存の Visual Studio にインポートするために使用されます。 詳細は[こちら](../install/import-export-installation-configurations.md)の `.vsconfig` をご覧ください。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                     | Type   | 必須 | 値                                                                |
|------------------------------------------|--------|----------|----------------------------------------------------------------------|
| **コメント**                             | string | No       | comments は省略可能なプロパティです。 使用しません。                                |
| [**input**](#input)                      | string | No       | `.vsconfig` の完全なパス。 詳細については、下の「[入力](#input)」を参照してください。 |
| [additionalOptions](#additional-options) | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。     |

### <a name="input"></a>入力

`input` プロパティは、`.vsconfig` ファイルの完全なパスを指定するために使用されます。 記載されていない場合、ツールは現在のディレクトリで `.vsconfig` を検索し、その値を Visual Studio インストーラーに渡します。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、`additionalOptions` の値として渡すことができます。 

| 名前                      | Type      | 必須 | 値                                                                                                                                                                                    |
|---------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --installPath             | string    | No       | 変更する Visual Studio インスタンスのインストール パス。                                                                                                                       |

インストール パスが指定されていない場合は、コンピューター上に複数のインスタンスがある場合、ツールによって、コンピューターにインストールされている最初の Visual Studio が変更されます。 

### <a name="default-behavior"></a>既定の動作

`require-vscomponent` ツールの既定の動作では、現在のディレクトリ内の `.vsconfig` ファイルを検索し、これらの詳細を使用して Quiet モードで Visual Studio インストーラーを実行します。 `require-vscomponent` は、既存の Visual Studio のインストールの変更のみをサポートしています。 

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-vscomponent` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-import-the-configurations-of-a-given-vsconfig-file-path"></a>指定された vsconfig ファイルのパスの構成をインポートする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "comments": "A sample dot-devinit file.",
    "run": [
        {
            "tool": "require-vscomponent",
            "input": "C:\\.vsconfig"
        }
    ]
}
```

#### <a name="devinitjson-that-will-import-the-configurations-of-a-given-vsconfig-file-path-to-the-visual-studio-instance-specified-via-an-install-path"></a>指定された vsconfig ファイルのパスの構成をインストール パスで指定された Visual Studio インスタンスにインポートする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "comments": "A sample dot-devinit file.",
    "run": [
        {
            "tool": "require-vscomponent",
            "input": "C:\\.vsconfig",
            "additionalOptions": "--installPath 'C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Enterprise'"
        }
    ]
}
```