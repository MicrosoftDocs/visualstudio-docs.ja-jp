---
title: require-psmodule
description: devinit ツール require-psmodule。
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
ms.openlocfilehash: cdb37bf4e714cfc25e5bf82354856fd4d3d63e87
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635378"
---
# <a name="require-psmodule"></a>require-psmodule

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。


`require-psmodule` ツールは、PowerShell スクリプトで使用できるように、[Install-Module](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true) を使用して [PowerShell ギャラリー](https://www.powershellgallery.com/)から [PowerShell モジュール](/powershell/scripting/developer/module/understanding-a-windows-powershell-module?view=powershell-7&preserve-view=true)をインストールするために使用されます。

> [!TIP]
> モジュールをインストールした後も、[Import-Module](/powershell/module/microsoft.powershell.core/import-module?view=powershell-7&preserve-view=true) を使用してスクリプトにインポートする必要があります。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                   |
| [**input**](#input)                              | string | はい      | インストールするパッケージ。 詳細については、下の「[入力](#input)」を参照してください。                       |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。 詳細については、下の「[追加オプション](#additional-options)」を参照してください。              |

### <a name="input"></a>入力

`input` プロパティは、インストールする PowerShell モジュールの `Name` である必要があります。 使用可能な PowerShell モジュールの一覧については、[PowerShell ギャラリー](https://www.powershellgallery.com/)を検索してください。

### <a name="additional-options"></a>追加オプション

追加のオプションは [Install-Module](/powershell/module/powershellget/install-module?preserve-view=true&view=powershell-7) コマンドに直接渡され、[Microsoft Docs](/powershell/module/powershellget/install-module?preserve-view=true&view=powershell-7) に記載されています。

### <a name="default-behavior"></a>既定の動作

`input` は必須であり、`require-psmodule` ツールの既定の動作はエラーを出すことになります。

### <a name="built-in-options"></a>組み込みオプション

`require-psmodule` ツールでは、`Install-Module` をヘッドレスで実行できるように、`Install-Module` のコマンド ライン引数がいくつか設定されます。 これらの引数を以下に示します。詳細については、[Install-Module](/powershell/module/powershellget/install-module?view=powershell-7&preserve-view=true) を参照してください。

| 名前         | 説明                                                                                                                                                                                                                                                                                                                                                               |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **-Force**   | モジュールをインストールし、モジュールのインストール競合に関する警告メッセージをオーバーライドします。 同じ名前のモジュールがコンピューターに既に存在する場合、Force では複数のバージョンをインストールできます。 同じ名前とバージョンの既存モジュールが存在する場合、モジュールを上書きします。 Force と AllowClobber は、Install-Module コマンドで一緒に使用できます。 |
| **-WhatIf**  | -WhatIf フラグは、`devinit` コマンドにドライ ランが渡されたときに追加されます。                                                                                                                                                                                                                                                                                                       |
| **-Verbose** | -Verbose フラグは、`devinit` コマンドに詳細が渡されたときに追加されます。                                                                                                                                                                                                                                                                                                      |


## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-psmodule` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-powershellget-module"></a>PowerShellGet モジュールをインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-psmodule",
            "input": "PowerShellGet",
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-the-powershellget-module-from-a-specific-repository"></a>特定のリポジトリから PowerShellGet モジュールをインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-psmodule",
            "input": "PowerShellGet",
            "additionalOptions": "-Repository PSGallery"
        }
    ]
}
```