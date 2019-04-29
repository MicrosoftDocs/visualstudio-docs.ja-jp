---
title: IDebugExpressionEvaluator::GetMethodLocationProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c15baa5475e912559b8cc0a23264b0c19ef8a464
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874193"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
このメソッドは、メモリ アドレスにメソッドの場所とオフセットを変換します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMethodLocationProperty( 
   LPCOLESTR             upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodLocationProperty(
   string               upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   out IDebugProperty2  ppProperty
);
```

#### <a name="parameters"></a>パラメーター
 `upstrFullyQualifiedMethodPlusOffset`

 [in]メソッドの場所とのオフセットは、文字列として表されます。

 `pSymbolProvider`

 [in]シンボル プロバイダーで表した、 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)オブジェクト。

 `pAddress`

 [in]表されるメソッド内のアドレス、 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)オブジェクト。

 `pBinder`

 [in]バインダーで表した、 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクト。

 `ppProperty`

 [out]返します、 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)メモリ アドレスを表すインターフェイスです。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 たとえば、ブレークポイントを設定するのには、返されたアドレスを使用できます。

 名前に関係なく`upstrFullyQualifiedMethodPlusOffset`、このパラメーターは、部分的に修飾メソッド名を渡すことができます。 選択したメソッドを囲む、1 つは、その場合は、`pAddress`します。 このパラメーターを解釈する方法は、式エバリュエーターと言語のサポートの実装の責任です。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)