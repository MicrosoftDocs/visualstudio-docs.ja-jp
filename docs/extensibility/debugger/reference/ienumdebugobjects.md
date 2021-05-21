---
description: このインターフェイスは、IDebugObject インターフェイスを実装するオブジェクトのコレクションを表します。
title: IEnumDebugObjects | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d9cd15c267906730ea94636e94978f5f77374e6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052828"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーターに関するページ](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージド式エバリュエーターのサンプルに関するページ](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)をご覧ください。

 このインターフェイスは、[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、このインターフェイスを実装して、[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスを実装するオブジェクトのセットを提供します。 [GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md) メソッドが存在するため、これは標準の COM 列挙ではないことにご注意ください。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md) は、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスには、次のメソッドが実装されています。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|列挙から [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの次のセットを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|指定された数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|列挙を最初の要素にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|現在の列挙のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|列挙のエントリの数を取得します。|

## <a name="remarks"></a>解説
 デバッグ エンジンがこのインターフェイスを使用して、配列内のオブジェクトのセットを列挙できます。

## <a name="requirements"></a>要件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)
