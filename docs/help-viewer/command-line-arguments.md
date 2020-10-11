---
title: ヘルプ コンテンツ マネージャーのコマンド ライン引数
description: ヘルプコンテンツマネージャー (HlpCtntMgr.exe) のコマンドライン引数を使用して、ローカルヘルプコンテンツを配置および管理する方法を指定します。
ms.date: 11/01/2017
ms.topic: reference
ms.assetid: 3aa9890a-1147-42ba-adea-17935d184038
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 24011c50cf6f8d2204abdaa8b6119f7873470bcf
ms.sourcegitcommit: dfbbf041e68ec3a4cd97196b19c9226a4793e702
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91879048"
---
# <a name="command-line-arguments-for-the-help-content-manager"></a>ヘルプ コンテンツ マネージャーのコマンド ライン引数

ヘルプコンテンツマネージャー (*HlpCtntMgr.exe*) のコマンドライン引数を使用して、ローカルヘルプコンテンツを配置および管理する方法を指定できます。 管理者のアクセス許可でこのコマンド ライン ツールのスクリプトを実行する必要があり、これらのスクリプトをサービスとして実行することはできません。 このツールを使用して、以下のタスクを実行できます。

- ディスクまたはクラウドのローカル ヘルプ コンテンツを追加または更新します。

- ローカル ヘルプ コンテンツを削除します。

- ローカル ヘルプ コンテンツ ストアを移動します。

- ローカル ヘルプ コンテンツを、サイレント モードで追加、更新、削除、または移動します。

構文:

```cmd
HlpCtntmgr.exe /operation Value /catalogname CatalogName /locale Locale /sourceuri InstallationPoint
```

次に例を示します。

```cmd
hlpctntmgr.exe /operation install /catalogname VisualStudio15 /locale en-us /sourceuri d:\productDocumentation\HelpContentSetup.msha
```

>[!NOTE]
> カタログ名は、Visual Studio 2017 と Visual Studio 2019 の両方に対して VisualStudio15 です。 これは予期しない問題である可能性がありますが、これは、Visual Studio の両方のバージョンで同じヘルプビューアーが使用されているためです。

## <a name="switches-and-arguments"></a>スイッチおよび引数

次の表に、ヘルプ コンテンツ マネージャーのコマンド ライン ツールで使用できるスイッチと引数の定義を示します。

|スイッチ|必須|引数|
|------------|---------------|---------------|
|/operation|はい|-   **Install** -- 指定されたインストール ソースからローカル コンテンツ ストアにブックを追加します。<br />     このスイッチには、/booklist 引数、/sourceURI 引数、または両方が必要です。 /sourceURI 引数を指定しない場合、Visual Studio の既定の URI がインストール ソースとして使用されます。 /booklist 引数を指定しない場合、/sourceUri のすべてのブックがインストールされます。<br />-   **Uninstall** -- 指定するブックをローカル コンテンツ ストアから削除します。<br />     このスイッチには、/booklist 引数または /sourceURI 引数が必要です。  /sourceURI 引数を指定すると、すべてのブックが削除され、/booklist 引数は無視されます。<br />-   **Move** -- 指定するパスにローカル ストアを移動します。 既定のローカルストアパスは、 *% Programdata%* の下のディレクトリとして設定されています<br />     このスイッチには、/locationPath 引数と /catalogName 引数が必要です。 有効でないパスを指定した場合、またはドライブにコンテンツを保持するのに十分な空き領域がない場合は、エラー メッセージがイベント ログに記録されます。<br />-   **Refresh** -- インストール後または最近の更新後に変更されたトピックを更新します。<br />     このスイッチには /sourceURI 引数が必要です。|
|/catalogName|はい|コンテンツ カタログの名前を指定します。 Visual Studio 2017 および Visual Studio 2019 の場合、これは VisualStudio15 です。|
|/locale|いいえ|ヘルプ ビューアーの現在のインスタンスのコンテンツを表示および管理するために使用される製品ロケールを指定します。 たとえば、英語-米国の場合は `EN-US` を指定します。<br /><br /> ロケールを指定しない場合、オペレーティング システムのロケールが使用されます。 そのロケールを特定できない場合、`EN-US` が使用されます。<br /><br /> 有効でないロケールを指定した場合は、エラー メッセージがイベント ログに記録されます。|
|/e|いいえ|現在のユーザーに管理者資格情報がある場合は、ヘルプ コンテンツ マネージャーを管理特権に昇格させます。|
|/sourceURI|いいえ|コンテンツのインストール元の URL (サービス API)、またはコンテンツインストールファイル (*msha*) へのパスを指定します。 URL は、Visual Studio 2010 スタイルのエンドポイントの製品グループ (最上位のノード)、または製品ブック (リーフ レベル ノード) を指すことができます。 URL の最後にスラッシュ (/) を含める必要はありません。 後続のスラッシュを含めた場合も適切に処理されます。<br /><br /> 見つからないファイルや有効でないファイル、アクセスできないファイルを指定した場合、またはインターネットへの接続が使用できないか、コンテンツの管理中に中断した場合は、エラー メッセージがイベント ログに記録されます。|
|/vendor|いいえ|削除される製品コンテンツの販売元 (`Microsoft` など) を指定します。 このスイッチの既定の引数は Microsoft です。|
|/productName|いいえ|削除されるブックの製品名を指定します。 製品名は、コンテンツに付属している *helpcontentsetup. msha* ファイルまたは *books.html* ファイルで識別されます。 一度に 1 つの製品からのみブックを削除できます。 複数の製品からブックを削除するには、複数のインストールを実行する必要があります。|
|/booklist|いいえ|管理するブックの名前をスペースで区切って指定します。 値は、インストール メディアに示されたブック名と一致する必要があります。<br /><br /> この引数を指定しない場合、/sourceURI で指定された製品の推奨されるブックがすべてインストールされます。<br /><br /> ブック名にスペースが 1 つ以上含まれている場合は、リストが適切に区切られるようにブック名を二重引用符 (") で囲みます。<br /><br /> 有効でないか到達可能でない /sourceURI を指定した場合は、エラー メッセージが記録されます。|
|/skuId|いいえ|インストール ソースから製品の在庫管理単位 (SKU) を指定し、/SourceURI スイッチで識別されるブックにフィルターを適用します。|
|/membership|いいえ|-   **Minimum** -- /skuId スイッチで指定する SKU に基づいて、最小限のヘルプ コンテンツ セットをインストールします。 SKU とコンテンツ セットの間のマッピングは、サービス API で公開されます。<br />-   **Recommended** -- /skuId 引数で指定する SKU の推奨ブック セットをインストールします。 インストールソースは、サービス API または *です。MSHA*。<br />-   **Full** -- /skuId 引数で指定する SKU のすべてのブック セットをインストールします。 インストールソースは、サービス API または *です。MSHA*。|
|/locationpath|いいえ|ローカル ヘルプ コンテンツの既定のフォルダーを指定します。 このスイッチは、コンテンツをインストールまたは移動する場合にのみ使用する必要があります。 このスイッチを指定する場合は、/silent スイッチも指定する必要があります。|
|/silent|いいえ|ユーザーに確認せずに、または状態通知領域のアイコンなどの UI を表示せずに、ヘルプ コンテンツをインストールまたは削除します。 出力は *% Temp%* ディレクトリ内のファイルに記録されます。 **重要:** コンテンツをサイレントインストールするには、 *.mshc*ファイルではなく、デジタル署名された *.cab*ファイルを使用する必要があります。|
|/launchingApp|いいえ|ヘルプ ビューアーが親アプリケーションなしで起動されるときのアプリケーションおよびカタログ コンテキストを定義します。 このスイッチの引数は、*CompanyName*、*ProductName*、および *VersionNumber* です (例: `/launchingApp Microsoft,VisualStudio,16.0`)。<br /><br /> これは、/silent パラメーター付きでコンテンツをインストールするために必要です。|
|/wait *秒数*|いいえ|インストール、アンインストール、および更新操作を一時停止します。 操作が既にカタログに対して進行中の場合、プロセスは特定の秒数が経過するまで続行を待機します。 無期限に待機するには、0 を使用します。|
|/?|いいえ|ヘルプ コンテンツ マネージャーのコマンド ライン ツールのスイッチとその説明を一覧表示します。|

### <a name="exit-codes"></a>終了コード

ヘルプ コンテンツ マネージャーのコマンド ライン ツールをサイレント モードで実行すると、次の終了コードが返されます。

```
Success = 0,

FailureToElevate = 100
InvalidCmdArgs = 101,
FailOnFetchingOnlineContent = 110,
FailOnFetchingContentFromDisk = 120,
FailOnFetchingInstalledBooks = 130,
NoBooksToUninstall = 200,
NoBooksToInstall = 300,
FailOnUninstall = 400,
FailOnInstall = 500,
FailOnMove = 600,
FailOnUpdate = 700,
FailOnRefresh = 800,
Cancelled = 900,
Others = 999,
ContentManagementDisabled = 1200,
OnlineHelpPreferenceDisabled = 1201
UpdateAlreadyRunning = 1300 - (Signals that the update didn't run because another was in progress.)
```

## <a name="see-also"></a>関連項目

- [ヘルプビューアーの管理者ガイド](../help-viewer/administrator-guide.md)
- [ヘルプコンテンツマネージャーのオーバーライド](../help-viewer/behavior-overrides.md)
- [Microsoft ヘルプ ビューアー](../help-viewer/overview.md)