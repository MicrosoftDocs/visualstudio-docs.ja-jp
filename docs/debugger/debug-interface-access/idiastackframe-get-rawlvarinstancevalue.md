---
description: このメソッドは、指定されたローカル変数の値を生バイトとして取得します。
title: IDiaStackFrame::get_rawLVarInstanceValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_rawLVarInstanceValue method
ms.assetid: ce526259-85a6-475b-9274-0b3a21d95db2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dc7bc12fe8fd38fc02b6794b2026bce328d95511
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634274"
---
# <a name="idiastackframeget_rawlvarinstancevalue"></a>IDiaStackFrame::get_rawLVarInstanceValue
このメソッドは、指定されたローカル変数の値を生バイトとして取得します。

## <a name="syntax"></a>構文

```C++
HRESULT get_rawLVarInstanceValue(
   IDiaLVarInstance* pInstance,
   DWORD             cbDataMax,
   DWORD*            pcbData,
   BYTE*             pbData
);
```

#### <a name="parameters"></a>パラメーター
 `pInstance`

[入力] 値を取得するローカル変数のインスタンスを表す `IDiaLVarInstance` オブジェクト。

 `cbDataMax`

[入力] `pbData` によってポイントされるバッファー内の最大バイト数。 これは、最大 8 バイトにすることができます (`sizeof(ULONGLONG)`)。

 `pcbData`

[出力] バッファーに格納されている実際のバイト数を返します。

 `pbData`

[出力] データを格納するバッファー。 これは `NULL` にすることはできません。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
