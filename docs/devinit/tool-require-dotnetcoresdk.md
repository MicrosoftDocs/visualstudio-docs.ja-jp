---
title: require-dotnetcoresdk
description: devinit ツール require-dotnetcoresdk。
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
ms.openlocfilehash: 1963ad8dfe1bd31eb3f98ec6fdf57524a274cfb6
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635323"
---
# <a name="require-dotnetcoresdk"></a>require-dotnetcoresdk

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-dotnetcoresdk` ツールは、[.NET Core SDK](https://dotnet.microsoft.com/) と共有ランタイムを [dotnet-install](/dotnet/core/tools/dotnet-install-script) スクリプトでインストールするために使用されます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                               |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                               |
| [**input**](#input)                              | string | No       | インストールする .NET Core SDK のバージョン。 詳細については、下の「[入力](#input)」を参照してください。 |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。                    |

### <a name="input"></a>入力

`input` プロパティは、インストールする .NET Core SDK のバージョンを指定するために使用されます。 バージョンの一覧については、[dotnet-core のサイト](https://dotnet.microsoft.com/download/dotnet-core)を参照してください。

### <a name="additional-options"></a>追加オプション

追加の構成オプションは、`additionalOptions` の値として渡すことができます。 これらの引数は、[dotnet-install](/dotnet/core/tools/dotnet-install-script) スクリプトで使用される引数にそのまま渡されます。 使用可能なパラメーターの詳細については、[dotnet-install](/dotnet/core/tools/dotnet-install-script) スクリプトの[ドキュメント](/dotnet/core/tools/dotnet-install-script)を参照してください。 `additionalOptions` を使用する場合は、必ず PowerShell の引数名と形式を使用してください。

> [!NOTE]
> スペースが含まれている値を引数に追加する場合は、エスケープされた引用符 (円記号を使用) のペアを追加する必要があります。 「[使用例](#example-usage)」で `-InstallDir` を使用している例を参照してください。

### <a name="default-behavior"></a>既定の動作

`require-dotnetcoresdk` ツールの既定の動作では、現在の作業ディレクトリの `global.json` [(ドキュメント)](/dotnet/core/tools/global-json?tabs=netcore3x) ファイルに指定されているバージョンの .NET Core SDK がインストールされます。 `global.json` ファイルが見つからない場合、`require-dotnetcoresdk` では最新バージョンの .NET Core SDK と共有ランタイムがインストールされます。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-dotnetcoresdk` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-the-latest-version-of-net-core"></a>最新バージョンの .NET Core をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core"></a>特定のバージョンの .NET Core をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "input": "3.0.0"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-a-specific-version-of-net-core-and-aspnet-core"></a>特定のバージョンの .NET Core と ASP.NET Core をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "input": "3.0.0",
            "additionalOptions": "-Runtime aspnetcore"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-net-core-in-a-specific-directory"></a>特定のディレクトリに .NET Core をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-dotnetcoresdk",
            "additionalOptions": "-InstallDir \"C:\\Program Files\\dotnet\""
        }
    ]
}
```