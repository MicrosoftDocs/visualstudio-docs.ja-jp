---
description: 列挙シーケンス内の指定された数のカスタム属性を取得します。
title: IEnumDebugCustomAttributes::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::Next
helpviewer_keywords:
- IEnumDebugCustomAttributes::Next
ms.assetid: e36f856b-2619-42d1-b73e-4f2390fc22bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8b1e65f993d91bedde8fb02631a0e2c369d43522
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083090"
---
# <a name="ienumdebugcustomattributesnext"></a>IEnumDebugCustomAttributes::Next
列挙シーケンス内の指定された数のカスタム属性を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next ( 
   ULONG      celt,
   CODE_PATH* rgelt,
   ULONG*     pceltFetched
);
```

```csharp
int Next(
   uint                        celt,
   out IDebugCustomAttribute[] rgelt,
   ref uint                    pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in] 取得する要素の数。 `rgelt` 配列の最大サイズも指定します。

`rgelt`\
[out] 入力される [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) オブジェクトの配列。

`pceltFetched`\
[out] `rgelt` で実際に返された要素の数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返すことができた要素の数が要求された数よりも少なかった場合は、`S_FALSE` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
