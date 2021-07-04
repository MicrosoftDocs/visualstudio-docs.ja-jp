---
description: この関数では、確認するディレクトリの一覧が指定されたとき、どのディレクトリとファイル (オプション) がソース管理に格納されるかを特定します。
title: SccPopulateDirList 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccPopulateDirList
helpviewer_keywords:
- SccPopulateDirList function
ms.assetid: dfff634b-b155-498b-a356-6eb252ac4fad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bf2620ff42106be7c858c5104dbf9cb2521252ab
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902359"
---
# <a name="sccpopulatedirlist-function"></a>SccPopulateDirList 関数
この関数では、確認するディレクトリの一覧が指定されたとき、どのディレクトリとファイル (オプション) がソース管理に格納されるかを特定します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccPopulateDirList(
   LPVOID        pContext,
   LONG          nDirs,
   LPCSTR*       lpDirPaths,
   POPDIRLISTFUNCpfnPopulate,
   LPVOID        pvCallerData,
   LONG          fOptions
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース管理プラグインのコンテキスト ポインター。

 nDirs

[入力] `lpDirPaths` 配列内のディレクトリ パスの数。

 lpDirPaths

[入力] 確認するディレクトリ パスの配列。

 pfnPopulate

[入力] `lpDirPaths` 内のディレクトリ パスとファイル名 (オプション) ごとに呼び出すコールバック関数 (詳細については、「[POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)」を参照)。

 pvCallerData

[入力] 変更なしでコールバック関数に渡される値。

 fOptions

[入力] ディレクトリの処理方法を制御する値の組み合わせ (指定できる値については、「[特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)」の「PopulateDirList フラグ」セクションを参照)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|操作は正常に完了しました。|
|SCC_E_UNKNOWNERROR|エラーが発生しました。|

## <a name="remarks"></a>解説
 実際にソース管理リポジトリ内に存在するディレクトリとファイル名 (オプション) だけがコールバック関数に渡されます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)
- [エラー コード](../extensibility/error-codes.md)
