---
title: IDebugFunctionObject::Evaluate |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::Evaluate
helpviewer_keywords:
- IDebugFunctionObject::Evaluate method
ms.assetid: 29349ea3-d5c1-4135-aa76-ced073ab9683
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d56d80a10967f2ed0da82ad79905914874e73df1
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66200762"
---
# <a name="idebugfunctionobjectevaluate"></a>IDebugFunctionObject::Evaluate
関数の呼び出しをオブジェクトとして結果の値を返します。

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
[in]配列の[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)入力パラメーターを表すオブジェクト。 これらの各パラメーターは、のいずれかで作成された、`Create`メソッド、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)インターフェイス。

`dwParams`\
[in]パラメーターの数、`ppParams`配列。

`dwTimeout`\
[in]このメソッドから戻る前に待機するミリ秒単位で最大の時間を指定します。 使用`INFINITE`を無期限に待機します。

`ppResult`\
[out]返します、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトとして関数の値を表します。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを設定しで表される関数呼び出しを実行、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)オブジェクト。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)