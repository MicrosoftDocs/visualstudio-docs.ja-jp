---
description: 完全修飾ファイル名のリストを前提に、この関数はローカル ドライブにチェックアウトします。
title: SccCheckout 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f93052ebe255cddb4703a8246b7e89c744548a7f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060381"
---
# <a name="scccheckout-function"></a>SccCheckout 関数
完全修飾ファイル名のリストを前提に、この関数はローカル ドライブにチェックアウトします。 コメントは、チェックアウトされているすべてのファイルに適用されます。コメント引数には `null` 文字列を指定できます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] チェックアウト対象として選択されたファイルの数。

 lpFileNames

[入力] チェックアウトするファイルの完全修飾ローカル パス名の配列。

 lpComment

[入力] チェックアウトされる選択された各ファイルに適用されるコメント。

 fOptions

[入力] コマンド フラグ (「[特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)」を参照)。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|チェックアウトに成功しました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソースコード管理されていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作の実行が許可されていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 ファイルはチェックアウトされませんでした。|
|SCC_E_ALREADYCHECKEDOUT|ユーザーは既にファイルをチェックアウトしています。|
|SCC_E_FILEISLOCKED|ファイルがロックされているため、新しいバージョンの作成が禁止されています。|
|SCC_E_FILEOUTEXCLUSIVE|別のユーザーがこのファイルに対して排他的チェックアウトを実行しました。|
|SCC_I_OPERATIONCANCELED|操作は完了前にキャンセルされました。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
