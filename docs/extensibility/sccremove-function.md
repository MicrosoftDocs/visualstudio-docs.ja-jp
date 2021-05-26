---
description: この関数は、ソース管理システムからファイルを削除します。
title: SccRemove 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d80daf83458c9e05ef0a081348080579e7fafef4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073873"
---
# <a name="sccremove-function"></a>SccRemove 関数
この関数は、ソース管理システムからファイルを削除します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccRemove(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] `lpFileNames` 配列で指定されているファイルの数。

 lpFileNames

[入力] 削除するファイルの完全修飾ローカル パス名の配列。

 lpComment

[入力] 削除する各ファイルに適用されるコメント。

 fOptions

[入力] コマンド フラグ (未使用)。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|削除に成功しました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理されていません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作はサポートされていません。|
|SCC_E_ISCHECKEDOUT|現在ユーザーがチェックアウトしているため、ファイルを削除できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。ファイルは削除されませんでした。|
|SCC_I_OPERATIONCANCELED|操作は完了前にキャンセルされました。|

## <a name="remarks"></a>解説
 この関数は、ソース管理システムからファイルを削除しますが、ユーザーのローカル ハード ドライブからは削除しません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
