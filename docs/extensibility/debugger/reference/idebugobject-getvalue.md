---
title: IDebugObject::GetValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetValue
helpviewer_keywords:
- IDebugObject::GetValue method
ms.assetid: eec6051e-8ecb-49fa-bdd4-dd786f211692
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59d58e136045bb4177755c981f91974f9ac2fa77
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323644"
---
# <a name="idebugobjectgetvalue"></a>IDebugObject::GetValue
連続した一連のバイトとしてオブジェクトの値を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int GetValue(
   ref byte[] pValue,
   uint nSize
);
```

## <a name="parameters"></a>パラメーター
`pValue`\
[入力、出力]入力が連続する一連のオブジェクトの値を表すバイト配列。

`nSize`\
[in]フェッチするバイトの最大数。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 呼び出すことでフェッチできる値のバイトの合計数を取得、 [GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)メソッド。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)