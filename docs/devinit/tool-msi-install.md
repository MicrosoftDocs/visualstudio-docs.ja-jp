---
title: msi-install
description: msiexec 用の devinit ツール。
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
ms.openlocfilehash: d2da7f26501cfa686cd0703f7dbbbef4053f761b
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635305"
---
# <a name="msi-install"></a>msi-install

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`msi-install` ツールは、[msiexec](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec) を使用して `.msi` 形式のパッケージ ファイルをインストールするために使用します。

## <a name="usage"></a>使用法

`input` が省略されているか空の場合、ツールはエラーを出力します。

| 名前                                         | Type   | 必須 | 値                                                                             |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------------|
| **コメント**                                 | string | いいえ       | comments は省略可能なプロパティです。 使用しません。                                             |
| [**input**](#input)                          | string | はい      | インストールする `msi`。 詳細については、下記の「[入力](#input)」を参照してください。                      |
| [**additionalOptions**](#additional-options) | string | いいえ       | 詳細については、下記の「[追加オプション](#additional-options)」を参照してください。                  |

### <a name="input"></a>入力

input プロパティは、インストールする `.msi` ファイルのパスまたは URL を指定するために使用します。 `.msi` のパスが正しくない場合や、URL が `.msi` を直接参照していない場合、`msi-install` はインストール パッケージを開けないことを認識します。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、additionalOptions の値として渡すことができます。 これらの引数は、`msiexec` の[ドキュメント](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)で定義されており、`msiexec` で使用される引数にそのまま渡されます。

### <a name="built-in-options"></a>組み込みオプション

msi-install ツールでは、msi をヘッドレスで実行できるように、`msiexec` のコマンド ライン引数がいくつか設定されます。 これらの引数を以下に示します。詳細については、`msiexec` の[ドキュメント](https://docs.microsoft.com/windows-server/administration/windows-commands/msiexec)を参照してください。

| 名前          | 説明                                                                                                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /i            | 通常のインストールを実行します。                                                                                                                                                                    |
| スイッチを        | ユーザー操作を必要としない Quiet モードを指定します。                                                                                                                                        |
| /qn           | インストール プロセス時に UI が表示されないことを指定します。                                                                                                                                           |
| /passive      | インストール時に進行状況バーのみを表示する無人モードを指定します。                                                                                                                    |
| /l*V          | ログを有効にして、詳細情報を含むすべての情報をコンピューターのローカル一時フォルダー内の `devinit.log` ファイルに記録します。 ツールが失敗した場合は、ログ ファイルのパスが表示されます。      |
| /norestart    | インストールの完了後にコンピューターを再起動しないようにしますが、再起動が必要な場合は 3010 終了コードを返します。                                                                  |

### <a name="default-behavior"></a>既定の動作

`input` プロパティは必須であり、`msi-install` ツールの既定の動作はエラーを出すことになります。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `msi-install` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-7-zip-msi"></a>7-Zip MSI をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-4.0",
    "run": [
        {
            "tool": "msi-install",
            "input": "https://www.7-zip.org/a/7z1900.msi"
        }
    ]
}
```
