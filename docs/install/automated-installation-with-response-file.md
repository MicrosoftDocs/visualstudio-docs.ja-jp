---
title: 応答ファイルでインストールを自動化する
description: Visual Studio のインストールの自動化に役立つ JSON 応答ファイルを作成する方法について説明します
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- response file
- automate
- installation
- command-line
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: fe1d1a3c5ec13995cb69fff6ba6ec74c7a6c90d9
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307725"
---
# <a name="automate-installs-by-using-settings-in-a-response-file"></a>応答ファイルの設定を利用し、インストールを自動化する

Visual Studio を展開する管理者は、次の例のように `--in` パラメーターを使用して応答ファイルを指定できます。

```shell
vs_enterprise.exe --in customInstall.json
```

応答ファイルは、その内容がコマンド ライン引数を反映する [JSON](http://json-schema.org/) ファイルです。  一般的に、コマンド ライン パラメーターが引数を取らない場合 (`--quiet` や `--passive` など)、応答ファイルの値は true/false にしてください。  引数を取る場合 (`--installPath <dir>` など)、応答ファイルの値は文字列にしてください。  引数を取り、コマンド ラインに何回も出てくる場合 (`--add <id>` など)、文字列の配列にしてください。

コマンド ラインで指定されているパラメーターは、パラメーターが複数入力を受け付ける場合 (`--add` など) を除き、応答ファイルの設定をオーバーライドします。 複数入力がある場合、コマンドラインで指定された入力が応答ファイルの設定と結合されます。

## <a name="setting-a-default-configuration-for-visual-studio"></a>Visual Studio の既定構成を設定する

`--layout` でネットワーク レイアウト キャッシュを作成した場合、最初の `response.json` ファイルがレイアウトで作成されます。 部分的レイアウトを作成する場合、この応答ファイルにはレイアウトに含まれていたワークロードと言語が含まれます。  このレイアウトからセットアップを実行すると、自動的にこの response.json ファイルが使用され、レイアウトに含まれていたワークロードとコンポーネントが選択されます。  ユーザーは Visual Studio をインストールする前にセットアップ UI の任意のワークロードを引き続き選択または選択解除できます。

レイアウトを作成する管理者はレイアウトの `response.json` ファイルを変更することで、ユーザーがレイアウトから Visual Studio をインストールするときに表示される既定の設定を制御できます。  たとえば、管理者が特定のワークロードとコンポーネントを既定でインストールする場合、それらを追加するように `response.json` ファイルを構成できます。

Visual Studio セットアップをレイアウト フォルダーから実行すると、レイアウト フォルダーの応答ファイルが _自動的に_ 使用されます。  `--in` オプションを使用する必要はありません。

オフライン レイアウト フォルダーで作成された `response.json` ファイルを更新することで、このレイアウトからインストールするユーザーの既定設定を定義できます。

> [!WARNING]
> レイアウトが作成されたときに定義された既存プロパティをそのままにすることが重要です。

レイアウトの基本 `response.json` ファイルは、次の例のようになります。ただし、インストールする製品とチャネルの値は異なります。

::: moniker range="vs-2017"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

::: moniker range=">=vs-2019"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/16/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.16.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

レイアウトを作成または更新すると、response.template.json ファイルも作成されます。  このファイルには、使用できるワークロード、コンポーネント、言語 ID がすべて含まれています。  このファイルは、カスタム インストールに含められるものすべてのテンプレートとして提供されます。  管理者は、このファイルを元にカスタム応答ファイルを作成できます。  インストール対象でないものの ID を削除して、自分の応答ファイルに保存するだけです。  response.template.json をカスタマイズしないでください。レイアウトが更新されるたびに変更内容が失われます。

## <a name="example-layout-response-file-content"></a>レイアウト応答ファイルの内容の例

次の例では、Visual Studio Enterprise、6 つの共通ワークロード、コンポーネントがインストールされます。UI 言語として英語とフランス語の両方がインストールされます。 これをテンプレートとして利用できます。ワークロードとコンポーネントを自分がインストールするものに変更してください。

::: moniker range="vs-2017"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2017",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

::: moniker-end

::: moniker range=">=vs-2019"

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/16/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.16.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2019",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)
* [Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング](troubleshooting-network-related-errors-in-visual-studio.md)
