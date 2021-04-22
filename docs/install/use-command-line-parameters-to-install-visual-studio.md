---
title: コマンド ライン パラメーターを使用して Visual Studio をインストールする
titleSuffix: ''
description: コマンド ライン パラメーターを使用して、Visual Studio のインストールを制御またはカスタマイズする方法を説明します。
ms.date: 4/16/2021
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 23c83611e7663d35b229517f1e0224eb4ae7bb57
ms.sourcegitcommit: 367a2d9df789aa617abaa09b0cd0a18db7357d0c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107800820"
---
# <a name="use-command-line-parameters-to-install-visual-studio"></a>コマンド ライン パラメーターを使用して Visual Studio をインストールする

プログラムから、またはコマンド プロンプトから Visual Studio をインストールする場合、さまざまなコマンド ライン パラメーターを使用してインストールを管理またはカスタマイズし、以下のアクションを実行することができます。

- 事前に選択された特定のオプションと動作を使用して、クライアントでのインストールを開始する。
- インストール プロセスを自動化する。
- クライアント コンピューターをインストールまたは更新するための、製品ファイルのネットワーク レイアウトを作成または管理する。

コマンド ライン オプションは、セットアップ ブートストラップ (ダウンロード プロセスを開始する小さい (1 MB 未満の) ファイル)、または [Microsoft Update カタログ](https://catalog.update.microsoft.com)に展開される管理者向け更新プログラム パッケージで使用できます。 

::: moniker range="vs-2017"

Visual Studio 2017 バージョン 15.9 のブートストラップを入手するには、[**Visual Studio の以前のバージョン**](https://visualstudio.microsoft.com/vs/older-downloads/)のページに移動し、次のいずれかのブートストラップ ファイルをダウンロードします。

| エディション | ファイル名 |
|-------------|-----------------------|
|Visual Studio Enterprise 2017 バージョン 15.9 | vs_enterprise.exe |
|Visual Studio Professional 2017 バージョン 15.9 | vs_professional.exe |
|Visual Studio Build Tools 2017 バージョン 15.9  | vs_buildtools.exe |

::: moniker-end

::: moniker range="vs-2019"

[Visual Studio のダウンロード ページ](https://visualstudio.microsoft.com/downloads)または、「[Visual Studio 2019 リリース](https://docs.microsoft.com/visualstudio/releases/2019/history#installing-an-earlier-release)」のページから、ご自分で選択した Visual Studio のバージョンおよびエディション用の Visual Studio 2019 のブートストラップを入手できます。 お使いのセットアップ ファイル、またはブートストラップは、次のいずれか (あるいは同様) になります。

| Edition                    | ファイル                                                                    |
|----------------------------|-------------------------------------------------------------------------|
| Visual Studio 2019 Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019)     |
| Visual Studio 2019 Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019) |
| Visual Studio 2019 Build Tools   | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019)     |
| Visual Studio 2019 Community    | [vs_community.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019)  |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio のビルド番号とリリース日](visual-studio-build-numbers-and-release-dates.md)」ページを参照してください。

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>前にブートストラップ ファイルをダウンロードしてあり、そのバージョンを確認したい場合は、次のようにします。 Windows でエクスプローラーを開き、ブートストラップ ファイルを右クリックし、 **[プロパティ]** を選択して、 **[詳細]** タブを選択し、 **[製品バージョン]** の値を表示します。 この値に対応する Visual Studio のリリースを調べるには、「[Visual Studio 2019 リリース](https://docs.microsoft.com/visualstudio/releases/2019/history)」のページを参照してください。

::: moniker-end

管理者向け更新プログラムを入手するには、[Microsoft Update カタログ](https://catalog.update.microsoft.com)に移動し、インストールする更新プログラムを検索して、[ダウンロード] ボタンを押します。 管理者向け更新プログラムは、Visual Studio が既にコンピューターにインストールされていることを前提としています。 管理者向け更新プログラムを適用しても、まったく新しいインストールが開始されるわけではありません。

## <a name="bootstrapper-commands-and-command-line-parameters"></a>ブートストラップのコマンドとコマンド ライン パラメーター

製品をインストールしたり、レイアウトを維持したりするために、プログラムで Visual Studio ブートストラップを呼び出すときの最初のパラメーターは、実行する操作を記述するコマンド (動詞) です。 後続の省略可能なコマンド ライン パラメーター (すべて先頭に 2 つのダッシュ -- が付いている) によって、その操作がどのように行われるかがさらに定義されます。 Visual Studio のすべてのコマンド ライン パラメーターで大文字と小文字が区別されません。その他の例については、[コマンド ライン パラメーターの例](command-line-parameter-examples.md)に関する記事を参照してください。

構文例: `vs_enterprise.exe [command] <optional parameters>...`

| **コマンド** | **説明** |
| ----------------------- | --------------- |
| (空白) | 既定のコマンドはどちらも製品をインストールし、すべてのレイアウト メンテナンス操作に使用されます。 |
| `modify` | インストールされている製品を変更します。 |
| `update` | インストールされている製品を更新します。 |
| `repair` | インストールされている製品を修復します。 |
| `uninstall` | インストールされている製品をアンインストールします。 |
| `export` | インストールの選択をインストール構成ファイルにエクスポートします。 **注記**: vs_installer.exe でのみ使用できます。 |


| **パラメーター** | **説明** |
| ----------------------- | --------------- |
| `--installPath <dir>` | 既定の install コマンドの場合、このパラメーターは **省略可能** で、インスタンスがクライアント コンピューターのどこにインストールされるかを示します。 update や modify などの他のコマンドの場合、このパラメーターは **必須** であり、操作するインスタンスのインストール ディレクトリを示します。 |
| `--add <one or more workload or component IDs>` | **省略可能**: install または modify コマンドの実行中に、この反復可能なパラメーターでは、追加する 1 つ以上のワークロードまたはコンポーネント ID が指定されます。 成果物の必須のコンポーネントはインストールされますが、推奨されるコンポーネントまたは省略可能なコンポーネントはインストールされません。 `--includeRecommended` や `--includeOptional` のパラメーターを使用して、他のコンポーネントをグローバルに制御できます。 複数のワークロードやコンポーネントを含める場合、`--add` コマンドを繰り返します (例: `--add Workload1 --add Workload2`)。 詳細に制御するために、ID に `;includeRecommended` または `;includeOptional` を追加できます (例: `--add Workload1;includeRecommended` または `--add Workload2;includeRecommended;includeOptional`)。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 |
| `--remove <one or more workload or component IDs>` | **省略可能**: modify コマンドの実行中に、この反復可能なパラメーターでは、削除する 1 つ以上のワークロードまたはコンポーネント ID が指定されます。 これは、`--add` パラメーターと同じように補完および動作します。 |
| `--addProductLang <language-locale>` | **省略可能**: install または modify コマンドの実行中に、この反復可能なパラメーターでは、製品と共にインストールする必要がある UI 言語パックが指定されます。 存在しない場合、インストールでは、コンピューターのロケールに対応する言語パックが使用されます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--removeProductLang <language-locale>` | **省略可能**: install または modify コマンドの実行中に、この反復可能なパラメーターでは、製品から削除する必要がある UI 言語パックが決定されます。  これは、`--addProductLang` パラメーターと同じように補完および動作します。 |
| `--in <path>` | **省略可能**: 構成設定を含むことができる[応答ファイル](automated-installation-with-response-file.md)の URI またはパス。 |
| `--all` | **省略可能**: install または modify コマンドの実行中に、このパラメーターでは製品のすべてのワークロードとコンポーネントがインストールされます。 |
| `--allWorkloads` | **省略可能**: install または modify コマンドの実行中に、このパラメーターを指定すると、すべてのワークロードとコンポーネントがインストールされますが、推奨される、またはオプションのコンポーネントはインストールされません。 |
| `--includeRecommended` | **省略可能**: install または modify コマンドの実行中、このパラメーターには、インストールされているワークロードに対して推奨されるコンポーネントが含まれますが、オプションのコンポーネントは含まれません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。 |
| `--includeOptional` | **省略可能**: install または modify コマンドの実行中、このパラメーターには、インストールされているワークロードに対して省略可能なコンポーネントが含まれますが、推奨されるコンポーネントは含まれません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。  |
| `--quiet, -q` | **省略可能**: 任意のコマンドで使用します。このパラメーターにより、コマンドの実行中にユーザー インターフェイスが表示されなくなります。 |
| `--passive, -p` | **省略可能**: このパラメーターにより、ユーザー インターフェイスは非対話形式で表示されます。 このパラメーターは、`--quiet` パラメーターとは相互に排他的です (実際にはオーバーライドされます)。  |
| `--norestart` | **省略可能**: このパラメーターは、`--passive` または `--quiet` のいずれかのパラメーターと組み合わせる必要があります。  install、update、または modify コマンドの実行中に、`--norestart` パラメーターを追加すると、必要な再起動が遅延します。 |
| `--force` | **省略可能**: このパラメーターは、Visual Studio プロセスが使用されている場合でも、Visual Studio を強制的に閉じます。 |
| `--installWhileDownloading` | **省略可能**: install、update、または modify コマンドの実行中に、このパラメーターを指定すると、Visual Studio で製品を同時にダウンロードしてインストールすることができます。 これは既定のエクスペリエンスです。 |
| `--downloadThenInstall` | **省略可能**: install、update、または modify コマンドの実行中に、このパラメーターを指定すると、Visual Studio がすべてのファイルをインストール前に強制的にダウンロードします。 `--installWhileDownloading` パラメーターとは相互に排他的です。 |
| `--nickname <name>` | **省略可能**: install コマンドの実行時に、このパラメーターを実行するとインストールされている製品に割り当てるニックネームが定義されます。 ニックネームは 10 文字を超えることはできません。  |
| `--productKey` | **省略可能**: install コマンドの実行時に、このパラメーターを実行するとインストールされている製品に使用するプロダクト キーが定義されます。 `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx` または `xxxxxxxxxxxxxxxxxxxxxxxxx` のいずれかの形式の英数字 25 文字で構成されます。 |
| `--help, --?, -h, -?` | このページのオフライン バージョンが表示されます。 |
| `--config <path>` | **省略可能**: インストールまたは変更の操作中に、以前に保存したインストール構成ファイルに基づいて、追加するワークロードおよびコンポーネントが決定されます。 この操作は追加式で、ワークロードやコンポーネントがファイル内に存在しない場合、削除されることはありません。 また、製品に適用されない項目は追加されません。 エクスポート操作中に、インストール構成ファイルの保存場所を決定します。 |


> [!IMPORTANT]
> 複数の個別のワークロード、コンポーネント、または言語を指定する場合、項目ごとに `--add` または `--remove` のコマンド ライン スイッチを繰り返す必要があります。

## <a name="layout-command-and-command-line-parameters"></a>レイアウトのコマンドとコマンド ライン パラメーター
すべてのレイアウト管理操作は、コマンドが既定のインストール (空白) であることを前提としています。 そのため、すべてのレイアウト管理操作は、最初に必要な `--layout` パラメーターで始まる必要があります。  次の表は、コマンド ラインを使用してレイアウトを作成または更新するために使用できるその他のパラメーターについて説明しています。

| **レイアウト パラメーター** | **説明** |
| ----------------------- | --------------- |
| `--layout <dir>` | オフライン インストールのキャッシュを作成または更新するディレクトリを指定します。 詳細については、「[Visual Studio のネットワーク ベース インストールを作成する](create-a-network-installation-of-visual-studio.md)」をご覧ください。|
| `--lang <one or more language-locales>` | **省略可能**: `--layout` とともに使用して、指定した言語でのリソース パッケージによるオフライン インストール キャッシュを準備します。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--add <one or more workload or component IDs>` | **省略可能**: 1 つ以上のワークロード ID またはコンポーネント ID を追加します。 成果物の必須のコンポーネントはインストールされますが、推奨されるコンポーネントまたは省略可能なコンポーネントはインストールされません。 `--includeRecommended` や `--includeOptional` を使用して、他のコンポーネントをグローバルに制御できます。 詳細に制御するために、ID に `;includeRecommended` または `;includeOptional` を追加できます (例: `--add Workload1;includeRecommended` または `--add Workload2;includeOptional`)。 詳しくは、[ワークロード ID とコンポーネント ID](workload-and-component-ids.md) に関するページをご覧ください。 <br/>**注意**: `--add` を使用する場合、指定したワークロードとコンポーネント、およびその依存関係のみがダウンロードされます。 `--add` を指定しない場合は、すべてのワークロードとコンポーネントがレイアウトにダウンロードされます。|
| `--includeRecommended` | **省略可能**: インストールされているワークロードの推奨されるコンポーネントを含めますが、オプションのコンポーネントは含めません。 ワークロードは、`--allWorkloads` または `--add` のいずれかで指定されます。 |
| `--includeOptional` | **省略可能**: レイアウトに含まれるワークロードに、推奨 *および* 省略可能なコンポーネントが含まれます。 ワークロードは、`--add` で指定されます。  |
| `--keepLayoutVersion` | **省略可能**: レイアウトのバージョンを更新することなく、レイアウトに変更を適用します。 |
| `--verify` | **省略可能**: レイアウトの内容を確認します。 破損または欠落しているすべてのファイルが一覧に表示されます。 |
| `--fix` | **省略可能**: レイアウトの内容を確認します。  いずれかのファイルが破損または欠落している場合は、再ダウンロードします。 レイアウトを修正するには、インターネットへのアクセスが必要です。 |
| `--clean <one or more paths to catalogs>` | **省略可能**: 新しいバージョンに更新されたレイアウトから古いバージョンのコンポーネントを削除します。 |

| **高度なレイアウト パラメーター** | **説明** |
| ----------------------- | --------------- |
| `--channelId <id>` | **省略可能**: インストールするインスタンスのチャネル ID です。 インストール コマンドでは必須です。`--installPath` が指定されている場合、他のコマンドでは無視されます。 |
| `--channelUri <uri>` | **省略可能**: チャネル マニフェストの URI です。 更新が不要な場合、`--channelUri` で存在しないファイル (たとえば、--channelUri C:\doesntExist.chman) を指定できます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--installChannelUri <uri>` | **省略可能**: インストールに使用するチャネル マニフェストの URI です。 `--channelUri` で指定された URI (`--installChannelUri` を指定した場合は必ず指定する必要があります) は、更新プログラムを検出するために使用されます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--installCatalogUri <uri>` | **省略可能**: インストールに使用するカタログ マニフェストの URI です。 これを指定すると、チャネル マネージャーは、インストール チャネル マニフェストの URI を使用する前に、この URI からカタログ マニフェストをダウンロードしようとします。 このパラメーターは、レイアウトのキャッシュが既にダウンロードされている製品カタログで作成される、オフライン インストールをサポートするために使用されます。 インストール コマンドに使用できます。その他のコマンドでは無視されます。 |
| `--productId <id>` | **省略可能**: インストールされるインスタンスの製品 ID です。 これは、通常のインストール条件では事前に設定されています。 |
| `--wait` | **省略可能**: インストールが完了し、終了コードが返されるまでプロセスは待機します。 このオプションは、インストールが完了するまで待ってから、そのインストールからのリターン コードを処理する必要があるインストールの自動化に役立ちます。 |
| `--locale <language-locale>` | **省略可能**: インストーラー自体のユーザー インターフェイスの表示言語を変更します。 設定は保持されます。 詳しくは、このページの「[言語ロケールの一覧](#list-of-language-locales)」セクションをご覧ください。|
| `--cache` | **省略可能**: 指定した場合、インストールされた後、その後の修復用にパッケージが保持されます。 このオプションでは、その後のインストール、修復、または修正に使用されるグローバル ポリシー設定がオーバーライドされます。 既定のポリシーでは、パッケージをキャッシュします。 アンインストール コマンドでは、これは無視されます。 詳細については、「[disable or move the package cache](disable-or-move-the-package-cache.md)」 (パッケージ キャッシュの無効化または移動) を参照してください。 |
| `--nocache` | **省略可能**: 指定した場合、パッケージはインストールまたは修復された後、削除されます。 必要な場合にのみ、もう一度ダウンロードされ、使用後はもう一度削除されます。 このオプションでは、その後のインストール、修復、または修正に使用されるグローバル ポリシー設定がオーバーライドされます。 既定のポリシーでは、パッケージをキャッシュします。 アンインストール コマンドでは、これは無視されます。 詳細については、「[disable or move the package cache](disable-or-move-the-package-cache.md)」 (パッケージ キャッシュの無効化または移動) を参照してください。 |
| `--noUpdateInstaller` | **省略可能**: 指定した場合、quiet が指定されていると、インストーラーはインストーラー自体を更新しません。 インストーラーの更新が必要な場合に、noUpdateInstaller と quiet の両方が指定されていると、インストーラーはコマンドを失敗させて、0 以外の終了コードを返します。 |
| `--noWeb` | **省略可能**: 指定した場合、Visual Studio のセットアップでは、レイアウト ディレクトリにあるファイルを使って Visual Studio がインストールされます。 ユーザーがレイアウトに含まれないコンポーネントをインストールしようとした場合、セットアップは失敗します。  詳細については、「[ネットワーク インストールから展開する](create-a-network-installation-of-visual-studio.md)」をご覧ください。 <br/><br/> **重要**: この切り替えによって、Visual Studio のセットアップで更新プログラムのチェックが行われなくなることはありません。 詳細については、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」をご覧ください。 |
| `--path <name>=<path>` | **省略可能**: インストール用のカスタム インストール パスを指定するために使用します。 サポートされているパス名は、shared、cache、および install です。 |
| `--path cache=<path>` | **省略可能**: 指定した場所を使用してインストール ファイルがダウンロードされます。 この場所は、Visual Studio を初めてインストールするときにのみ設定することができます。 例: `--path cache="C:\VS\cache"` |
| `--path shared=<path>` | **省略可能**: Visual Studio のサイド バイ サイド インストール用の共有ファイルが含まれています。 ツールおよび SDK については、このドライブ上の場所にインストールされるものもあれば、この設定をオーバーライドして、別のドライブにインストールされるものもあります。 例: `--path shared="C:\VS\shared"` <br/><br/>**重要**: これは Visual Studio を初めてインストールするときに 1 回のみ設定できます。 |
| `--path install=<path>` | **省略可能**: `–-installPath` と等価です。 具体的には、`--installPath "C:\VS"` と `--path install="C:\VS"` が等価です。 これらのコマンドは、一度に 1 つしか使用できません。 |

## <a name="administrator-update-command-and-command-line-parameters"></a>管理者向け更新プログラムのコマンドとコマンド ライン パラメーター
[Microsoft Update カタログ](https://catalog.update.microsoft.com)からクライアント コンピューターのインストール ディレクトリに管理者向け更新プログラムをダウンロードする場合は、ファイルをダブルクリックするだけで更新プログラムを適用できます。 また、コマンド ウィンドウを開き、以下のパラメーターの一部を渡して、既定の動作を変更することもできます。 

Microsoft Endpoint Manager (SCCM) を使用して管理者向け更新プログラムを展開する場合は、次のパラメーターを使用して、パッケージを変更して動作を調整できます。 クライアント コンピューターの構成ファイルを使用してパラメーターを制御することもできます。 詳細については、「[管理者更新プログラムを構成する方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)」を参照してください

すべての管理者更新プログラムのパラメーターは、"更新" コンテキストで実行されることに注意してください。

| **管理者向け更新プログラムのパラメーター** | **説明** |
| ----------------------- | --------------- |
| `--installerUpdateArgs [optional parameters]` | このパラメーターは、管理者向け更新プログラムのシナリオに関連する特定のパラメーターの "パススルー配列" として機能します。 この目的で有効になっている省略可能なパラメーターは次のとおりです。 <br/><br/> `--quiet`: これは管理者向け更新プログラムの既定のエクスペリエンスであり、完全を期すためにここに記載されています。 <br/> `--passive`: このパラメーターは `--quiet` パラメーターをオーバーライドします。  これにより、UI が非対話的な方法で表示されます。 <br/>`--norestart`: このパラメーターは、`--quiet` または `--passive` と組み合わせて使用する必要があり、必要な再起動の遅延を引き起こします。 <br/>`--noWeb`: このパラメーターにより、Visual Studio が製品の更新プログラムをインターネット上で確認しなくなります。 <br/>`--force`: このパラメーターにより、Visual Studio が使用されている場合でも、Visual Studio が強制的に閉じられます。 このパラメーターは、作業が失われる可能性があるため、注意して使用してください。 このパラメーターは、ユーザー コンテキストで使用する必要があります。 <br/>`--installWhileDownloading`: このパラメーターにより、Visual Studio で製品のダウンロードとインストールが両方同時にできるようになります。 これは管理者向け更新プログラムの既定のエクスペリエンスであり、完全を期すためにここに記載されています。 <br/>`--downloadThenInstall`: このパラメーターを指定すると、Visual Studio はすべてのファイルをインストール前に強制的にダウンロードします。 `--installWhileDownloading` パラメーターとは相互に排他的です。 |
| `--checkPendingReboot` | コンピューターに保留中の再起動がある場合は、その原因がどのアプリケーションであるかにかかわらず、更新プログラムは中止されます。 既定では、保留中の再起動の有無はチェックされません。 |


構文例: `visualstudioupdate-16.9.0to16.9.4.exe --installerUpdateArgs=--force,--noWeb --checkPendingReboot`

## <a name="list-of-workload-ids-and-component-ids"></a>ワークロード ID とコンポーネント ID の一覧

Visual Studio 製品ごとに並べられているワークロード ID とコンポーネント ID の一覧については、「[Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)」のページをご覧ください。

## <a name="list-of-language-locales"></a>言語ロケールの一覧

| **言語ロケール** | **Language** |
| ----------------------- | --------------- |
| Cs-cz | チェコ語 |
| De-de | ドイツ語 |
| En-us | 英語 |
| Es-es | スペイン語 |
| Fr-fr | フランス語 |
| It-it | イタリア語 |
| Ja-jp | 日本語 |
| Ko-kr | 韓国語 |
| Pl-pl | ポーランド語 |
| Pt-br | ポルトガル語 - ブラジル |
| Ru-ru | ロシア語 |
| Tr-tr | トルコ語 |
| Zh-cn | 中国語 - 簡体字 |
| Zh-tw | 中国語 - 繁体字 |

## <a name="error-codes"></a>エラー コード

操作の結果に応じて、`%ERRORLEVEL%` 環境変数は、次のいずれかの値に設定されます。

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

操作ごとに、インストールの進行状況を示す複数のログ ファイルが `%TEMP%` ディレクトリに生成されます。 フォルダーを日付で並べ替え、`dd_bootstrapper`、`dd_client`、`dd_setup` で始まるファイルを探します (それぞれブートストラップ、インストーラー アプリ、セットアップ エンジンを表します)。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

- [Visual Studio のインストールに使用するコマンド ライン パラメーターの例](command-line-parameter-examples.md)
- [Visual Studio のオフライン インストールを作成する](create-an-offline-installation-of-visual-studio.md)
- [応答ファイルで Visual Studio インストールを自動化する](automated-installation-with-response-file.md)
- [Visual Studio のワークロードとコンポーネント ID](workload-and-component-ids.md)
