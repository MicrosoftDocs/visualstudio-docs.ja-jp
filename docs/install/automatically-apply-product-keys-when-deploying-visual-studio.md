---
title: プロダクト キーを自動的に適用する
description: Visual Studio を展開するときに、プロダクト キーをプログラムで適用する方法を説明します。
ms.date: 09/24/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: d79260be-6234-4fd3-89b5-a9756b4a93c1
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: a78da89d8e8ce4251bc9288270628bfe784eca7a
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307719"
---
# <a name="automatically-apply-product-keys-when-deploying-visual-studio"></a>Visual Studio の展開時にプロダクト キーを自動的に適用する

Visual Studio の配置を自動化するために使用されるスクリプトの一部として、プログラム的にプロダクト キーを適用することができます。 プロダクト キーは、Visual Studio のインストール中またはインストール完了後に、プログラム的にデバイスで設定できます。

::: moniker range=">=vs-2022"

> [!IMPORTANT]
> Visual Studio 2022 は現在、プレビュー段階にあります。プレビュー期間中、Visual Studio 2022 は評価ライセンスで利用できますが、これにはプロダクト キーを適用する必要がありません。

::: moniker-end

::: moniker range="vs-2017"

## <a name="apply-the-license-after-installation"></a>インストール後にライセンスを適用する

ターゲット コンピューターにある `StorePID.exe` ユーティリティをサイレント モードで使用して、インストールされているバージョンの Visual Studio をプロダクト キーでアクティブにすることができます。 `StorePID.exe` は次の既定の場所に Visual Studio 2017 をインストールするユーティリティ プログラムです。

```shell
C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE
```

 System Center エージェントまたは管理者特権でのコマンド プロンプトを使用して、昇格された特権で `StorePID.exe` を実行します。 これに続いてプロダクト キーと Microsoft 製品コード (MPC) を入力します。

>[!IMPORTANT]
> プロダクト キーには、ダッシュ (-) を含めてください。

 ```shell
 StorePID.exe [product key including the dashes] [MPC]
 ```

::: moniker-end

::: moniker range="vs-2019"

## <a name="apply-the-license-after-installation"></a>インストール後にライセンスを適用する

ターゲット コンピューターにある `StorePID.exe` ユーティリティをサイレント モードで使用して、インストールされているバージョンの Visual Studio をプロダクト キーでアクティブにすることができます。 `StorePID.exe` は、次の既定の場所に Visual Studio 2019 と共にインストールされるユーティリティ プログラムです。

```shell
C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE
```

 System Center エージェントまたは管理者特権でのコマンド プロンプトを使用して、昇格された特権で `StorePID.exe` を実行します。 これに続いてプロダクト キーと Microsoft 製品コード (MPC) を入力します。

>[!IMPORTANT]
> プロダクト キーには、ダッシュ (-) を含めてください。

 ```shell
 StorePID.exe [product key including the dashes] [MPC]
 ```

::: moniker-end

::: moniker range="vs-2017"

次の例は Visual Studio 2017 Enterprise にライセンスを適用するコマンド ラインです。MPC は 08860 で、プロダクト キーは `AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE` です。既定の場所にインストールするものと想定しています。

```shell
"C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\StorePID.exe" AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 08860
```

::: moniker-end

::: moniker range="vs-2019"

次の例は、Visual Studio 2019 Enterprise にライセンスを適用するコマンド ラインを示しています。ここでは、MPC は 09260、プロダクト キーは `AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE` で、既定の場所へのインストールを想定しています。

```shell
"C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\StorePID.exe" AAAAA-BBBBB-CCCCC-DDDDDD-EEEEEE 09260
```

::: moniker-end

::: moniker range="vs-2017"

 次の表に、Visual Studio の各エディションの MPC コードを一覧します。

| Visual Studio エディション                | MPC   |
|--------------------------------------|-------|
| Visual Studio Enterprise 2017        | 08860 |
| Visual Studio Professional 2017      | 08862 |
| Visual Studio Test Professional 2017 | 08866 |

::: moniker-end

::: moniker range="vs-2019"

| Visual Studio エディション                | MPC   |
|--------------------------------------|-------|
| Visual Studio Enterprise 2019        | 09260 |
| Visual Studio Professional 2019      | 09262 |

::: moniker-end

::: moniker range="vs-2017"

`StorePID.exe` が正常にプロダクト キーを適用した場合は `%ERRORLEVEL%` として 0 を返します。 エラーが発生した場合、エラーの状態に基づいて次のいずれかのコードが返されます。

| エラー                     | コード |
|---------------------------|------|
| `PID_ACTION_SUCCESS`      | 0    |
| `PID_ACTION_NOTINSTALLED` | 1    |
| `PID_ACTION_INVALID`      | 2    |
| `PID_ACTION_EXPIRED`      | 3    |
| `PID_ACTION_INUSE`        | 4    |
| `PID_ACTION_FAILURE`      | 5    |
| `PID_ACTION_NOUPGRADE`    | 6    |

> [!NOTE]
> Visual Studio の仮想インスタンスを実行する場合は、ローカル AppData フォルダーとレジストリも仮想化してください。 仮想インスタンスのトラブルシューティングを行うには、`<Visual Studio installation directory>\Common7\IDE\DDConfigCA.exe` を実行します。  

::: moniker-end

::: moniker range="vs-2019"

`StorePID.exe` が正常にプロダクト キーを適用した場合は `%ERRORLEVEL%` として 0 を返します。 エラーが発生した場合、エラーの状態に基づいて次のいずれかのコードが返されます。

| エラー                     | コード |
|---------------------------|------|
| `PID_ACTION_SUCCESS`      | 0    |
| `PID_ACTION_NOTINSTALLED` | 1    |
| `PID_ACTION_INVALID`      | 2    |
| `PID_ACTION_EXPIRED`      | 3    |
| `PID_ACTION_INUSE`        | 4    |
| `PID_ACTION_FAILURE`      | 5    |
| `PID_ACTION_NOUPGRADE`    | 6    |

> [!NOTE]
> Visual Studio の仮想インスタンスを実行する場合は、ローカル AppData フォルダーとレジストリも仮想化してください。 仮想インスタンスのトラブルシューティングを行うには、`<Visual Studio installation directory>\Common7\IDE\DDConfigCA.exe` を実行します。  

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](../install/install-visual-studio.md)
* [Visual Studio のオフライン インストールを作成する](../install/create-an-offline-installation-of-visual-studio.md)