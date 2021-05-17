---
description: このインターフェイスは、列挙型を表します。
title: IDebugEnumField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 18671f8f719dc797709677a14417eaa0a54aaea2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092528"
---
# <a name="idebugenumfield"></a>IDebugEnumField
このインターフェイスは、列挙型を表します。

## <a name="syntax"></a>構文

```
IDebugEnumField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーは、列挙型を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) が `FIELD_TYPE_ENUM` を返す場合に、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスからこのインターフェイスを取得するには、[QueryInterface](/cpp/atl/queryinterface) を使用します。

## <a name="methods-in-vtable-order"></a>VTable 順序のメソッド
 このインターフェイスは、`IDebugField` および `IDebugContainerField` インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|この列挙型の名前を記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。|
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|指定された値に関連付けられている列挙定数の名前を返します。|
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|指定された列挙定数名に関連付けられている値を返します|
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|指定された列挙定数名に関連付けられている値を返しますが、大文字と小文字は区別しません。|

## <a name="remarks"></a>解説
 これは、[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md) がある場所に実際にバインドされている、基になるシンボルです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
