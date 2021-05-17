---
description: このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) では、デバッグ エンジン (DE) を表すインターフェイスを取得できます。
title: IDebugQueryEngine2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 899c5dceab16d4783cb28bff31c67e67bf5df774
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083649"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) では、デバッグ エンジン (DE) を表すインターフェイスを取得できます。

## <a name="syntax"></a>構文

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、DE 自体の [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) インターフェイスへのアクセスを許可するために、最も一般的な DE インターフェイス ([IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)、[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)、[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) など) を実装するオブジェクトに対してこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 一般的な DE インターフェイスを取得するには、このインターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugQueryEngine2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|カスタム デバッグ エンジン (DE) インターフェイスを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは通常、関数を使用した因果関係の順序のステップ実行をサポートするために、[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを実装するオブジェクトに実装されます。つまり、デバッガーが関数からステップ アウトすると、次に実行される関数がスタック上の前の関数ではなく、要するに別のスレッドの関数になることがあります。 "因果関係" の定義については、「[Visual Studio デバッガーの用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
