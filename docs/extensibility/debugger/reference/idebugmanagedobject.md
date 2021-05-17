---
description: このインターフェイスを使用すると、式エバリュエーター (EE) では、値クラスのインスタンス (たとえば、System.Decimal) でプロパティまたはメソッドを呼び出したり、デバッグ中のプログラムで Evaluate を呼び出さずに値を設定したりすることができます。
title: IDebugManagedObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88eadb33aaccc09a7c4667ad01d9acee538169f2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076863"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスを使用すると、式エバリュエーター (EE) では、値クラスのインスタンス (たとえば、`System.Decimal`) でプロパティまたはメソッドを呼び出したり、デバッグ中のプログラムで [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) を呼び出さずに値を設定したりすることができます。

## <a name="syntax"></a>構文

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、変数などのマネージド コード オブジェクトを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、値クラスのインスタンスを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) で [GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugManagedObject` インターフェイスでは、[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) から継承されたメソッドに加えて以下のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|マネージド コード オブジェクトを表し、このインターフェイスから適切なマネージド コード インターフェイスを取得できるインターフェイスを返します。|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|このオブジェクトの値を、指定したマネージド コード オブジェクトの値に設定します。|

## <a name="remarks"></a>解説
 式エバリュエーターでは、このインターフェイスを使用して、マネージド コード オブジェクトを解析ツリーに格納します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
