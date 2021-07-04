---
title: サービス ベースライン使用時の Visual Studio の更新
description: サービス ベースライン使用時の Visual Studio の更新方法について学習します。
ms.date: 07/17/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
monikerRange: '>=vs-2019'
ms.openlocfilehash: 03a192657a46c2db15cb2d1121735905f06da478
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306671"
---
# <a name="update-visual-studio-while-on-a-servicing-baseline"></a>サービス ベースライン使用時の Visual Studio の更新

Visual Studio は、製品のライフサイクルの間に頻繁に更新されます。 2 種類の更新があります。

* **マイナー リリース更新**&mdash; たとえば、16.0 から 16.1 &mdash; 新しい機能とコンポーネントが含まれます。  
* **サービス更新** — たとえば、16.0.4 から 16.0.5 — 重要な問題だけに対象を絞った修正が含まれます。

エンタープライズ管理者は、各クライアントをサービス ベースラインに留めることを選択できます。 サービス ベースラインは、次のサービス ベースラインのリリースから 1 年間、サービス更新プログラムによりサポートされます。

サービス ベースラインのオプションによって、開発者と管理者は、新しいマイナー更新プログラムに含まれる新機能、バグの修正、またはコンポーネントを、より柔軟に採用できるようになります。 最初のサービス ベースラインは 16.0.x です。 詳細については、「[Enterprise および Professional のお客様向けのサポート オプション](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers)」をご覧ください。

## <a name="how-to-get-onto-a-servicing-baseline"></a>サービス ベースラインの使用を始める方法

サービス ベースラインの使用を開始するには、[My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0) から修正済みバージョンの Visual Studio インストーラーのブートストラップをダウンロードします。 このブートストラップには、その特定のバージョンの製品の構成、ワークロード、およびコンポーネントへのリンクが含まれています。

> [!NOTE]
> 修正済みバージョンのブートストラップと標準のブートストラップを区別するよう注意してください。 標準のブートストラップは、入手可能な最新リリースの Visual Studio を使うよう構成されています。 標準のブートストラップを My.VisualStudio.com からダウンロードした場合、そのファイル名に番号が記載されています (例: vs_enterprise__123456789-123456789.exe)。

エンタープライズ管理者は、インストール中に各クライアントを構成して、クライアントが最新リリースに更新できないようにする必要があります。 これにはいくつかの方法があります。
- [応答の構成ファイルで `channelUri` 設定を変更](update-servicing-baseline.md#install-a-servicing-baseline-on-a-network)して、レイアウトまたはローカル フォルダーでチャネル マニフェストを使用する。
- [コマンドライン実行を使って channelUri を変更](update-servicing-baseline.md#install-a-servicing-baseline-via-the-internet)し、存在しないファイルを使用する。
- [更新プログラムを無効にするようクライアント システム上のポリシーを設定](update-servicing-baseline.md#use-policy-settings-to-disable-clients-from-updating)し、クライアントが自己更新できないようにします。

### <a name="install-a-servicing-baseline-on-a-network"></a>ネットワーク上のサービス ベースラインをインストールする

ネットワーク レイアウト インストールを使う管理者は、レイアウトの *response.json* ファイルの `channelUri` の値を変更して、同じフォルダー内にある *channelmanifest.json* ファイルを使うようにする必要があります。 従う手順については、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」をご覧ください。 `channelUri` の値を変更すると、クライアントがレイアウトの場所で更新プログラムを検索できるようになります。

### <a name="install-a-servicing-baseline-via-the-internet"></a>インターネット経由でサービス ベースラインをインストールする

インターネット ベースのインストールを行う場合は、セットアップを起動するために使うコマンドラインに、`--channelUri` と存在しないチャンネル マニフェストを追加します。 これにより、Visual Studio の更新で入手可能な最新リリースを使えないようになります。 次に例を示します。

```shell
vs_enterprise.exe --channelUri c:\doesnotexist.chman
```

### <a name="use-policy-settings-to-disable-clients-from-updating"></a>ポリシーの設定を使ってクライアントが更新できないようにする

クライアントの更新を制御するもう一つのオプションは、[更新通知をオフにする](controlling-updates-to-visual-studio-deployments.md)ことです。 インストールで channelUri 値が変更されていなかった場合は、このオプションを使います。 これで、クライアントが入手可能な最新リリースへのリンクを受信できなくなります。 修正済みバージョンのブートストラップは、クライアントで特定のバージョンに更新するために引き続き必要です。

## <a name="how-to-stay-on-a-servicing-baseline"></a>サービス ベースラインを使い続ける方法

サービス ベースライン用の更新プログラムを入手できる場合、[My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0) でサービス更新プログラム用に修正済みバージョンのブートストラップ ファイルを入手できます。

ネットワーク レイアウト インストールを使って配置を行う管理者の場合、管理者は[レイアウトの場所](update-a-network-installation-of-visual-studio.md)を更新する必要があります。 その場所からインストールしたクライアントは、更新通知を受け取ります。 更新をクライアントに配置する必要がある場合は、[こちらの手順](update-a-network-installation-of-visual-studio.md#deploy-an-update-to-client-machines)に従ってください。 更新用の "response.json" を変更する場合は、新しいワークロード、コンポーネント、または言語を追加しないでください。 製品を更新した後は、このような設定の管理は配置の '変更' として実行する必要があります。

インターネット ベースのインストールの場合は、新しい修正済みバージョンのブートストラップを、クライアント上の存在しないチャネル マニフェストを指す `--channelUri` パラメーターと共に実行します。 Quiet または受動モードで更新プログラムを配置する場合は、2 つの別々のコマンドを使います。

1. Visual Studio インストーラーを更新する。

    ```shell
    vs_enterprise.exe --quiet --update
    ```

::: moniker range="vs-2019"
 
2. Visual Studio アプリケーション自体を更新する。
    ```shell
    vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

::: moniker-end

::: moniker range=">=vs-2022"

2. Visual Studio アプリケーション自体を更新する。
    ```shell
    vs_enterprise.exe update --installPath "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio インスタンスの検出および管理用のツール](tools-for-managing-visual-studio-instances.md)
* [応答ファイルの設定を定義する方法](automated-installation-with-response-file.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
