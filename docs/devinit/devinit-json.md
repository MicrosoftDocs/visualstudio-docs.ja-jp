---
title: devinit 構成ファイル
description: devinit の .devinit.json マニフェスト ファイルに関するドキュメント。
ms.date: 11/02/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 4f94ee609ba4c0783a06648ed037e58d864aa2a9
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635334"
---
# <a name="devinit-configuration-file"></a>devinit 構成ファイル

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`.devinit.json` ファイルでは、アプリケーションの実行およびビルドに必要なシステム全体の依存関係が定義されます。 システム全体の依存関係は、Node.js、SQL Server、IIS、RabbitMQ、Docker などのようなものです。これらは、特定のリポジトリではインストールされない、開発用ボックスに通常インストールするものです。 NuGet や NPM などのパッケージ マネージャーの場合のように、アプリケーション固有の依存関係を定義する場所ではありません。 ただし、パッケージ マネージャーが必要であることを定義する場所です。

## <a name="file-location"></a>ファイルの場所

`devinit init` コマンドは、`.devinit.json` ファイルを介して実行されます。 既定では、`devinit` によって次の場所にあるファイルが検索されます。

* {current-directory}\\.devinit.json
* {current-directory}\\devinit.json
* {current-directory}\\.devinit\\.devinit.json
* {current-directory}\\.devinit\\devinit.json
* {current-directory}\\devinit\\.devinit.json
* {current-directory}\\devinit\\devinit.json
* {current-directory}\\.devcontainer\\.devinit.json
* {current-directory}\\.devcontainer\\devinit.json

> [!NOTE]
> 複数の既定のファイルが見つかった場合は、上記の一覧で最初に出現するファイルが devinit によって使用されます。

`.devinit.json` ファイルを `--file`/`-f` オプションで明示的に指定することもできます。

### <a name="directories-and-relative-paths"></a>ディレクトリと相対パス

パスは、devinit が実行されている場所を基準とした相対パスです。 これは通常、`devinit` が実行された現在の作業ディレクトリです。

## <a name="file-format"></a>ファイル形式
`.devinit.json` には、実行するツールを複数指定できます。 `run` セクションには、任意の数のオブジェクトを含めることができます。 この例については、すべてのツールが含まれているサンプルの [.devinit.json](sample-all-tool.md) を参照してください。

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "comments": "string",
    "run": [
        {
            "comments": "string",
            "tool": "string",
            "input": "string|null|undefined",
            "additionalOptions": "string|null|undefined"
        }
    ]
}
```

### <a name="property-values"></a>プロパティ値

| 名前         | Type   | 必須 | 値                              |
|--------------|--------|----------|------------------------------------|
| **コメント** | string | No       | ファイルのコメント。             |
| **run**      | array  | はい      | [ツール オブジェクトの実行](#run-tool-object) |

#### <a name="run-tool-object"></a>ツール オブジェクトの実行

| 名前                  | Type   | 必須 | 値                                                                                                      |
|-----------------------|--------|----------|------------------------------------------------------------------------------------------------------------|
| **コメント**          | string | No       | ツール エントリのコメント。                                                                               |
| **tool**              | string | はい      | ツールの名前。 使用可能なツールの一覧については、`devinit list` コマンドを参照してください。                            |
| **input**             | string | No       | ツールの入力。 ツールによって異なります。 たとえば、必要なバージョン、パッケージ ID、ファイル名、フォルダーなどです。|
| **additionalOptions** | string | No       | ツールに渡す追加のコマンド ライン引数。                                                |

## <a name="examples"></a>例

devinit の使用例については、[サンプルのセクション](sample-readme.md)を参照してください。
