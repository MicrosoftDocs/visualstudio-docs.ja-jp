---
description: IDiaStackWalkHelper::put_registerValue は、レジスタの値を設定します。
title: IDiaStackWalkHelper::put_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::put_registerValue method
ms.assetid: 8f02ce54-ef59-455f-8aa6-dc26761c7aff
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fdc66faea9537759e9754ce799339175db585673
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634777"
---
# <a name="idiastackwalkhelperput_registervalue"></a>IDiaStackWalkHelper::put_registerValue
レジスタの値を設定します。

## <a name="syntax"></a>構文

```C++
HRESULT put_registerValue ( 
   DWORD     index,
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>パラメーター
 `index`

[入力] 書き込み先のレジスタを指定する [CV_HREG_e 列挙型](../../debugger/debug-interface-access/cv-hreg-e.md) の列挙体からの値。

 `NewVal`

[入力] 新しいレジスタ値。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 値のサイズに関係なく、レジストリに通常、保持されるものだけ実装で格納します。 たとえば、8 ビットのレジスタであれば、指定の値の下位 8 ビットだけ保持します。

## <a name="see-also"></a>関連項目
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [CV_HREG_e 列挙型](../../debugger/debug-interface-access/cv-hreg-e.md)
