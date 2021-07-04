---
title: ソース管理プラグインの API 関数 | Microsoft Docs
description: ソース管理プラグイン API によって提供される関数について説明します。この関数は、ソース管理プラグインによって実装される必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f93ddff78aa151218d0b46d017e4631d9489e44
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899603"
---
# <a name="source-control-plug-in-api-functions"></a>ソース管理プラグインの API 関数
ソース管理プラグイン API には、次の関数が用意されています。これらの関数は、この API に従って、ソース管理プラグインによって実装される必要があります。 各関数のシグネチャ、およびビット フラグとその他のパラメーターに関連付けられているセマンティクスについては、このリファレンスで詳しく説明します。

## <a name="initialization-and-housekeeping-functions"></a>初期化関数とハウスキーピング関数

|機能|説明|
|--------------|-----------------|
|[SccCloseProject](../extensibility/scccloseproject-function.md)|プロジェクトを閉じます。|
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|特定のコマンドの詳細オプションを使用するよう、ユーザーに促します。|
|[SccGetVersion](../extensibility/sccgetversion-function.md)|ソース管理プラグインのバージョンを返します。|
|[SccInitialize](../extensibility/sccinitialize-function.md)|ソース管理プラグインを初期化します。 これは、プラグインのインスタンスごとに 1 回、呼び出されます。|
|[SccOpenProject](../extensibility/sccopenproject-function.md)|プロジェクトを開きます。|
|[SccSetOption](../extensibility/sccsetoption-function.md)|さまざまなオプションを設定するために使用されるジェネリック関数。 各オプションは `SCC_OPT_xxx` で始まり、定義された独自の一連の値を含みます。|
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|ソース管理プラグインを解除する必要があるときに 1 回、呼び出されます。|

## <a name="core-source-control-functions"></a>コア ソース管理関数

|機能|説明|
|--------------|-----------------|
|[SccAdd](../extensibility/sccadd-function.md)|完全修飾パス名によって指定されたファイルの配列をソース管理システムに追加します。|
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|ソース管理システムに既に存在するファイルをユーザーが参照し、そのファイルを現在のプロジェクトの一部として含めることができるようにします。|
|[SccCheckin](../extensibility/scccheckin-function.md)|ファイルの配列をチェックインします。|
|[SccCheckout](../extensibility/scccheckout-function.md)|ファイルの配列をチェックアウトします。|
|[SccDiff](../extensibility/sccdiff-function.md)|完全修飾パス名によって指定されたローカル ユーザーのファイルと、ソース管理下のバージョンとの違いを表示します。|
|[SccGet](../extensibility/sccget-function.md)|一連のファイルの読み取り専用コピーを取得します。|
|[SccGetEvents](../extensibility/sccgetevents-function.md)|呼び出し元が (`SccQueryInfo` を使用して) 問い合わせたファイルの状態を確認します。|
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|プラグインにとって意味のあるプロジェクト パスを指定することをソース管理プラグインがユーザーに促すようにします。|
|[SccHistory](../extensibility/scchistory-function.md)|完全修飾ローカル ファイル名の配列の履歴を表示します。|
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|ファイルの一覧で、ファイルの現在の状態を調べます。 さらに、ファイルが `nCommand` の条件に一致しない場合は、`pfnPopulate` 関数を使用して呼び出し元に通知します。|
|[SccProperties](../extensibility/sccproperties-function.md)|完全修飾ファイルのプロパティを表示します。|
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|完全修飾ファイルの一覧で、ファイルの現在の状態を調べます。|
|[SccRemove](../extensibility/sccremove-function.md)|完全修飾ファイルの配列をソース管理システムから削除します。|
|[SccRename](../extensibility/sccrename-function.md)|特定のファイルの名前を、ソース管理システムでの新しい名前に変更します。|
|[SccRunScc](../extensibility/sccrunscc-function.md)|ソース管理システムのすべての機能にアクセスします。|
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|ファイルの配列のチェックアウトを元に戻します。|

## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>追加機能をサポートする関数 (ソース管理プラグイン API のバージョン 1.2)
 この関数のグループは、ソース管理プラグイン API のバージョン 1.2 に含まれる追加機能を定義します。 これらの関数は、より高度なソース管理機能へのアクセスを提供します。

|機能|説明|
|--------------|-----------------|
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|バッチ操作を開始します。|
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|既存の親プロジェクトの下に、特定の名前のサブプロジェクトを作成します。|
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|完全修飾パス名によって指定されたローカル ユーザーのディレクトリと、ソース管理データベースの場所との違いを表示します。|
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|完全修飾ディレクトリの一覧で、ディレクトリの現在の状態を調べます。|
|[SccEndBatch](../extensibility/sccendbatch-function.md)|バッチ操作を終了します。|
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|特定のプロジェクト (プロジェクトが存在している必要があります) の親パスを返します。|
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|ファイルに対して複数のチェックアウトが許可されるかどうかを確認します。|
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|プラグインが MSSCCPRJ.SCC ファイルを作成するかどうかを確認します。|

## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>高度な機能をサポートする関数 (ソース管理プラグイン API のバージョン 1.3)
 この関数のグループは、ソース管理プラグイン API のバージョン 1.3 に含まれる追加機能を定義します。 これらの関数は、より高度なソース管理機能へのアクセスを提供します。

|機能|説明|
|--------------|-----------------|
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|ソース管理から現在のプロジェクトに、ファイルの一覧を追加します。|
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|ユーザー インターフェイスを使用せずにソース管理からファイルの一覧を取得します。|
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|ローカル ファイルとは異なる、ソース管理内のファイルの一覧を取得します。|
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|ソース管理プラグインでサポートされている拡張機能を指定するフラグを取得します。|
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|ユーザー固有のオプションを取得します。|
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|ソース管理下にある 1 つまたは複数のプロジェクト内のディレクトリとファイルの一覧を調べます。 見つかった各ディレクトリおよびファイル名は、コールバック関数に渡されます。|
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|ファイルの一覧に対して行われた名前の変更を調べます。 各ファイル名は、その変更の状態と共にコールバック関数に渡されます。|

## <a name="requirements"></a>必要条件
 ヘッダー: scc.h

 (環境 SDK の共通インクルード フォルダーで提供されます。これは既定では、 *[drive]* \Program Files\VSIP 8.0\EnvSDK\common\inc です。また、MSSCCI サンプルを含む VSIP フォルダー、 *[drive]* \Program Files\VSIP 8.0\MSSCCI でも提供されます)。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
- [ソース管理プラグインの作成](../extensibility/internals/creating-a-source-control-plug-in.md)
