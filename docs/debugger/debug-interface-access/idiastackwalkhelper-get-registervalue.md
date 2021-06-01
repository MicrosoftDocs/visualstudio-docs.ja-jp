---
description: IDiaStackWalkHelper::get_registerValue を使用すると、レジスタの値を取得できます。
title: IDiaStackWalkHelper::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fa87529f90b20d7d9099dd76e294e406ae0c7a08
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108635183"
---
# <a name="idiastackwalkhelperget_registervalue"></a>IDiaStackWalkHelper::get_registerValue
レジスタの値を取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_registerValue ( 
   DWORD      index,
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>パラメーター
 `index`

[入力] 値を取得するレジスタを指定する [CV_HREG_e 列挙型](../../debugger/debug-interface-access/cv-hreg-e.md)の列挙体の値。

 `pRetVal`

[出力] レジスタの現在の値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 `pRetVal` パラメーターのサイズに関係なく、通常、レジストリに保持されるものだけ実装で格納します。 たとえば、8 ビットのレジスタであれば、指定の値の下位 8 ビットだけ保持します。 この 8 ビット値は、このメソッドから返されるときに 64 ビットに拡張されます。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [CV_HREG_e 列挙型](../../debugger/debug-interface-access/cv-hreg-e.md)
