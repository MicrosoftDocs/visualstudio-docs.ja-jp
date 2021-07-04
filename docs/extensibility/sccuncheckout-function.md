---
description: この関数では、前のチェックアウト操作を元に戻します。これで、選択したファイルのコンテンツがチェックアウト前の状態に復元されます。
title: SccUncheckout 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3a382a112b5a11acc36c52735c949ebef71052ec
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904088"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 関数
この関数では、前のチェックアウト操作を元に戻します。これで、選択したファイルのコンテンツがチェックアウト前の状態に復元されます。 チェックアウト後にファイルに加えられた変更はすべて失われます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccUncheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] 提供するすべてのダイアログ ボックスの親としてソース管理プラグインで使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] `lpFileNames` 配列で指定されているファイルの数。

 lpFileNames

[入力] チェックアウトを元に戻すファイルの完全修飾ローカル パス名の配列。

 fOptions

[入力] コマンド フラグ (使用されません)。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|チェックアウトが正常に元に戻されました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理下にありません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 チェックアウトを元に戻すことができませんでした。|
|SCC_E_NOTCHECKEDOUT|ユーザーは、ファイルをチェックアウトしていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理から開かれていません。|
|SCC_I_OPERATIONCANCELED|操作は完了前にキャンセルされました。|

## <a name="remarks"></a>解説
 この操作の後、チェックアウトを元に戻す操作が実行されたファイルの `SCC_STATUS_CHECKEDOUT` と `SCC_STATUS_MODIFIED` フラグは両方ともクリアされます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
