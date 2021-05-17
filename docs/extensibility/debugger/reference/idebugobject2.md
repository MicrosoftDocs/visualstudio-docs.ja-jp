---
description: このインターフェイスでは、オブジェクトに関する追加情報が提供されます。
title: IDebugObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c5e3b3f05ae205e30cff7085b71c1690d02c73e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084689"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスでは、オブジェクトに関する追加情報が提供されます。

## <a name="syntax"></a>構文

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、このインターフェイスを実装して、エイリアスと、オブジェクトに関する情報へのアクセスをサポートします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスでは、[QueryInterface](/cpp/atl/queryinterface) を使用してこのインターフェイスを取得できます。 また、[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) ではこのインターフェイスが返されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugObject2` インターフェイスでは、[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスのメソッドに加えて、次のものが実装されます。

|メソッド|説明|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|このオブジェクトによって表されるプロパティをバッキングしている可能性があるフィールドまたは変数 (存在する場合) を取得します。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|このオブジェクトの値を表すマネージド コード オブジェクトを取得します。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|このオブジェクトの一意の ID を作成するか、既存のエイリアスを返します。|
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|このオブジェクトに関連付けられているエイリアスを取得します (存在する場合)。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|このオブジェクトの型を取得します。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|このオブジェクトがユーザー データを表しているかどうかを判別します。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|エディット コンティニュの状態が無効になっているかどうかを判別します。<br /><br /> カスタム式エバリュエーターでは、このメソッドは実装されません (常に `E_NOTIMPL` を返す必要があります)。|

## <a name="remarks"></a>解説
 エイリアスの詳細については、「[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
