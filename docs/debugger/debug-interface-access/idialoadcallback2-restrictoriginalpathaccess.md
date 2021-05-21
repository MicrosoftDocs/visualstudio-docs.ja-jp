---
description: 元のデバッグ ディレクトリで .pdb ファイルを検索しても良いかどうかを判断します。
title: IDiaLoadCallback2::RestrictOriginalPathAccess | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback2::RestrictOriginalPathAccess method
ms.assetid: 31fde3af-2824-4b0f-8d0d-cee6046596f6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7af6794b57dfe5efe8d2e85f8e74febcede5ef23
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634864"
---
# <a name="idialoadcallback2restrictoriginalpathaccess"></a>IDiaLoadCallback2::RestrictOriginalPathAccess
元のデバッグ ディレクトリで .pdb ファイルを検索しても良いかどうかを判断します。

## <a name="syntax"></a>構文

```C++
HRESULT RestrictOriginalPathAccess ();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 `S_OK` 以外のリターン コードの場合、元のデバッグ ディレクトリで .pdb ファイルを検索できません。 元のデバッグ ディレクトリは、デバッグをオンにしたときに実行可能ファイルにコンパイルされるシンボル ファイルのパスです。 このパスは、実行可能ファイルが存在するパスと必ずしも同じではありません。

## <a name="see-also"></a>関連項目
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
