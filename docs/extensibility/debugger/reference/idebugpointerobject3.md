---
description: 解析ツリー内のポインターを表し、IDebugPointerObject インターフェイスを拡張します。
title: IDebugPointerObject3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPointerObject3 interface
ms.assetid: 11d26af4-1079-435e-96fa-d5269cbea8eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3be0c3b96e5f9d8edb82acc2f60eefe709943243
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087523"
---
# <a name="idebugpointerobject3"></a>IDebugPointerObject3
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、「[CLR Expression Evaluators](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)」 (CLR 式エバリュエーター) と「[Managed Expression Evaluator Sample](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」 (マネージド式エバリュエーターのサンプル) をご覧ください。

 解析ツリー内のポインターを表し、**IDebugPointerObject** インターフェイスを拡張します。

## <a name="syntax"></a>構文

```
IDebugPointerObject3 : IDebugPointerObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) が、このインターフェイスを実装します。

## <a name="methods"></a>メソッド
 このインターフェイスは、[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) インターフェイスのメソッドに加えて、次のメソッドを実装しています。

|メソッド|説明|
|------------|-----------------|
|[GetPointerAddress](../../../extensibility/debugger/reference/idebugpointerobject3-getpointeraddress.md)|ポインターのアドレスを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
