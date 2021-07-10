---
title: 配置の更新プログラムを制御する
description: ネットワークからインストールするときに、Visual Studio が更新プログラムを検索する場所を変更する方法を説明します。
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 35C7AB05-07D5-4B38-BCAC-AB88444E7368
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: f15281db55381dadbfd3370eb10a04feeab9c3a5
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307571"
---
# <a name="control-updates-to-network-based-visual-studio-deployments"></a>ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する

企業の管理者は、多くの場合、レイアウトを作成してそれをネットワーク ファイル共有でホストし、エンド ユーザーに展開します。 このページでは、ネットワーク レイアウト オプションを適切に構成する方法について説明します。

## <a name="controlling-where-visual-studio-looks-for-updates"></a>Visual Studio が更新プログラムを探す場所を変更する

**シナリオ 1: クライアントは元々レイアウトからインストールされましたが、ネットワーク レイアウトの場所または Web のいずれかから更新プログラムを受け取るように構成されています**

既定では、インストールが元々はネットワーク共有から展開された場合でも、Visual Studio によりオンラインで更新プログラムの検索が続けられます。 Web 上に更新プログラムがある場合は、ユーザーはそれをインストールできます。 ネットワーク レイアウト キャッシュは、更新された製品ビットがないか最初に検査されますが、そこで見つからない場合、Visual Studio によって更新された製品ビットが検索され、Web からダウンロードされます。

**シナリオ 2: クライアントが元々インストールされており、ネットワーク レイアウトからのみ更新プログラムを受け取る必要があります**

Visual Studio クライアントによって更新プログラムを検索する場所を制御する場合、たとえば、クライアント コンピューターからインターネットにアクセスできず、確実にレイアウトからのみインストールする場合は、クライアントのインストーラーによって更新された製品ビットが検索される場所を構成することができます。 クライアントによってレイアウトから初期インストールが行われる前に、この設定が正しく構成されていることを確認することをお勧めします。

1. オフライン レイアウトを作成します。

   ```shell
   vs_enterprise.exe --layout C:\vsoffline --lang en-US
   ```

2. それをホストするファイル共有にコピーします。

   ```shell
   xcopy /e C:\vsoffline \\server\share\VS
   ```

3. レイアウトの `response.json` ファイルを変更し、管理者が制御する channelManifest.json のコピーを指すように `channelUri` 値を変更します。

   値のバックスラッシュは、次の例のように必ずエスケープしてください。

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

   これでエンド ユーザーはこの共有からセットアップを実行し、Visual Studio をインストールできます。

   ```shell
   \\server\share\VS\vs_enterprise.exe
   ```

企業の管理者はユーザーが新しいバージョンの Visual Studio に更新する時期が来たと判断したとき、[レイアウトの場所を更新し](update-a-network-installation-of-visual-studio.md)、次のようにして更新されたファイルを組み込むことができます。

1. 次のようなコマンドを使用します。

   ```shell
   vs_enterprise.exe --layout \\server\share\VS --lang en-US
   ```

2. 更新後のレイアウトの `response.json` ファイルに、カスタマイズ内容が引き続き含まれているようにします。特に次のような channelUri の変更内容です。

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

このレイアウトからの既存の Visual Studio インストールは `\\server\share\VS\ChannelManifest.json` で更新プログラムを探します。 この channelManifest.json がユーザーがインストールしているものより新しい場合、Visual Studio は更新プログラムが利用できることをユーザーに通知します。

クライアントから開始されたインストールの更新プログラムにより、更新されたバージョンの Visual Studio がレイアウトから直接自動的にインストールされます。

**シナリオ 3: クライアントは元々Web からインストールされていましたが、現在はネットワーク レイアウトからの更新プログラムのみを受け取る必要があります**

場合によっては、クライアント コンピューターに既に Web から Visual Studio がインストールされている可能性がありますが、管理者は、今後のすべての更新プログラムを管理されたレイアウトから取得することを希望しています。 これを行うためにサポートされている唯一の方法は、目的のバージョンの製品を使用してネットワーク レイアウトを作成し、クライアント コンピューター上で、"_レイアウトの場所から_" ブートストラップを実行することです (例: `\\server\share\vs_enterprise.exe`)。 理想的には、元のクライアントのインストールは、ChannelURI が正しく構成されたネットワーク レイアウトからブートストラップを使用して行われるべきですが、ネットワーク レイアウトの場所から更新されたブートストラップを実行することもできます。 どちらの操作でも、クライアント コンピューター上に特定のレイアウトの場所との接続が組み込まれます。 このシナリオが正しく機能するための唯一の注意点は、レイアウトの `response.json` ファイルの "ChannelURI" が、最初のインストールが行われたときにクライアントのマシンに設定された ChannelURI と同じである必要があることです。 ほとんどの場合、この値は元々インターネットの[リリース チャネル](https://aka.ms/vs/16/release/channel)に設定されていました。

## <a name="controlling-notifications-in-the-visual-studio-ide"></a>Visual Studio IDE の通知を制御する

::: moniker range="vs-2017"

上述のとおり、Visual Studio はそのインストール元である場所 (ネットワーク共有やインターネットなど) で更新プログラムが利用できないか確認します。 更新プログラムが利用可能になると、Visual Studio は、ユーザーへの通知としてウィンドウの右上隅に通知フラグを表示します。

   ![更新プログラムの通知フラグ](media/notification-flag.png)

::: moniker-end

::: moniker range=">=vs-2019"

上述のとおり、Visual Studio はそのインストール元である場所 (ネットワーク共有やインターネットなど) で更新プログラムが利用できないか確認します。 更新プログラムが利用可能になると、Visual Studio では、ユーザーへの通知としてウィンドウの右下隅に通知アイコンが表示されます。

   ![Visual Studio IDE の通知アイコン](media/vs-2019/notification-bar.png "Visual Studio IDE の通知アイコン")

::: moniker-end

エンド ユーザーに更新プログラムを通知したくない場合は、通知を無効にすることができます。 (たとえば、中央のソフトウェア配布メカニズムを使用して更新プログラムを提供する場合、通知を無効にしたい場合があります。)

::: moniker range="vs-2017"

Visual Studio 2017 は[プライベート レジストリにレジストリ エントリを保存する](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)ので、そのレジストリを通常の方法で直接編集することはできません。 ただし、Visual Studio には `vsregedit.exe` ユーティリティが含まれます。これを利用し、Visual Studio 設定を変更できます。 次のコマンドで通知をオフにできます。

```shell
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 2019 は[プライベート レジストリにレジストリ エントリを保存する](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)ので、そのレジストリを通常の方法で直接編集することはできません。 ただし、Visual Studio には `vsregedit.exe` ユーティリティが含まれます。これを利用し、Visual Studio 設定を変更できます。 次のコマンドで通知をオフにできます。

```shell
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

::: moniker range=">=vs-2022"

Visual Studio 2022 は[プライベート レジストリにレジストリ エントリを保存する](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)ので、そのレジストリを通常の方法で直接編集することはできません。 ただし、Visual Studio には `vsregedit.exe` ユーティリティが含まれます。これを利用し、Visual Studio 設定を変更できます。 次のコマンドで通知をオフにできます。

```shell
vsregedit.exe set "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

(編集したいインストール済みのインスタンスと一致するようにディレクトリを置き換えてください。)

> [!TIP]
> [vswhere.exe](tools-for-managing-visual-studio-instances.md#detecting-existing-visual-studio-instances) を利用し、クライアント ワークステーションで特定のインスタンスの Visual Studio を見つけます。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [管理者の更新を有効にする](enabling-administrator-updates.md)
* [管理者の更新を適用する](applying-administrator-updates.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio インスタンスの管理用のツール](tools-for-managing-visual-studio-instances.md)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
