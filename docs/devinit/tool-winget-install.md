---
title: winget-install
description: winget 用の devinit ツール。
ms.date: 02/08/2021
ms.topic: reference
author: andysterland
ms.author: andster
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 4a2ad1ef30692d7d23f2d450f0ba32d6f38f8262
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635369"
---
# <a name="winget-install"></a>winget-install

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`winget-install` ツールは [winget パッケージ](https://docs.microsoft.com/windows/package-manager/winget/)のインストールに使用されます。

## <a name="usage"></a>使用法

`input` プロパティと `additionalOptions` プロパティの両方が省略されているか空の場合、ツールはエラーを出力します。

| 名前                                         | Type   | 必須 | 値                                                                             |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------------|
| **コメント**                                 | string | いいえ       | comments は省略可能なプロパティです。 使用しません。                                             |
| [**input**](#input)                          | string | いいえ       | インストールするパッケージ。 詳細については、下記の「[入力](#input)」を参照してください。                    |
| [**additionalOptions**](#additional-options) | string | いいえ       | 詳細については、下記の「[追加オプション](#additional-options)」を参照してください。                  |

### <a name="input"></a>入力

input プロパティは、インストールするパッケージの `Id` または `Name` を指定するために使用します ("MongoDB.Server" など)。 input の値は `winget install` コマンドに追加されます (たとえば、`winget install MongoDB.Server`)。 パッケージ名が一意ではなく、他のパッケージと一致する場合は、パッケージの `Id` を指定し、`additionalOptions` に `--exact` フラグを追加して、パッケージ ID を正確に一致させることができます。 パッケージの `Id` は、`winget search` コマンドを実行し、パッケージの `Id` パラメーターを使用して確認できます。  

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、additionalOptions の値として渡すことができます。 これらの引数は、`winget install` の[ドキュメント](https://docs.microsoft.com/windows/package-manager/winget/install)で定義されており、`winget install` で使用される引数にそのまま渡されます。

#### <a name="manifests"></a>マニフェスト

`winget` でサポートされる追加オプションは、インストールするパッケージの詳細を示す[マニフェスト ファイル](https://docs.microsoft.com/windows/package-manager/winget/install#local-install)を提供する機能です。 devinit でこの機能を使用するには、`input` パラメーターを空にする必要があります。また、`additionalOptions` プロパティには `--manifest` オプションを追加し、その後にマニフェストへのパスを指定する必要があります (たとえば、`--manifest path.to.manifest.yml`)。

### <a name="built-in-options"></a>組み込みオプション

winget-install ツールでは、winget をヘッドレスで実行できるように、winget のコマンド ライン引数がいくつか設定されます。 これらの引数を以下に示します。詳細については、`winget install` の[ドキュメント](https://docs.microsoft.com/windows/package-manager/winget/install)を参照してください。

| 名前     | 説明                                                                                                                       |
|----------|-----------------------------------------------------------------------------------------------------------------------------------|
| --silent | サイレント モードでインストーラーを実行します。 これにより、すべての UI が抑制されます。 既定のエクスペリエンスでは、インストーラーの進行状況が表示されます。                       | 

## <a name="example-usage"></a>使用例

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-6.0",
    "run": [
        {
            "comments": "Installs Microsoft PowerToys.",
            "tool": "winget-install",
            "input": "Microsoft.PowerToys",
            "additionalOptions": "--version 0.15.2",
        },
        {
            "comments": "Installs PostgreSQL.",
            "tool": "winget-install",
            "input": "PostgreSQL.PostgreSQL",
            "additionalOptions": "--exact"
        },
        {
            "comments": "Installs the package defined in winget-manifest.yml.",
            "tool": "winget-install",
            "additionalOptions": "--manifest winget-manifest.yml"
        }
    ]
}
```
