---
description: IDebugFunctionObject::Evaluate は、関数を呼び出して、結果の値をオブジェクトとして返します。
title: IDebugFunctionObject::Evaluate | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::Evaluate
helpviewer_keywords:
- IDebugFunctionObject::Evaluate method
ms.assetid: 29349ea3-d5c1-4135-aa76-ced073ab9683
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b9770878040422d96c31fab8d57df468af614e8e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063592"
---
# <a name="idebugfunctionobjectevaluate"></a>IDebugFunctionObject::Evaluate
関数を呼び出し、結果の値をオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Evaluate( 
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate(
   IDebugObject[]   ppParams,
   IntPtr           dwParams,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
[入力] 入力パラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。 これらの各パラメーターは、[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) インターフェイスの `Create` メソッドのいずれかを使用して作成されたものです。

`dwParams`\
[入力] `ppParams` 配列内のパラメーターの数。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位) を指定します。 待機時間を指定しない場合は `INFINITE` を使用します。

`ppResult`\
[出力] 関数の値をオブジェクトとして表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK が返されます。それ以外の場合は、エラー コードが返されます。

## <a name="remarks"></a>解説
 このメソッドは、[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクトによって表される関数の呼び出しをセットアップおよび実行します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
