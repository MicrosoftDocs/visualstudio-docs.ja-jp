---
description: この関数は、ソース管理から現在開いているプロジェクトにファイルの一覧を追加します。
title: SccAddFilesFromSCC 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fa08ec93383fa661d1e2dd055b3139b2ba90f34
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904865"
---
# <a name="sccaddfilesfromscc-function"></a>SccAddFilesFromSCC 関数
この関数は、ソース管理から現在開いているプロジェクトにファイルの一覧を追加します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAddFilesFromSCC(
   LPVOID  pContext,
   HWND    hWnd,
   LPSTR   lpUser,
   LPSTR   lpAuxProjPath,
   LONG    cFiles,
   LPCSTR* lpFilePaths,
   LPCSTR  lpDestination,
   LPCSTR  lpComment,
   LPBOOL  pbResults
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in] ソース管理プラグインのコンテキスト ポインター。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpUser

[入力、出力] ユーザー名 (null 終端文字を含め、最大 SCC_USER_SIZE 文字)。

 lpAuxProjPath

[入力、出力] プロジェクトを識別する補助文字列 (null 終端文字を含め、最大 `SCC_PRJPATH_`SIZE 文字)。

 cFiles

[入力] `lpFilePaths` によって指定されたファイルの数。

 lpFilePaths

[入力、出力] 現在のプロジェクトに追加するファイル名の配列。

 lpDestination

[入力] ファイルの書き込み先のパス。

 lpComment

[入力] 追加する各ファイルに適用されるコメント。

 pbResults

[入力、出力] 各ファイルに対して成功 (0 以外または TRUE) または失敗 (0 または FALSE) を示すフラグの配列 (配列のサイズは、少なくとも `cFiles` 以上の長さである必要があります)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_E_PROJNOTOPEN|プロジェクトが開いていません。|
|SCC_E_OPNOTPERFORMED|接続は、`lpAuxProjPath.` によって指定されたプロジェクトと同じではありません|
|SCC_E_NOTAUTHORIZED|ユーザーには、データベースを更新する権限がありません。|
|SCC_E_NONSPECIFICERROR|不明なエラー。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
