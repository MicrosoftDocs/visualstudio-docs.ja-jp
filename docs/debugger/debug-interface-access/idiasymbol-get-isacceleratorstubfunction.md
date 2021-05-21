---
description: シンボルが、parallel_for_each 呼び出しに対応するアクセラレータ用にコンパイルされたシェーダーの最上位関数シンボルに対応しているかどうかを示します。
title: IDiaSymbol::get_isAcceleratorStubFunction | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: cc4ea375-76f6-4ba8-baed-c5fa82108137
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 710622fdb8fb10d0357c060097f13bab3be7d05f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634686"
---
# <a name="idiasymbolget_isacceleratorstubfunction"></a>IDiaSymbol::get_isAcceleratorStubFunction
シンボルが、`parallel_for_each` 呼び出しに対応するアクセラレータ用にコンパイルされたシェーダーの最上位関数シンボルに対応しているかどうかを示します。

## <a name="syntax"></a>構文

```C++
HRESULT get_isAcceleratorStubFunction(
   BOOL* pFlag);
```

#### <a name="parameters"></a>パラメーター
 `pFlag`

[出力] シンボルが、`parallel_for_each` 呼び出しに対応するアクセラレータ用にコンパイルされたシェーダーの最上位関数シンボルに対応しているかどうかを示す `BOOL` へのポインター。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、`S_FALSE` またはエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
