---
title: エラー コード | Microsoft Docs
description: この記事には、ソース管理プラグイン API 関数のエラー コード、値、および説明の一覧が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- error codes, source control plug-ins
- source control plug-ins, error codes
- errors [Visual Studio SDK]
ms.assetid: d9cbd1c4-719b-467a-8100-333c1e146d3b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eedc9311bcafdd4241e065b40079abed3977dcef
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898306"
---
# <a name="error-codes"></a>エラー コード
ソース管理プラグイン API 関数からエラーが返された場合、次のエラー コードのいずれかであることが予想されます。 すべてのエラーは負であり、警告または情報エラー コードは正であり、成功は 0 です。

|エラー コード|値|説明|
|----------------|-----------|-----------------|
|`SCC_I_SHARESUBPROJOK`|7|プラグインは、2 つの手順でソース管理からのファイルの追加をサポートしています。 詳細については、[SccSetOption](../extensibility/sccsetoption-function.md) に関するページを参照してください。|
|`SCC_I_FILEDIFFERS`|6|ローカル ファイルが、ソース管理データベース内のファイルと異なります (たとえば、[SccDiff](../extensibility/sccdiff-function.md) からこの値が返されることがあります)。|
|`SCC_I_RELOADFILE`|5|ソース管理操作中にローカル ファイルが変更されました。可能であれば、IDE によりファイルを再度読み込む必要があります。|
|`SCC_I_FILENOTAFFECTED`|4|ファイルは影響を受けません。|
|`SCC_I_PROJECTCREATED`|3|プロジェクトは、ソース管理操作中に作成されました (たとえば、`SCC_OP_CREATEIFNEW` フラグが指定されている場合の [SccOpenProject](../extensibility/sccopenproject-function.md) の呼び出し中)。|
|`SCC_I_OPERATIONCANCELED`|2|操作が取り消されました。|
|`SCC_I_ADV_SUPPORT`|1|プラグインは、指定されたコマンドの詳細オプションをサポートします。 詳細については、[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) に関するページを参照してください。|
|`SCC_OK`|0|正常終了しました。|
|`SCC_E_INITIALIZEFAILED`|-1|エラー: 初期化に失敗しました。|
|`SCC_E_UNKNOWNPROJECT`|-2|エラー: プロジェクトが不明です。|
|`SCC_E_COULDNOTCREATEPROJECT`|-3|エラー: プロジェクトを作成できませんでした。|
|`SCC_E_NOTCHECKEDOUT`|-4|エラー: ファイルはチェックアウトされていません。|
|`SCC_E_ALREADYCHECKEDOUT`|-5|エラー: ファイルは既にチェックアウトされています。|
|`SCC_E_FILEISLOCKED`|-6|エラー: ファイルはロックされています。|
|`SCC_E_FILEOUTEXCLUSIVE`|-7|エラー: ファイルは排他的にチェックアウトされています。|
|`SCC_E_ACCESSFAILURE`|-8|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|`SCC_E_CHECKINCONFLICT`|-9|エラー: チェックイン中に競合が発生しました。|
|`SCC_E_FILEALREADYEXISTS`|-10|エラー: ファイルは既に存在します。|
|`SCC_E_FILENOTCONTROLLED`|-11|エラー: ファイルはソース管理されていません。|
|`SCC_E_FILEISCHECKEDOUT`|-12|エラー: ファイルはチェックアウトされています。|
|`SCC_E_NOSPECIFIEDVERSION`|-13|エラー: 指定されたバージョンがありません。|
|`SCC_E_OPNOTSUPPORTED`|-14|エラー: 操作はサポートされていません。|
|`SCC_E_NONSPECIFICERROR`|-15|不特定のエラーです。|
|`SCC_E_OPNOTPERFORMED`|-16|エラー、操作が実行されませんでした。|
|`SCC_E_TYPENOTSUPPORTED`|-17|エラー: ファイルの種類 (バイナリなど) が、ソース コード管理システムでサポートされていません。|
|`SCC_E_VERIFYMERGE`|-18|ファイルは自動マージされましたが、ユーザーの検証が保留中であるため、チェックインされていません。|
|`SCC_E_FIXMERGE`|-19|ファイルは自動マージされましたが、手動で解決する必要があるマージの競合のためにチェックインされませんでした。|
|`SCC_E_SHELLFAILURE`|-20|シェルの失敗によるエラー。|
|`SCC_E_INVALIDUSER`|-21|エラー: ユーザーが無効です。|
|`SCC_E_PROJECTALREADYOPEN`|-22|エラー: プロジェクトは既に開かれています。|
|`SCC_E_PROJSYNTAXERR`|-23|プロジェクトの構文エラー。|
|`SCC_E_INVALIDFILEPATH`|-24|エラー: ファイル パスが無効です。|
|`SCC_E_PROJNOTOPEN`|-25|エラー: プロジェクトが開かれていません。|
|`SCC_E_NOTAUTHORIZED`|-26|エラー: ユーザーにはこの操作を実行する権限がありません。|
|`SCC_E_FILESYNTAXERR`|-27|ファイルの構文エラー。|
|`SCC_E_FILENOTEXIST`|-28|エラー、ローカル ファイルが存在しません。|
|`SCC_E_CONNECTIONFAILURE`|-29|エラー: 接続エラーが発生しました。|
|`SCC_E_UNKNOWNERROR`|-30|不明なエラー。|
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|バックグラウンドの取得操作が現在進行中です。|

## <a name="macros-provided-for-quick-checking"></a>クイック チェック用のマクロ

```cpp
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)
```

## <a name="remarks"></a>解説
 すべてのソース管理プラグイン API 関数 ([SccAdd](../extensibility/sccadd-function.md)、[SccCheckin](../extensibility/scccheckin-function.md)、および [SccDiff ](../extensibility/sccdiff-function.md)を除く) は、引数として渡されたローカル ファイルが作業フォルダーに存在しない場合、成功することが想定されています。 たとえば、作業フォルダーには存在せず、ソース管理システムには存在するファイルに対して、IDE から [SccCheckout](../extensibility/scccheckout-function.md) または [SccUncheckout](../extensibility/sccuncheckout-function.md) の呼び出しが発行される場合があります。 この呼び出しは成功します。 作業フォルダーまたはソース管理システムにファイルがない場合にのみ、関数が失敗することが想定されています。

 `SccAdd` や `SccCheckin` など一部の関数からは、作業フォルダー内のファイルが存在しない場合に、特に `SCC_E_FILENOTEXIST` が返されます。 他の関数は、関数がソース管理システムの有効なファイル名で動作する場合、作業ファイルが存在しないときに成功することが想定されています。

 ソース管理プラグイン側では、何らかの操作中にプラグインによってファイルが読み取り専用としてマークされた場合でも、作業フォルダー内のファイルに対する特権に関して想定を行うべきではありません。 作業フォルダー内のファイルは、プラグインの制御外で移動、削除、および変更できます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md)
