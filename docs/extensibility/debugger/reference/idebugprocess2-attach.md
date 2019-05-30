---
title: IDebugProcess2::Attach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24a83c13d8953e3725a5fc5a4e55153b9ade88c4
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353247"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
セッション デバッグ マネージャー (SDM) をプロセスにアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
[in][IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)デバッグ イベント通知のために使用されるオブジェクト。

`rgguidSpecificEngines`\
[in]プロセスで実行するプログラムのデバッグに使用するデバッグ エンジンの Guid の配列。 このパラメーターは、null 値を指定できます。 詳細については、「解説」を参照してください。

`celtSpecificEngines`\
[in]エンジンでのデバッグの数、`rgguidSpecificEngines`配列とのサイズ、`rghrEngineAttach`配列。

`rghrEngineAttach`\
[入力、出力]デバッグ エンジンによって返される HRESULT コードの配列。 この配列のサイズがで指定された、`celtSpecificEngines`パラメーター。 各コードは、いずれかで、通常`S_OK`または`S_ATTACH_DEFERRED`します。 後者の場合は、DE がプログラムに現在接続されていることを示しません。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。 次の表では、使用可能なその他の値を示します。

|値|説明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定されたプロセスがデバッガーに既に結び付けられています。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|アタッチ時にセキュリティ違反が発生しました。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|デスクトップのプロセスをデバッガーにアタッチできません。|

## <a name="remarks"></a>Remarks
 指定されたデバッグ エンジン (DE) でデバッグできるプロセスで実行されているすべてのプログラム、SDM をアタッチするプロセスにアタッチ、`rgguidSpecificEngines`配列。 設定、`rgguidSpecificEngines`パラメーターを null に値を含めたり`GUID_NULL`プロセス内のすべてのプログラムにアタッチする配列。

 プロセスで発生するすべてのデバッグ イベントに送信される、指定された[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクト。 これは、 `IDebugEventCallback2` SDM は、このメソッドを呼び出すときにオブジェクトが提供されます。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)