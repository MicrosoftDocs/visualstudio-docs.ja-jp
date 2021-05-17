---
description: このインターフェイスは、関数のステップアウトまたはステップオーバーの後に、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugReturnValueEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReturnValueEvent2
helpviewer_keywords:
- IDebugReturnValueEvent2
ms.assetid: 2daded43-e427-4fbb-a19e-f3834e3723af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 17eafb8f974c193fd4796cd246bf7e0a1abe929a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075706"
---
# <a name="idebugreturnvalueevent2"></a>IDebugReturnValueEvent2
このインターフェイスは、関数のステップアウトまたはステップオーバーの後に、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugReturnValueEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、このインターフェイスを実装して、ステップアウトまたはステップオーバーされた関数からの戻り値を報告します。 このインターフェイスと同じオブジェクトに、[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、このイベント オブジェクトを作成して送信し、関数の戻り値を報告します。 このイベントは、SDM がデバッグ対象のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugReturnValueEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)|関数からステップアウトまたはステップオーバーするときに返される値を取得します。|

## <a name="remarks"></a>解説
 関数によって返される値は、[GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) を呼び出すことによって取得できます。 返された値は、 **[自動変数]** ウィンドウに表示されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
