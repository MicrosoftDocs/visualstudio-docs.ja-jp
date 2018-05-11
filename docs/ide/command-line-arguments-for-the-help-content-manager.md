---
title: ヘルプ コンテンツ マネージャーのコマンド ライン引数
ms.date: 11/01/2017
ms.prod: visual-studio-dev15
ms.technology: vs-help-viewer
ms.topic: reference
ms.assetid: 3aa9890a-1147-42ba-adea-17935d184038
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 82303d664245e9f04d13b6ee7ca39d09f43bc003
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
---
# <a name="command-line-arguments-for-the-help-content-manager"></a>ヘルプ コンテンツ マネージャーのコマンド ライン引数

ヘルプ コンテンツ マネージャー (*HlpCtntMgr.exe*) のコマンド ライン引数を使用して、ローカル ヘルプ コンテンツを配置および管理する方法を指定できます。 管理者のアクセス許可でこのコマンド ライン ツールのスクリプトを実行する必要があり、これらのスクリプトをサービスとして実行することはできません。 このツールを使用して、以下のタスクを実行できます。

-   ディスクまたはクラウドのローカル ヘルプ コンテンツを追加または更新します。

-   ローカル ヘルプ コンテンツを削除します。

-   ローカル ヘルプ コンテンツ ストアを移動します。

-   ローカル ヘルプ コンテンツを、サイレント モードで追加、更新、削除、または移動します。

構文:

```cmd
HlpCtntmgr.exe /operation Value /catalogname CatalogName /locale Locale /sourceuri InstallationPoint
```

例:

```cmd
hlpctntmgr.exe /operation install /catalogname VisualStudio15 /locale en-us /sourceuri d:\productDocumentation\HelpContentSetup.msha
```

## <a name="switches-and-arguments"></a>スイッチおよび引数

次の表に、ヘルプ コンテンツ マネージャーのコマンド ライン ツールで使用できるスイッチと引数の定義を示します。

|切り替え|必須?|引数|
|------------|---------------|---------------|
|/operation|[はい]|-   **Install** -- 指定されたインストール ソースからローカル コンテンツ ストアにブックを追加します。<br />     このスイッチには、/booklist 引数、/sourceURI 引数、または両方が必要です。 /sourceURI 引数を指定しない場合、Visual Studio の既定の URI がインストール ソースとして使用されます。 /booklist 引数を指定しない場合、/sourceUri のすべてのブックがインストールされます。<br />-   **Uninstall** -- 指定するブックをローカル コンテンツ ストアから削除します。<br />     このスイッチには、/booklist 引数または /sourceURI 引数が必要です。  /sourceURI 引数を指定すると、すべてのブックが削除され、/booklist 引数は無視されます。<br />-   **Move** -- 指定するパスにローカル ストアを移動します。 既定のローカル ストア パスは、*%ProgramData%* 下のディレクトリとして設定されます。<br />     このスイッチには、/locationPath 引数と /catalogName 引数が必要です。 有効でないパスを指定した場合、またはドライブにコンテンツを保持するのに十分な空き領域がない場合は、エラー メッセージがイベント ログに記録されます。<br />-   **Refresh** -- インストール後または最近の更新後に変更されたトピックを更新します。<br />     このスイッチには /sourceURI 引数が必要です。|
|/catalogName|[はい]|コンテンツ カタログの名前を指定します。|
|/locale|×|ヘルプ ビューアーの現在のインスタンスのコンテンツを表示および管理するために使用される製品ロケールを指定します。 たとえば、英語-米国の場合は `EN-US` を指定します。<br /><br /> ロケールを指定しない場合、オペレーティング システムのロケールが使用されます。 そのロケールを特定できない場合、`EN-US` が使用されます。<br /><br /> 有効でないロケールを指定した場合は、エラー メッセージがイベント ログに記録されます。|
|/e|×|現在のユーザーに管理者資格情報がある場合は、ヘルプ コンテンツ マネージャーを管理特権に昇格させます。|
|/sourceURI|×|コンテンツのインストール元の URL (サービス API)、またはコンテンツ インストール ファイル (*.msha*) へのパスを指定します。 URL は、Visual Studio 2010 スタイルのエンドポイントの製品グループ (最上位のノード)、または製品ブック (リーフ レベル ノード) を指すことができます。 URL の最後にスラッシュ (/) を含める必要はありません。 後続のスラッシュを含めた場合も適切に処理されます。<br /><br /> 見つからないファイルや有効でないファイル、アクセスできないファイルを指定した場合、またはインターネットへの接続が使用できないか、コンテンツの管理中に中断した場合は、エラー メッセージがイベント ログに記録されます。|
|/vendor|×|削除される製品コンテンツの販売元 (`Microsoft` など) を指定します。 このスイッチの既定の引数は Microsoft です。|
|/productName|×|削除されるブックの製品名を指定します。 製品名は、コンテンツに付属する *helpcontentsetup.msha* または *books.html* ファイルに示されています。 一度に 1 つの製品からのみブックを削除できます。 複数の製品からブックを削除するには、複数のインストールを実行する必要があります。|
|/booklist|×|管理するブックの名前をスペースで区切って指定します。 値は、インストール メディアに示されたブック名と一致する必要があります。<br /><br /> この引数を指定しない場合、/sourceURI で指定された製品の推奨されるブックがすべてインストールされます。<br /><br /> ブック名にスペースが 1 つ以上含まれている場合は、リストが適切に区切られるようにブック名を二重引用符 (") で囲みます。<br /><br /> 有効でないか到達可能でない /sourceURI を指定した場合は、エラー メッセージが記録されます。|
|/skuId|×|インストール ソースから製品の在庫管理単位 (SKU) を指定し、/SourceURI スイッチで識別されるブックにフィルターを適用します。|
|/membership|Ｘ|-   **Minimum** -- /skuId スイッチで指定する SKU に基づいて、最小限のヘルプ コンテンツ セットをインストールします。 SKU とコンテンツ セットの間のマッピングは、サービス API で公開されます。<br />-   **Recommended** -- /skuId 引数で指定する SKU の推奨ブック セットをインストールします。 インストール ソースは、サービス API または *.MSHA* です。<br />-   **Full** -- /skuId 引数で指定する SKU のすべてのブック セットをインストールします。 インストール ソースは、サービス API または *.MSHA* です。|
|/locationpath|×|ローカル ヘルプ コンテンツの既定のフォルダーを指定します。 このスイッチは、コンテンツをインストールまたは移動する場合にのみ使用する必要があります。 このスイッチを指定する場合は、/silent スイッチも指定する必要があります。|
|/silent|×|ユーザーに確認せずに、または状態通知領域のアイコンなどの UI を表示せずに、ヘルプ コンテンツをインストールまたは削除します。 *%Temp%* ディレクトリ内のファイルに出力が記録されます。 **重要:** コンテンツをサイレント モードでインストールするには、*.mshc* ファイルではなく、デジタル署名された *.cab* ファイルを使用する必要があります。|
|/launchingApp|×|ヘルプ ビューアーが親アプリケーションなしで起動されるときのアプリケーションおよびカタログ コンテキストを定義します。 このスイッチの引数は、*CompanyName*、*ProductName*、および *VersionNumber* です (例: `/launchingApp Microsoft,VisualStudio,15.0`)。<br /><br /> これは、/silent パラメーター付きでコンテンツをインストールするために必要です。|
|/wait *秒数*|×|インストール、アンインストール、および更新操作を一時停止します。 操作が既にカタログに対して進行中の場合、プロセスは特定の秒数が経過するまで続行を待機します。 無期限に待機するには 0 を使用します。|
|/?|×|ヘルプ コンテンツ マネージャーのコマンド ライン ツールのスイッチとその説明を一覧表示します。|

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

- [ヘルプ ビューアーの管理者ガイド](../ide/help-viewer-administrator-guide.md)
- [ヘルプ コンテンツ マネージャーのオーバーライド](../ide/help-content-manager-overrides.md)
- [Microsoft Help Viewer](../ide/microsoft-help-viewer.md)