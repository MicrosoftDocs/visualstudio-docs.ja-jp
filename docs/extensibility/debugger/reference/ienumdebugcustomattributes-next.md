---
title: IEnumDebugCustomAttributes::Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes::Next
helpviewer_keywords:
- IEnumDebugCustomAttributes::Next
ms.assetid: e36f856b-2619-42d1-b73e-4f2390fc22bd
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fdad468c788d475d32eddca160728b2c3ecf11d9
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56683716"
---
# <a name="ienumdebugcustomattributesnext"></a>IEnumDebugCustomAttributes::Next
指定された数の列挙体シーケンス内のカスタム属性を取得します。

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

#### <a name="parameters"></a>パラメーター
 `celt`

 [in]取得する要素の数。 最大サイズを指定します、`rgelt`配列。

 `rgelt`

 [out]配列の[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)情報を格納するオブジェクト。

 `pceltFetched`

 [out]実際に返される要素の数を返します`rgelt`します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返します`S_FALSE`返される可能性があります、要求された要素数よりも少ない場合、それ以外の場合、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)