---
description: このインターフェイスは、シンボルと式の値をカプセル化するためにバインダーによって作成されるオブジェクトを表します。
title: IDebugObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 18355c5b21f8df0fde5faa31caf8d64fb8f3f3fe
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054167"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスは、シンボルと式の値をカプセル化するためにバインダーによって作成されるオブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、オブジェクトを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、式エバリュエーターによって解析された式で使用されるすべてのオブジェクトの基底クラスです。 これは、[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md) メソッドの呼び出しによって返されます。 [QueryInterface](/cpp/atl/queryinterface) では、このインターフェイスからより特殊化されたインターフェイスが取得されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugObject` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|オブジェクトのサイズを取得します。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|オブジェクトの値を連続する一連のバイトとして取得します。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|連続する一連のバイトからオブジェクトの値を設定します。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|このオブジェクトの参照値を設定します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|オブジェクトの値のアドレスを表すメモリ コンテキストを取得します。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|デバッグ エンジンのアドレス空間にマネージド オブジェクトのコピーを作成します。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|このオブジェクトが null 参照であるかどうかをテストします。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|オブジェクトをこれと比較します。|
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|このオブジェクトが読み取り専用かどうかを判定します。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|オブジェクトが透過的プロキシかどうかを判定します。|

## <a name="remarks"></a>解説
 式エバリュエーターでは、このインターフェイスを基底クラスとして使用して、解析ツリー内のオブジェクトを表します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
