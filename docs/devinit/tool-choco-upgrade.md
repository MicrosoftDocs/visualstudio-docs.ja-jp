---
title: choco-upgrade
description: devinit ツール choco-upgrade。
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
ms.openlocfilehash: bcd2288ef9399f27f53565ea7ea971579cad7858
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635308"
---
# <a name="choco-upgrade"></a>choco-upgrade

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`choco-upgrade` ツールを使用すると、[chocolatey](https://chocolatey.org/docs/commandsupgrade) パッケージのインストールと更新を行うことができます。

## <a name="usage"></a>使用方法

`input` プロパティと `additionalOptions` プロパティの両方が省略されているか空の場合、ツールは何も行いません。

| 名前                                             | Type   | 必須  | 値                                                                                                          |
|--------------------------------------------------|--------|-----------|----------------------------------------------------------------------------------------------------------------|
| **コメント**                                     | string | No        | comments は省略可能なプロパティです。 使用しません。                                                                          |
| [**input**](#input)                              | string | はい       | アップグレードするパッケージ。 詳細については、下の「[入力](#input)」を参照してください。                                                 |
| [**additionalOptions**](#additional-options)     | string | No        | ツールに渡す追加オプション。 詳細については、下の「[追加オプション](#additional-options)」を参照してください。       |

### <a name="input"></a>入力

`input` プロパティは、アップグレードするパッケージの名前 ("mongodb" など)、または _packages.config_、 _.nuspec_、および _.nupkg_ 形式の構成ファイルへのパスを指定するために使用されます。 `input` の値は、[`additionalOptions`](#additional-options) で指定された引数、および組み込みの `choco` オプション ([下記](#built-in-options)で定義) と共に、`choco upgrade` コマンドに追加されます (例: `choco upgrade mongodb`)。 パッケージは、[Chocolatey パッケージ ギャラリー](https://chocolatey.org/packages)にあります。 構成ファイルを使用する場合は、そのファイルへのパスを `input` プロパティに渡すことができます (例: `"input":"packages.config"`)。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、`additionalOptions` の値として渡すことができます。 これらの引数は、chocolatey のドキュメントで定義されており、[`choco upgrade`](https://chocolatey.org/docs/commands-upgrade) で使用される引数にそのまま渡されます。

### <a name="built-in-options"></a>組み込みオプション

`choco-upgrade` ツールでは、`choco` をヘッドレスで実行できるように、`choco` のコマンド ライン引数がいくつか設定されます。 これらの引数を以下に示します。詳細については、[chocolatey のドキュメント](https://chocolatey.org/docs/)を参照してください。

| 名前                  | 説明                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------|
| **--yes**             | すべてのプロンプトを確認する - プロンプトではなく、肯定応答を選択します。 `--accept-license` を意味します。 |
| **--no-progress**     | 進行状況を表示しない - 進行状況のパーセンテージは表示されません。                                         |
| **--skip-powershell** | PowerShell をスキップする - chocolateyInstall.ps1 は実行されません。                                              |

### <a name="default-behavior"></a>既定の動作

`input` プロパティは必須であり、`choco-upgrade` ツールの既定の動作はエラーを出すことになります。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `choco-upgrade` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-update-packages-listed-in-packagesconfig"></a>packages.config に一覧表示されているパッケージを更新する .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "packages.config",
        }
    ]
}
```

#### <a name="devinitjson-that-will-upgrade-mongodb"></a>MongoDB をアップグレードする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "mongodb"
        }
    ]
}
```

#### <a name="devinitjson-that-will-upgrade-to-a-specific-version-of-mongodb"></a>特定のバージョンの MongoDB にアップグレードする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "choco-upgrade",
            "input": "mongodb",
            "additionalOptions": "--version 4.2.7"
        }
    ]
}
```