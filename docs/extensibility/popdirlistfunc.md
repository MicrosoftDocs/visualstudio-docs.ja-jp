---
title: POPDIRLISTFUNC | Microsoft Docs
description: ディレクトリを更新してどれがソース管理下にあるかを確認するために渡される、POPDIRLISTFUNC コールバック関数について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- POPLISTFUNC
helpviewer_keywords:
- POPDIRLISTFUNC callback function
ms.assetid: 0ee90fd2-5467-4154-ab4c-7eb02ac3a14c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c98b35d9f915e16072333c72df2e1e045850f5d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900396"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
これは、ディレクトリのコレクションと (必要に応じて) ファイル名を更新して、どれがソース管理下にあるかを確認するために、[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 関数に渡されるコールバック関数です。

 `POPDIRLISTFUNC` コールバックは、実際にソース管理下にある (`SccPopulateDirList` 関数に指定されたリスト内の) ディレクトリとファイル名に対してのみ呼び出す必要があります。

## <a name="signature"></a>署名

```cpp
typedef BOOL (*POPDIRLISTFUNC)(
   LPVOID pvCallerData,
   BOOL bFolder,
   LPCSTR lpDirectoryOrFileName
);
```

## <a name="parameters"></a>パラメーター
 pvCallerData

[入力] [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) に指定されたユーザー値。

 bFolder

[入力] `lpDirectoryOrFileName` 内の名前がディレクトリである場合は `TRUE`。それ以外の場合、名前はファイル名です。

 lpDirectoryOrFileName

[入力] ソース コード管理下にあるディレクトリまたはファイル名への完全なローカル パス。

## <a name="return-value"></a>戻り値
 IDE によって適切なエラー コードが返されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|処理し続けます。|
|SCC_I_OPERATIONCANCELED|処理を停止します。|
|SCC_E_xxx|該当するソース管理エラーが発生すると、処理が停止します。|

## <a name="remarks"></a>解説
 `SccPopulateDirList` 関数の `fOptions` パラメーターに `SCC_PDL_INCLUDEFILES` フラグが含まれている場合、リストにはファイル名とディレクトリ名が含められる可能性があります。

## <a name="see-also"></a>関連項目
- [IDE で実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [エラー コード](../extensibility/error-codes.md)
