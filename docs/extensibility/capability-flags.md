---
title: 機能フラグ | Microsoft Docs
description: ソース管理プラグインの機能を示す SCC_CAP_xxx フラグと、拡張機能を示す SCC_EXCAP_xxx フラグについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, capability flags
ms.assetid: a3f6071c-eac8-4bcd-8ffd-8d0a2d24a252
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3fdb660fd4e7c595f522686280f8bec6c0acae81
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905099"
---
# <a name="capability-flags"></a>機能フラグ
SCC_CAP_ *xxx* フラグは、ソース管理プラグインの機能を示すために使用されるビット フラグです。 SCC_EXCAP_ *xxx* フラグは、拡張機能を示し、整数値に解決される増分フラグです。

|機能コード|値|説明|
|---------------------|-----------|-----------------|
|`SCC_CAP_REMOVE`|0x00000001L|[SccRemove](../extensibility/sccremove-function.md) およびコマンドをサポートします。|
|`SCC_CAP_RENAME`|0x00000002L|[SccRename](../extensibility/sccrename-function.md) およびコマンドをサポートします。|
|`SCC_CAP_DIFF`|0x00000004L|[SccDiff](../extensibility/sccdiff-function.md) およびコマンドをサポートします。|
|`SCC_CAP_HISTORY`|0x00000008L|[SccHistory](../extensibility/scchistory-function.md) およびコマンドをサポートします。|
|`SCC_CAP_PROPERTIES`|0x00000010L|[SccProperties](../extensibility/sccproperties-function.md) およびコマンドをサポートします。|
|`SCC_CAP_RUNSCC`|0x00000020L|[SccRunScc](../extensibility/sccrunscc-function.md) およびコマンドをサポートします。|
|`SCC_CAP_GETCOMMANDOPTIONS`|0x00000040L|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) およびコマンドをサポートします。|
|`SCC_CAP_QUERYINFO`|0x00000080L|[SccQueryInfo](../extensibility/sccqueryinfo-function.md) およびコマンドをサポートします。|
|`SCC_CAP_GETEVENTS`|0x00000100L|[SccGetEvents](../extensibility/sccgetevents-function.md) およびコマンドをサポートします。|
|`SCC_CAP_GETPROJPATH`|0x00000200L|[SccGetProjPath](../extensibility/sccgetprojpath-function.md) およびコマンドをサポートします。|
|`SCC_CAP_ADDFROMSCC`|0x00000400L|[SccAddFromScc](../extensibility/sccaddfromscc-function.md) およびコマンドをサポートします。|
|`SCC_CAP_COMMENTCHECKOUT`|0x00000800L|チェックアウト時のコメントをサポートします。|
|`SCC_CAP_COMMENTCHECKIN`|0x00001000L|チェックイン時のコメントをサポートします。|
|`SCC_CAP_COMMENTADD`|0x00002000L|[追加] でのコメントをサポートします。|
|`SCC_CAP_COMMENTREMOVE`|0x00004000L|[削除] でのコメントをサポートします。|
|`SCC_CAP_TEXTOUT`|0x00008000L|IDE 提供の出力機能にテキストを書き込みます。|
|`SCC_CAP_ADD_STORELATEST`|0x00200000L|詳細なしにファイルの格納をサポートします。|
|`SCC_CAP_HISTORY_MULTFILE`|0x00400000L|複数のファイル履歴をサポートします。|
|`SCC_CAP_IGNORECASE`|0x00800000L|大文字と小文字を区別しないファイル比較をサポートします。|
|`SCC_CAP_IGNORESPACE`|0x01000000L|空白文字を無視するファイル比較をサポートします。|
|`SCC_CAP_POPULATELIST`|0x02000000L|余分なファイルの検索をサポートします。|
|`SCC_CAP_COMMENTPROJECT`|0x04000000L|プロジェクトの作成に関するコメントをサポートします。|
|`SCC_CAP_DIFFALWAYS`|0x10000000L|制御下にある場合は、すべての状態での差分をサポートします。|
|`SCC_CAP_GET_NOUI`|0x20000000L|プラグインでは Get 用の UI をサポートしませんが、IDE が引き続き [SccGet](../extensibility/sccget-function.md) を呼び出すことができます。|
|`SCC_CAP_REENTRANT`|0x40000000L|プラグインは再入可能で、スレッドセーフです。 バージョン 1.0 では、再入可能でスレッドセーフであると想定されたプラグインはありませんでした。 1\.1 プラグインでこのビットを設定した場合、複数のプロジェクトを並列して開くことがホストに許可されています。|

## <a name="capability-bits-added-in-version-12"></a>バージョン 1.2 で追加された機能ビット

|機能コード|値|説明|
|---------------------|-----------|-----------------|
|`SCC_CAP_CREATESUBPROJECT`|0x00010000L|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md) をサポートします。|
|`SCC_CAP_GETPARENTPROJECT`|0x00020000L|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md) をサポートします。|
|`SCC_CAP_BATCH`|0x00040000L|[SccBeginBatch](../extensibility/sccbeginbatch-function.md) と [SccEndBatch](../extensibility/sccendbatch-function.md) をサポートします。|
|`SCC_CAP_DIRECTORYSTATUS`|0x00080000L|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md) をサポートします。|
|`SCC_CAP_DIRECTORYDIFF`|0x00100000L|[SccDirDiff](../extensibility/sccdirdiff-function.md) をサポートします。|
|`SCC_CAP_MULTICHECKOUT`|0x08000000L|ファイルでの複数のチェックアウトと [SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md) をサポートします。|
|`SCC_CAP_SCCFILE`|0x80000000L|*MSSCCPRJ.SCC* ファイル (ユーザー/管理者のオーバーライドの対象) と [SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md) をサポートします。|

## <a name="capability-bits-added-in-version-13"></a>バージョン 1.3 で追加された機能ビット
 これらのフラグは、機能がサポートされているかどうかを判断するために、[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md) 関数に一度に 1 つずつ渡されます。

|拡張機能コード|値|説明|
|------------------------------|-----------|-----------------|
|`SCC_EXCAP_CHECKOUT_LOCALVER`|1|チェックアウト用の `SCC_CHECKOUT_LOCALVER` オプションをサポートします。|
|`SCC_EXCAP_BACKGROUND_GET`|2|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md) をサポートします。|
|`SCC_EXCAP_ENUM_CHANGED_FILES`|3|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md) をサポートします。|
|`SCC_EXCAP_POPULATELIST_DIR`|4|余分なディレクトリの検索をサポートします。|
|`SCC_EXCAP_QUERYCHANGES`|5|ファイルの変更の列挙をサポートします。|
|`SCC_EXCAP_ADD_FILES_FROM_SCC`|6|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md) をサポートします。|
|`SCC_EXCAP_GET_USER_OPTIONS`|7|[SccGetUserOption](../extensibility/sccgetuseroption-function.md) をサポートします。|
|`SCC_EXCAP_THREADSAFE_QUERY_INFO`|8|複数のスレッドでの SccQueryInfo の呼び出しをサポートします。|
|`SCC_EXCAP_REMOVE_DIR`|9|SccRemoveDir 関数をサポートします。|
|`SCC_EXCAP_DELETE_CHECKEDOUT`|10|チェックアウトされたファイルを削除できます。|
|`SCC_EXCAP_RENAME_CHECKEDOUT`|11|チェックアウトされたファイルの名前を変更できます。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
