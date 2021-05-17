---
description: このインターフェイスは、モジュールの読み込みまたはアンロード時にデバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugModuleLoadEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2
helpviewer_keywords:
- IDebugModuleLoadEvent2 interface
ms.assetid: 7d26fb23-5d49-4ba7-b7c5-3aed4d7be81e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6030e5962c0544a63b7b9658622447324a15792
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065360"
---
# <a name="idebugmoduleloadevent2"></a>IDebugModuleLoadEvent2
このインターフェイスは、モジュールの読み込みまたはアンロード時にデバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugModuleLoadEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、モジュールが読み込まれたかアンロードされたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、モジュールが読み込まれたかアンロードされたことを報告するために、このイベント オブジェクトを作成して送信します。 このイベントは、SDM がデバッグ中のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugModuleLoadEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)|読み込まれている、またはアンロードされているモジュールを取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、 **[モジュール]** ウィンドウを最新の状態に保つためにこのイベントを使用します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
