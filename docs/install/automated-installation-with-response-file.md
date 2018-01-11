---
title: "応答ファイルで Visual Studio インストールを自動化する | Microsoft Docs"
description: "Visual Studio のインストールの自動化に役立つ JSON 応答ファイルを作成する方法について説明します"
ms.date: 08/14/2017
ms.reviewer: tims
ms.suite: 
ms.technology: vs-acquisition
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- response file
- automate
- installation
- command-line
author: timsneath
ms.author: tglee
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 8bb0cfca6efe913b38a94daf0ed846699f0266cd
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-define-settings-in-a-response-file"></a>応答ファイルの設定を定義する方法
Visual Studio を展開する管理者は、次の例のように `--in` パラメーターを使用して応答ファイルを指定できます。

```
vs_enterprise.exe --in customInstall.json
```

応答ファイルは、その内容がコマンド ライン引数を反映する [JSON](http://json-schema.org/) ファイルです。  一般的に、コマンド ライン パラメーターが引数を取らない場合 (`--quiet` や `--passive` など)、応答ファイルの値は true/false にしてください。  引数を取る場合 (`--installPath <dir>` など)、応答ファイルの値は文字列にしてください。  引数を取り、コマンド ラインに何回も出てくる場合 (`--add <id>` など)、文字列の配列にしてください。

コマンド ラインで指定されているパラメーターは、パラメーターが複数入力を受け付ける場合 (`--add` など) を除き、応答ファイルの設定を上書きします。 複数入力がある場合、コマンドラインで指定された入力が応答ファイルの設定と結合されます。

# <a name="setting-a-default-configuration-for-visual-studio"></a>Visual Studio の既定構成を設定する

`--layout` でネットワーク レイアウト キャッシュを作成した場合、最初の `response.json` ファイルがレイアウトで作成されます。 部分的レイアウトを作成する場合、この応答ファイルにはレイアウトに含まれていたワークロードと言語が含まれます。  このレイアウトからセットアップを実行すると、自動的にこの response.json ファイルが使用され、レイアウトに含まれていたワークロードとコンポーネントが選択されます。  ユーザーは Visual Studio をインストールする前にセットアップ UI の任意のワークロードを引き続き選択または選択解除できます。

レイアウトを作成する管理者はレイアウトの `response.json` ファイルを変更することで、ユーザーがレイアウトから Visual Studio をインストールするときに表示される既定の設定を制御できます。  たとえば、管理者が特定のワークロードとコンポーネントを既定でインストールする場合、それらを追加するように `response.json` ファイルを構成できます。

Visual Studio セットアップをレイアウト フォルダーから実行すると、レイアウト フォルダーの応答ファイルが_自動的に_使用されます。  `--in` オプションを使用する必要はありません。

オフライン レイアウト フォルダーで作成された `response.json` ファイルを更新することで、このレイアウトからインストールするユーザーの既定設定を定義できます。

> [!WARNING]
> レイアウトが作成されたときに定義された既存プロパティをそのままにすることが重要です。

レイアウトの基本 `response.json` ファイルは、次の例のようになります。ただし、インストールする製品とチャネルの値は異なります。

```json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```
レイアウトを作成または更新すると、response.template.json ファイルも作成されます。  このファイルには、使用できるワークロード、コンポーネント、言語 ID がすべて含まれています。  このファイルは、カスタム インストールに含められるものすべてのテンプレートとして提供されます。  管理者は、このファイルを元にカスタム応答ファイルを作成できます。  インストール対象でないものの ID を削除して、自分の応答ファイルに保存するだけです。  response.template.json をカスタマイズしないでください。レイアウトが更新されるたびに変更内容が失われます。

## <a name="example-layout-response-file-content"></a>レイアウト応答ファイルの内容の例
次の例では、Visual Studio Enterprise、6 つの共通ワークロード、コンポーネントがインストールされます。UI 言語として英語とフランス語の両方がインストールされます。 これをテンプレートとして利用できます。ワークロードとコンポーネントを自分がインストールするものに変更してください。

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

## <a name="get-support"></a>サポートを受ける
ときには、問題が発生してしまうことがあります。 Visual Studio のインストールが失敗した場合は、「[Troubleshooting Visual Studio 2017 installation and upgrade issues (Visual Studio 2017 のインストールとアップグレードの問題のトラブルシューティング)](troubleshooting-installation-issues.md)」ページをご覧ください。 トラブルシューティングの手順でも解決しない場合は、ライブ チャットでインストールの支援を依頼してください (英語のみ)。 詳細については、[Visual Studio のサポート ページ](https://www.visualstudio.com/vs/support/#talktous)をご覧ください。

他のいくつかのサポート オプションを次に示します。
* Visual Studio インストーラーおよび Visual Studio IDE の両方に表示される [[問題の報告]](../ide/how-to-report-a-problem-with-visual-studio-2017.md) ツールから、製品の問題を Microsoft に報告できます。
* [UserVoice](https://visualstudio.uservoice.com/forums/121579) で、製品に関する提案を投稿できます。
* [Visual Studio 開発者コミュニティ](https://developercommunity.visualstudio.com/)で製品の問題を追跡したり、質問したり、回答を検索したりできます。
* [Gitter コミュニティの Visual Studio に関する掲示板](https://gitter.im/Microsoft/VisualStudio)で、Microsoft や他の Visual Studio 開発者と情報を交換することもできます。  (このオプションでは [GitHub](https://github.com/) アカウントが必要になります)。

## <a name="see-also"></a>関連項目
* [Visual Studio 2017 のワークロード ID とコンポーネント ID](workload-and-component-ids.md)
