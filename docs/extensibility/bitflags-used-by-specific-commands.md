---
title: 特定のコマンドで使用されるビットフラグ | Microsoft Docs
description: ソース管理プラグイン API で使用されるビットフラグについて説明します。それらを使用する関数別に整理してあります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, bitflags used by specific commands
ms.assetid: 37969977-6f7d-45c9-ba03-1306ae71f5d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 41f070d61e547724b3067a9f4a1980d658fc30be
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097293"
---
# <a name="bitflags-used-by-specific-commands"></a>特定のコマンドで使用されるビットフラグ
ソース管理プラグイン API の多くの関数の動作は、単一の値に 1 つ以上のビットを設定することによって変更できます。 これらの値はビットフラグと呼ばれます。 ソース管理プラグイン API で使用されるさまざまなビットフラグについては、それらを使用する関数別にグループ化して、ここで詳しく説明しています。

## <a name="checked-out-flag"></a>Checked out フラグ
 このフラグは、[SccAdd](../extensibility/sccadd-function.md) または [SccCheckin](../extensibility/scccheckin-function.md) のいずれかに対して設定できます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_KEEP_CHECKEDOUT`|0x1000|ファイルをチェックアウトしたままにします。|

## <a name="add-flags"></a>Add フラグ
 これらのフラグは [SccAdd](../extensibility/sccadd-function.md) によって使用されます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_FILETYPE_AUTO`|0x00|ソース管理プラグインは、ファイルがテキストであるかバイナリであるかを自動的に検出するよう要求されます。|
|`SCC_FILETYPE_TEXT`|0x01|ファイルの種類はテキストです。|
|`SCC_FILETYPE_BINARY`|0x04|ファイルの種類はバイナリです。 **注:**  `SCC_FILETYPE_TEXT` フラグと `SCC_FILETYPE_BINARY` フラグは同時に使用できません。 1 つだけ設定するか、どちらも設定しません。|
|`SCC_ADD_STORELATEST`|0x02|最新のバージョンのみを格納します (デルタなし)。|

## <a name="diff-flags"></a>Diff フラグ
 [SccDiff](../extensibility/sccdiff-function.md) では、これらのフラグを使用して、diff 操作のスコープを定義します。 `SCC_DIFF_QD_xxx` フラグは同時に使用できません。 これらのいずれか 1 つが指定されている場合、視覚的フィードバックは提供されません。 "クイック diff" (QD) では、プラグインによって、ファイルがどのように異なるかは特定されず、ファイルが異なるかどうかだけが確認されます。 これらのフラグのどれも指定されていない場合は、"視覚的 diff" が実行されて、ファイルの詳細な相違点が計算され、表示されます。 要求された QD がサポートされていない場合、プラグインは次に最適なものに移動します。 たとえば、IDE からチェックサムが要求され、プラグインでそれをサポートしていない場合、プラグインでは内容の完全なチェックが行われます (それでも視覚的な表示よりもずっと高速です)。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_DIFF_IGNORECASE`|0x0002|大文字と小文字の区別を無視します。|
|`SCC_DIFF_IGNORESPACE`|0x0004|空白の違いを無視します。 **注:** `SCC_DIFF_IGNORECASE` フラグと `SCC_DIFF_IGNORESPACE` フラグは省略可能なビットフラグです。|
|`SCC_DIFF_QD_CONTENTS`|0x0010|ファイルの内容全体の比較による QD。|
|`SCC_DIFF_QD_CHECKSUM`|0x0020|チェックサムによる QD。|
|`SCC_DIFF_QD_TIME`|0x0040|ファイルの日付/時刻スタンプによる QD。|
|`SCC_DIFF_QUICK_DIFF`|0x0070|これは、すべての QD ビットフラグを確認するために使用されるマスクです。 これを関数に渡してはいけません。3 つの QD ビットフラグは同時に使用できません。 QD は常に、UI の表示はないことを意味します。|

## <a name="populatelist-flag"></a>PopulateList フラグ
 このフラグは、`fOptions` パラメーターの [SccPopulateList](../extensibility/sccpopulatelist-function.md) によって使用されます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_PL_DIR`|0x00000001L|IDE からは、ファイルではなくディレクトリが渡されようとしています。|

## <a name="populatedirlist-flags"></a>PopulateDirList フラグ
 これらのフラグは、`fOptions` パラメーターの [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) によって使用されます。

|オプション値|値|説明|
|------------------|-----------|-----------------|
|SCC_PDL_ONELEVEL|0x0000|ディレクトリについて、ディレクトリの 1 レベルだけを調べます (これは既定値です)。|
|SCC_PDL_RECURSIVE|0x0001|指定された各ディレクトリの下にあるすべてのディレクトリを再帰的に調べます。|
|SCC_PDL_INCLUDEFILES|0x0002|調査プロセスにファイル名を含めます。|

## <a name="openproject-flags"></a>OpenProject フラグ
 これらのフラグは、`dwFlags` パラメーターの [SccOpenProject](../extensibility/sccopenproject-function.md) によって使用されます。

|オプション値|値|説明|
|------------------|-----------|-----------------|
|SCC_OP_CREATEIFNEW|0x00000001L|ソース管理内にプロジェクトが存在しない場合は、プロジェクトを作成します。 このフラグが設定されていない場合、ユーザーにプロジェクトの作成を求めるプロンプトを表示します (`SCC_OP_SILENTOPEN` フラグが指定されていない場合)。|
|SCC_OP_SILENTOPEN|0x00000002L|ユーザーにプロジェクトの作成を求めるプロンプトを表示しません。ただ `SCC_E_UNKNOWNPROJECT` を返します。|

## <a name="get-flags"></a>Get フラグ
 これらのフラグは、[SccGet](../extensibility/sccget-function.md) と [SccCheckout](../extensibility/scccheckout-function.md) によって使用されます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_GET_ALL`|0x00000001L|IDE から、ファイルではなくディレクトリが渡されようとしています。これらのディレクトリ内のすべてのファイルを取得します。|
|`SCC_GET_RECURSIVE`|0x00000002L|IDE からディレクトリが渡されようとしています。これらのディレクトリと、そのすべてのサブディレクトリを取得します。|

## <a name="noption-values"></a>nOption 値
 これらのフラグは、`nOption` パラメーターの [SccSetOption](../extensibility/sccsetoption-function.md) によって使用されます。

|フラグ|値|説明|
|----------|-----------|-----------------|
|`SCC_OPT_EVENTQUEUE`|0x00000001L|イベント キューの状態を設定します。|
|`SCC_OPT_USERDATA`|0x00000002L|`SCC_OPT_NAMECHANGEPFN` のユーザー データを指定します。|
|`SCC_OPT_HASCANCELMODE`|0x00000003L|IDE でキャンセルを処理できます。|
|`SCC_OPT_NAMECHANGEPFN`|0x00000004L|名前の変更のためのコールバックを設定します。|
|`SCC_OPT_SCCCHECKOUTONLY`|0x00000005L|ソース管理プラグイン UI のチェックアウトを無効にして、作業ディレクトリを設定しません。|
|`SCC_OPT_SHARESUBPROJ`|0x00000006L|ソース管理システムから追加して作業ディレクトリを指定します。 直接の子孫である場合は、関連付けられているプロジェクトに対する共有を試みます。|

## <a name="dwval-bitflags"></a>dwVal ビットフラグ
 これらのフラグは、`dwVal` パラメーターの [SccSetOption](../extensibility/sccsetoption-function.md) によって使用されます。

|フラグ|値|説明|`nOption` 値で使用|
|----------|-----------|-----------------|-----------------------------|
|`SCC_OPT_EQ_DISABLE`|0x00L|イベント キューのアクティビティを中断します。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_EQ_ENABLE`|0x01L|イベント キューのログ記録を有効にします。|`SCC_OPT_EVENTQUEUE`|
|`SCC_OPT_HCM_NO`|0L|(既定値) キャンセル モードはありません。必要な場合はプラグインで提供する必要があります。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_HCM_YES`|1L|IDE でキャンセルを処理します。|`SCC_OPT_HASCANCELMODE`|
|`SCC_OPT_SCO_NO`|0L|(既定値) プラグイン UI からチェックアウトできます。作業ディレクトリが設定されます。|`SCC_OPT_SCCCHECKOUTONLY`|
|`SCC_OPT_SCO_YES`|1L|プラグイン UI のチェックアウトはありません。作業ディレクトリはありません。|`SCC_OPT_SCCCHECKOUTONLY`|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
