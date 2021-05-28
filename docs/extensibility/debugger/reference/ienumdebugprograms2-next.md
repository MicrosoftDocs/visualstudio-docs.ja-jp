---
description: プログラムの列挙体から次の要素セットを返します。
title: IEnumDebugPrograms2::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2::Next
helpviewer_keywords:
- IEnumDebugPrograms2::Next
ms.assetid: 9120e263-e97c-4a40-ab2c-e9264ce3d6c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 347b779a4b8fea4737cc17a16f513e70a5661fff
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080023"
---
# <a name="ienumdebugprograms2next"></a>IEnumDebugPrograms2::Next
列挙体から次の要素セットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG            celt,
   IDebugProgram2** rgelt,
   ULONG*           pceltFetched
);
```

```csharp
int Next(
   uint             celt,
   IDebugProgram2[] rgelt,
   ref uint         pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[入力] 取得する要素の数。 `rgelt` 配列の最大サイズも指定します。

`rgelt`\
[入力、出力] 入力される [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 要素の配列。

`pceltFetched`\
[出力] `rgelt` で実際に返された要素の数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返すことができた要素の数が要求された数よりも少なかった場合は、`S_FALSE` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
