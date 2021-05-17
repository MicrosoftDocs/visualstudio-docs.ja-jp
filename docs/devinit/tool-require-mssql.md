---
title: require-mssql
description: devinit ツール require-mssql。
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
ms.openlocfilehash: e39a03fe70d2e4399b758e06e9acb2e0de59ef08
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635367"
---
# <a name="require-mssql"></a>require-mssql

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`require-mssql` ツールは、[Microsoft SQL Server 2019 Developer Edition](https://www.microsoft.com/sql-server/application-development) を MS SQL Server ISO からインストールするために使用されます。 SQL Server は、統合 Windows 認証を使用して `localhost` で使用できるようになり、SQL Server には接続文字列 `"Server=localhost;Integrated Security=true;"` を使用してアクセスできます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                                                   |
|--------------------------------------------------|--------|----------|-----------------------------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                                                   |
| [**input**](#input)                              | string | No       | 詳細については、下の「[入力](#input)」を参照してください。                                                  |
| [**additionalOptions**](#additional-options)     | string | No       | 使用しません。 詳細については、下の「[追加オプション](#additional-options)」を参照してください。              |

### <a name="input"></a>入力

`input` プロパティには、次の 2 つの値のいずれかを持つ文字列を指定できます。

| 値     | 説明                              |
|-----------|------------------------------------------|
| インストール   | SQL Server をインストールします。                     |
| uninstall | SQL Server のすべてのインストールをアンインストールします。 |

### <a name="additional-options"></a>追加オプション

使用しません。

### <a name="default-behavior"></a>既定の動作

`require-mssql` ツールの既定の動作では、SQL Server がインストールされます。

### <a name="built-in-options"></a>組み込みオプション

`require-mssql` ツールでは、インストーラーをヘッドレスで実行できるように、インストーラーのコマンド ライン引数がいくつか設定されます。 これらの引数を以下に示します。詳細については、[SQL のインストールに関するドキュメント](/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-ver15&preserve-view=true)を参照してください。

| 名前                                                               | 説明 |
|--------------------------------------------------------------------|-------------|
| /q                                                                 |             |
| /ACTION=Install                                                    |             |
| /FEATURES=SQLEngine, LocalDB                                       |             |
| /UpdateEnabled                                                     |             |
| /UpdateSource=MU                                                   |             |
| /X86=false                                                         |             |
| /INSTANCENAME=MSSQLSERVER                                          |             |
| /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server"          |             |
| /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" |             |
| /SQLSVCINSTANTFILEINIT=True                                        |             |
| /INSTANCEDIR="C:\Program Files\Microsoft SQL Server"               |             |
| /AGTSVCACCOUNT="NT Service\SQLSERVERAGENT"                         |             |
| /AGTSVCSTARTUPTYPE=Manual                                          |             |
| /SQLSVCSTARTUPTYPE=Automatic                                       |             |
| /SQLCOLLATION="SQL_Latin1_General_CP1_CI_AS"                       |             |
| /SQLSVCACCOUNT="NT Service\MSSQLSERVER"                            |             |
| /SQLSYSADMINACCOUNTS=Administrators                                |             |
| /IACCEPTSQLSERVERLICENSETERMS                                      |             |

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `require-msssql` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-mssql"></a>MSSQL をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "require-mssql",
            "input": "install",
        }
    ]
}
```