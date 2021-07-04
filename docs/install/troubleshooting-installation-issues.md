---
title: インストールまたはアップグレードの問題をトラブルシューティングする
description: ときには、問題が発生してしまうことがあります。 Visual Studio のインストールまたはアップグレードが失敗した場合、このページが役に立ちます。
ms.date: 06/24/2020
ms.custom: vs-acquisition
ms.topic: troubleshooting
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 556EDD3F-E365-43EE-B3DD-03AA4353F75B
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 802e4cfb78a9302bd24bca55cda1bf9eab79f9ef
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387828"
---
# <a name="troubleshoot-visual-studio-installation-and-upgrade-issues"></a>Visual Studio のインストールとアップグレードの問題のトラブルシューティング

> [!IMPORTANT]
> インストールに関する問題がある場合、 Microsoft によるサポートを受けられます。 [**インストール チャット**](https://visualstudio.microsoft.com/vs/support/#talktous) (英語のみ) のサポート オプションが用意されています。

このトラブルシューティング ガイドには、インストールに関する問題のほとんどを解決できるステップ バイ ステップの手順が含まれています。

## <a name="online-installations"></a>オンライン インストール

次の手順は、通常のオンライン インストール用に最適化されています。 オフライン インストールに影響を与える問題については、「[オフライン インストールのトラブルシューティング方法](#offline-installations)」をご覧ください。

### <a name="step-1---check-whether-this-problem-is-a-known-issue"></a>手順 1 - この問題が既知の問題であるかどうかを確認する

::: moniker range="vs-2017"

Visual Studio インストーラーには、Microsoft が修正に取り組んでいる問題がいくつかあります。 問題の回避策があるかどうか、[リリース ノートの既知の問題に関するセクション](/visualstudio/releasenotes/vs2017-relnotes#-known-issues)で確認してください。

::: moniker-end

::: moniker range=">=vs-2019"

Visual Studio インストーラーには、Microsoft が修正に取り組んでいる問題がいくつかあります。 問題の回避策があるかどうか、[リリース ノートの既知の問題に関するセクション](/visualstudio/releases/2019/release-notes#-known-issues)で確認してください。

::: moniker-end

### <a name="step-2---try-repairing-visual-studio"></a>手順 2 - Visual Studio の修復を試す

修復では、多くの一般的な更新プログラムの問題が修正されます。 Visual Studio で修復機能を使用する状況と方法の詳細については、「[Visual Studio の修復](repair-visual-studio.md)」を参照してください。

### <a name="step-3---check-with-the-developer-community"></a>手順 3 - 開発者コミュニティを確認する

[Visual Studio 開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)でエラー メッセージを検索します。 コミュニティの他のメンバーが、問題の解決策を文書化している可能性があります。

### <a name="step-4---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems"></a>手順 4 - Visual Studio インストーラーのディレクトリを削除してアップグレードの問題を修正する

Visual Studio インストーラーのブートストラップは、Visual Studio インストーラーの残りをインストールする最小限の軽量な実行可能ファイルです。 Visual Studio インストーラー ファイルを削除して、ブートストラップを再実行すると、いくつかの更新エラーを解決できる場合があります。

> [!NOTE]
> 次のアクションを実行すると、Visual Studio インストーラー ファイルが再インストールされ、インストール メタデータがリセットされます。

::: moniker range="vs-2017"

1. Visual Studio インストーラーを閉じます。
2. Visual Studio インストーラーのディレクトリを削除します。 通常、ディレクトリは `C:\Program Files (x86)\Microsoft Visual Studio\Installer` です。
3. Visual Studio インストーラーのブートストラップを実行します。 [ダウンロード] フォルダーのブートストラップのファイル名には `vs_[Visual Studio edition]__*.exe` のパターンが使用されている場合があります。 アプリケーションが見つからない場合は、「[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)」ページに移動し、Visual Studio のお使いのエディションの **[ダウンロード]** をクリックして、ブートストラップをダウンロードできます。 次に、実行可能ファイルを実行して、インストール メタデータをリセットします。
4. Visual Studio のインストールまたは更新を再度試します。 インストーラーのエラーが続く場合は、次の手順に進みます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio インストーラーを閉じます。
2. Visual Studio インストーラーのディレクトリを削除します。 通常、ディレクトリは `C:\Program Files (x86)\Microsoft Visual Studio\Installer` です。
3. Visual Studio インストーラーのブートストラップを実行します。 [ダウンロード] フォルダーのブートストラップのファイル名には `vs_[Visual Studio edition]__*.exe` のパターンが使用されている場合があります。 アプリケーションが見つからない場合は、「[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads)」ページに移動し、Visual Studio のお使いのエディションの **[ダウンロード]** をクリックして、ブートストラップをダウンロードできます。 次に、実行可能ファイルを実行して、インストール メタデータをリセットします。
4. Visual Studio のインストールまたは更新を再度試します。 インストーラーのエラーが続く場合は、次の手順に進みます。

::: moniker-end

### <a name="step-5---report-a-problem"></a>手順 5 - 問題を報告する

ファイルの破損など、一部の状況では、ケースごとに問題を調べる必要がある場合があります。 サポートに役立つように、次のことを実行します。

::: moniker range="vs-2017"

1. セットアップ ログを収集します。 詳細については、「[Visual Studio のインストール ログを取得する方法](#installation-logs)」をご覧ください。
2. Visual Studio インストーラーを開き、 **[問題の報告]** をクリックして、Visual Studio フィードバック ツールを開きます。
![[フィードバックの送信] ボタンからフィードバック ツールを開くことができます](media/report-a-problem.png)
3. 問題のレポートにタイトルを付け、関連する詳細を入力します。 **[次へ]** をクリックして **[添付ファイル]** セクションに移動し、生成されたログ ファイルを添付します (通常、ファイルは `%TEMP%\vslogs.zip` にあります)。
4. **[次へ]** をクリックして問題レポートを確認し、 **[送信]** をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. セットアップ ログを収集します。 詳細については、「[Visual Studio のインストール ログを取得する方法](#installation-logs)」をご覧ください。
2. Visual Studio インストーラーを開き、 **[問題の報告]** をクリックして、Visual Studio フィードバック ツールを開きます。
![[フィードバックの送信] ボタンからフィードバック ツールを開くことができます](media/vs-2019/vs-installer-report-problem.png)
3. 問題のレポートにタイトルを付け、関連する詳細を入力します。 **[次へ]** をクリックして **[添付ファイル]** セクションに移動し、生成されたログ ファイルを添付します (通常、ファイルは `%TEMP%\vslogs.zip` にあります)。
4. **[次へ]** をクリックして問題レポートを確認し、 **[送信]** をクリックします。

::: moniker-end

### <a name="step-6---run-installcleanupexe-to-remove-installation-files"></a>手順 6 - InstallCleanup.exe を実行してインストール ファイルを削除する

最後の手段として、[Visual Studio を削除](remove-visual-studio.md)し、すべてのインストール ファイルと製品情報を削除できます。

1. 「[Visual Studio の削除](remove-visual-studio.md)」の説明に従ってください。
2. 「[手順 4 - Visual Studio インストーラーのディレクトリを削除してアップグレードの問題を修正する](#step-4---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems)」で説明したブートストラップを再実行します。
3. Visual Studio のインストールまたは更新を再度試します。

### <a name="step-7---contact-us-optional"></a>手順 7 - 問い合わせる (省略可能)

前の手順のいずれに従っても Visual Studio のインストールまたはアップグレードに失敗する場合は、詳細なサポートのために [**ライブ チャット**](https://visualstudio.microsoft.com/vs/support/#talktous) サポート オプション (英語のみ) を使用してお問い合わせください。

## <a name="offline-installations"></a>オフライン インストール

[オフライン インストール](create-an-offline-installation-of-visual-studio.md)を作成して、ローカル レイアウトからインストールする際に役立つ可能性がある、既知の問題と回避策を次の表に示します。

| 懸案事項       | アイテム                   | ソリューション |
| ----------- | ---------------------- | -------- |
| ユーザーにファイルへのアクセス権がない。 | アクセス許可 (ACL) | オフライン インストールを共有する *前* に、他のユーザーに読み取りアクセス権を付与するように、必ずアクセス許可 (ACL) を調整してください。 |
| 新しいワークロード、コンポーネント、または言語をインストールできない。  | `--layout`  | 部分レイアウトからインストールし、その部分レイアウトには以前ダウンロードしなかったワークロード、コンポーネント、または言語を選択した場合は、インターネットにアクセスできることを確認してください。 |

[ネットワーク インストール](create-a-network-installation-of-visual-studio.md)に関する問題を解決する方法の詳細については、「[Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング](troubleshooting-network-related-errors-in-visual-studio.md)」を参照してください。

## <a name="installation-logs"></a>インストールのログ

セットアップ ログは、インストールに関する問題の多くをトラブルシューティングするために必要です。 Visual Studio インストーラーの [[問題の報告]](../ide/how-to-report-a-problem-with-visual-studio.md) を使用して問題を送信するとき、レポートには自動でこれらのログが含まれます。

Microsoft サポートに連絡する場合、[Microsoft Visual Studio と .NET Framework ログ収集ツール](https://www.microsoft.com/download/details.aspx?id=12493)を使用して、これらのセットアップ ログを提供する必要がある場合があります。 このログ収集ツールは、Visual Studio にインストールされている .NET Framework、Windows SDK、SQL Server などのすべてのコンポーネントからセットアップ ログを収集します。 また、コンピューター情報、Windows インストーラーのインベントリ、Visual Studio インストーラーの Windows イベント ログ情報、Windows インストーラー、システムの復元に関する情報を収集します。

ログを収集するには:

1. [ツールをダウンロード](https://www.microsoft.com/download/details.aspx?id=12493)します。
2. 管理コマンド プロンプトを開きます。
3. ツールを保存したディレクトリから `Collect.exe` を実行します。
4. `%TEMP%` ディレクトリで結果の `vslogs.zip` ファイルを探します (例: `C:\Users\YourName\AppData\Local\Temp\vslogs.zip`)。

> [!NOTE]
> このツールは、インストールの実行に失敗したときと同じユーザー アカウントで実行する必要があります。 別のユーザー アカウントでこのツールを実行する場合は、`–user:<name>` オプションを設定して、インストールの実行に失敗したユーザー アカウントを指定します。 追加オプションや使用に関する情報を収集するには、管理コマンド プロンプトで `Collect.exe -?` を実行します。

## <a name="live-help"></a>ライブ ヘルプ

このトラブルシューティング ガイドに記載されているソリューションの一覧に従っても Visual Studio のインストールまたはアップグレードに失敗する場合は、詳細なサポートのために [**ライブ チャット**](https://visualstudio.microsoft.com/vs/support/#talktous) サポート オプション (英語のみ) を使用してください。

## <a name="see-also"></a>関連項目

* [Visual Studio の修復](repair-visual-studio.md)
* [Visual Studio の削除](remove-visual-studio.md)
* [ファイアウォールまたはプロキシ サーバーの内側に Visual Studio および Azure Services をインストールして使用する](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Visual Studio インスタンスの検出および管理用のツール](tools-for-managing-visual-studio-instances.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
