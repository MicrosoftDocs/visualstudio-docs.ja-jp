---
description: このインターフェイスは、ユーザーからの応答を必要とするメッセージを Visual Studio に送信するために、デバッグ エンジン (DE) によって使用されます。
title: IDebugMessageEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2
helpviewer_keywords:
- IDebugMessageEvent2 interface
ms.assetid: a9ff3d00-e9ac-4cd6-bda9-584a4815aff8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5593e822b974ddb7c666f622192e3e4630b7222
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058431"
---
# <a name="idebugmessageevent2"></a>IDebugMessageEvent2
このインターフェイスは、ユーザーからの応答を必要とするメッセージを Visual Studio に送信するために、デバッグ エンジン (DE) によって使用されます。

## <a name="syntax"></a>構文

```
IDebugMessageEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 ユーザーの応答を必要とするメッセージを Visual Studio に送信するために、DE によりこのインターフェイスが実装されます。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 `IDebugEvent2` インターフェイスにアクセスするために SDM によって [QueryInterface](/cpp/atl/queryinterface) が使用されます。

 このインターフェイスの実装では、Visual Studio の [SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md) の呼び出しを DE に伝達する必要があります。 たとえば、DE のメッセージ処理スレッドにポストされるメッセージを使用してこれを行うことができます。また、このインターフェイスを実装するオブジェクトでは、DE への参照を保持し、`IDebugMessageEvent2::SetResponse` に渡された応答を使用して DE にコールバックすることもできます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE により、このイベント オブジェクトが作成、送信され、応答を必要とするメッセージをユーザーに表示します。 このイベントは、SDM がデバッグ中のプログラムにアタッチされたときに提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugMessageEvent2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetMessage](../../../extensibility/debugger/reference/idebugmessageevent2-getmessage.md)|表示されるメッセージを取得します。|
|[SetResponse](../../../extensibility/debugger/reference/idebugmessageevent2-setresponse.md)|応答がある場合、メッセージ ボックスからそれを設定します。|

## <a name="remarks"></a>解説
 DE では、特定のメッセージに対してユーザーからの特定の応答が必要な場合に、このインターフェイスが使用されます。 たとえば、プログラムにリモートでアタッチしようとした後に "アクセスが拒否されました" というメッセージを取得した場合、DE によりメッセージ ボックス スタイル `MB_RETRYCANCEL` の `IDebugMessageEvent2` イベントでこの特定のメッセージを Visual Studio に送信します。 これにより、ユーザーはアタッチ操作を再試行またはキャンセルできます。

 DE では、Win32 関数 `MessageBox` の規則に従うことによって、このメッセージを処理する方法を指定します (詳細については、[AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) に関するページを参照してください)。

 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) インターフェイスを使用して、ユーザーからの応答を必要としないメッセージを Visual Studio に送信します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
