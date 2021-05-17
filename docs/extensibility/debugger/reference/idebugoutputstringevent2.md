---
description: このインターフェイスは、文字列を出力するために、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。
title: IDebugOutputStringEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4576914ada9a575569ce09c120dbbd9bc11fdfa9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084650"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
このインターフェイスは、文字列を出力するために、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugOutputStringEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、このインターフェイスを実装して、IDE の **[出力]** ウィンドウに文字列を送信します。 このインターフェイスと同じオブジェクトに、[IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスを実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE では、このイベント オブジェクトを作成して送信し、 **[出力]** ウィンドウに文字列を送信します。 このイベントは、SDM がデバッグ中のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugOutputStringEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|表示可能なメッセージを取得します。|

## <a name="remarks"></a>解説
 たとえば、アンマネージド コードでは、デバッグされているプログラムで Win32 `OutputDebugString` 関数に文字列が送信されたときに、出力される文字列が生成されます。 この文字列は DE によってインターセプトされ、`IDebugOutputStringEvent2` イベントとして SDM に送信されます。

 ユーザーの応答を必要とするメッセージを送信するには、[IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) を使用します。

 応答を必要としないエラー メッセージを送信するには、[IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) を使用します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
