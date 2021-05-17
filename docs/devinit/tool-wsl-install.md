---
title: wsl-install
description: devinit ツール wsl-install。
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
ms.openlocfilehash: 4dff121d7866918d5c30986dc9bd4c3cab039ac5
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "108635350"
---
# <a name="wsl-install"></a>wsl-install

> [!IMPORTANT]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 その一環として、`devinit` と関連ツールは利用できなくなります。 今後のプレビューとロードマップの情報のために、Visual Studio の開発者コミュニティ フォーラムに参加することをお勧めします。

`wsl-install` ツールは、[Linux 用 Windows サブシステム](/windows/wsl/) (WSL) 向けの Linux ディストリビューションをインストールするために使用されます。

> [!IMPORTANT]
> `wsl-install` ツールを使用するには、Windows で WSL 2 が既に有効になっている必要があります。 何らかの理由で WSL 2 が有効になっていない場合は、[WSL のインストールに関するドキュメント](https://docs.microsoft.com/windows/wsl/install-win10)を参照してください。 また、[windowsfeature-enable](tool-windowsfeature-enable.md) ツールを使用して、必要なすべての Windows 機能を有効にすることもできます。

## <a name="usage"></a>使用方法

`input` と `additionalOptions` の両方のプロパティが省略されているか空の場合、ツールは次に示す[既定の](#default-behavior)動作に従います。

| 名前                                             | Type   | 必須 | 値                                                             |
|--------------------------------------------------|--------|----------|-------------------------------------------------------------------|
| **コメント**                                     | string | No       | comments は省略可能なプロパティです。 使用しません。                             |
| [**input**](#input)                              | string | はい      | インストールするディストリビューション。 詳細については、下の「[入力](#input)」を参照してください。     |
| [**additionalOptions**](#additional-options)     | string | No       | 詳細については、下の「[追加オプション](#additional-options)」を参照してください。  |

### <a name="input"></a>入力

デプロイするディストリビューションが含まれている AppX アプリケーション配布パッケージ (`.appx`) の URI。 URI の指す `.appx` アーカイブには、アーカイブのルートまたは内部 `.appx` アーカイブ内に `install.tar.gz` が 1 つだけ含まれている必要があります。 サポートされているディストリビューションの例を次に示します。

| ディストリビューション                          | Uri                                                           |
|---------------------------------|---------------------------------------------------------------|
| Ubuntu 20.04                    | https://aka.ms/wslubuntu2004                                  |
| Ubuntu 18.04                    | https://aka.ms/wsl-ubuntu-1804                                |
| Ubuntu 16.04                    | https://aka.ms/wsl-ubuntu-1604                                |
| Debian GNU/Linux                | https://aka.ms/wsl-debian-gnulinux                            |
| Kali Linux                      | https://aka.ms/wsl-kali-linux-new                             |
| OpenSUSE Leap 42                | https://aka.ms/wsl-opensuse-42                                |
| SUSE Linux Enterprise Server 12 | https://aka.ms/wsl-sles-12                                    |

> [!NOTE]
> ARM Linux ディストリビューションは、GitHub Codespaces では現在サポートされていません。

### <a name="additional-options"></a>追加オプション

複数の追加オプションがサポートされています。

| 名前                      | Type      | 必須 | 値                                                                                                                                                                                    |
|---------------------------|-----------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| --wsl-version             | string    | No       | 使用する WSL のバージョン。 既定値は 2 です。                                                                                                                                  |
| --post-create-command     | string    | No       | インストールが完了した後に Linux ディストリビューション内で実行するコマンド。 コマンドは、1 単語として書式設定するか、引用符で囲む必要があります。 既定では、コマンドはありません。  |

### <a name="default-behavior"></a>既定の動作

`input` プロパティ (インストールするディストリビューション) は必須であり、`wsl-install` ツールの既定の動作はエラーを出すことになります。

## <a name="example-usage"></a>使用例
`.devinit.json` を使用して `wsl-install` を実行する方法の例を次に示します。

#### <a name="devinitjson-that-will-install-ubuntu-2004"></a>Ubuntu 20.04 をインストールする .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-ubuntu-2004-and-perform-a-post-create-command"></a>Ubuntu 20.04 をインストールし、作成後コマンドを実行する .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'echo Hello from Ubuntu!'"
        }
    ]
}
```

#### <a name="devinitjson-that-will-install-ubuntu-2004-and-perform-a-post-create-command-that-configures-the-packages-listed"></a>Ubuntu 20.04 をインストールし、一覧表示されているパッケージを構成する作成後コマンドを実行する .devinit.json:
```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "run": [
        {
            "tool": "wsl-install",
            "input": "https://aka.ms/wslubuntu2004",
            "additionalOptions": "--wsl-version 2 --post-create-command 'apt-get update && apt-get install g++ gcc g++-9 gcc-9 cmake gdb ninja-build zip rsync -y'"
        }
    ]
}
```
