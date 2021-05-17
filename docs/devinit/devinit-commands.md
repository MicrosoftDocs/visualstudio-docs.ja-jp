---
title: devinit のコマンド
description: devinit のコマンドを使用してコンポーネントをインストールする方法の詳細を説明します。
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: d6c8f487fcb35fc210db57f0c8a49a2a86f909e9
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635333"
---
# <a name="devinit-commands"></a>devinit のコマンド

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

## <a name="init"></a>Init

```console
devinit init
```

[.devinit.json](devinit-json.md) ファイルに指定されているツールを実行して、環境を初期化します。

### <a name="options-for-init"></a>init のオプション

`devinit init` コマンドの省略可能なオプション。

| 引数             | 必須 | 説明                                                               |
|----------------------|----------|---------------------------------------------------------------------------|
| -f、--file            | No       | `.devinit.json` ファイルへのパス。                                         |
| --error-action       | No       | エラーを処理する方法を指定します。 オプション: Stop、Ignore、Continue (既定)。|
| -v、--verbose         | No       | 詳細出力を生成します。                                                      |
| -n、--dry-run         | No       | ドライ ラン。                                                                  |

#### <a name="--file-argument"></a>--file 引数

_devinit.json_ ファイルへのパスを指定します。 --file が指定されていない場合は、次の場所にある既定のファイルが検索されます。

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

#### <a name="--error-action-argument"></a>--error-action 引数

[下記](#options-for-run)を参照してください。

#### <a name="--verbose-switch"></a>--verbose スイッチ

[下記](#options-for-run)を参照してください。

#### <a name="--dry-run-switch"></a>--dry-run スイッチ

[下記](#options-for-run)を参照してください。

## <a name="run"></a>実行

```console
devinit run -t <toolname>
```

特定のツールを実行します。パラメーターは次のとおりです。 具体的な使用方法については、各ツールの[ドキュメント](devinit-tool-list.md)を参照してください。

### <a name="options-for-run"></a>run のオプション

`devinit run` コマンドのオプション。

| 引数                                      | 必須 | 説明                                                                          |
|-----------------------------------------------|----------|--------------------------------------------------------------------------------------|
| -t、--tool                                     | はい      | 必須。 ツールの名前。                                                             |
| -i、--input                                    | No       | ツールの入力値。 たとえば、ファイル名、パッケージ、名前などです。                     |
| --error-action                                | No       | ツールのエラーを処理する方法を指定します。Stop、Ignore、Continue。 既定値は stop です。 |
| -v、--verbose                                  | No       | 詳細出力を生成します。                                                                 |
| -n、--dry-run                                  | No       | ドライ ラン。                                                                             |
| --&lt;arg1&gt; &lt;arg2&gt; ... &lt;argN&gt;  | No       | ツールの追加のコマンド ライン引数。                                       |

#### <a name="--error-action-argument"></a>--error-action 引数

ツールから 0 以外の終了コードが返された場合に実行するアクションを指定します。 有効な値は次のとおりです。

| 引数 | 説明                                                                                                                                                                                                                                                                           |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| continue | 標準エラーにエラーを出力した後、他のツールの処理を続行します。 devinit.exe の終了コードは 0 以外 (失敗) です。 この動作は Stop エラー アクションに似ていますが、処理は続行されます。 `continue` は、init コマンドの既定のエラー アクションです。              |
| ignore   | 標準出力に警告を出力した後、他のツールの処理を続行します。 DevInit プロセスの終了コードは常に 0 (成功) です。 `ignore` 設定では、すべてのエラーが無視されます。                                                                                                      |
| stop     | 標準エラーにエラーを出力し、ツールの処理を停止します。 devinit.exe の終了コードは 0 以外 (失敗) です。 これは continue エラー アクションに似ていますが、最初に発生したエラーで処理が停止します。 `stop` は、init を除くすべてのコマンドの既定のエラー アクションです。 |

#### <a name="--dry-run-switch"></a>--dry-run スイッチ

実行されるツール コマンドをエコーします。 ツールによっては、そのツールについて説明されているように、さらにアクションが実行される場合があります。 

#### <a name="--verbose-switch"></a>--verbose スイッチ

標準出力に詳細出力を出力します。 実行するツールで詳細オプションがサポートされている場合は、verbose スイッチがツールに反映されます。

#### <a name="--dry-run-switch"></a>--dry-run スイッチ

実行されるツール コマンドをエコーしますが、どのツールも実行しません。

#### <a name="additional-command-line-arguments"></a>追加のコマンド ライン引数

`<arg>` の値にスペースが含まれている場合は、エスケープされた引用符のペアを追加する必要があります。

```console
devinit run -t <toolname> -<somearg> "<some value>"
```

特定のディレクトリ `C:\Program Files\dotnet` に dotnet をインストールする場合は、次のようにします。

```console
devinit run -t require-dotnetcoresdk --"-InstallDir \"C:\Program Files\dotnet\""
```

## <a name="list"></a>List

```console
devinit list
```

使用可能なすべてのツールの一覧を出力します。

## <a name="show"></a>表示

```console
devinit show -t <toolname>
```

| 引数       | 必須 | 説明                                                                          |
|----------------|----------|--------------------------------------------------------------------------------------|
| -t、--tool      | はい      | 必須。 ツールの名前。                                                             |

指定されたツールのヘルプ情報を出力します。

## <a name="version"></a>Version

```console
devinit version
```

devinit の現在のバージョン情報を出力します。

## <a name="help"></a>ヘルプ

```console
devinit help
devinit help list
```

devinit または特定のコマンド `devinit <command>` のヘルプ テキストを出力します。
 
