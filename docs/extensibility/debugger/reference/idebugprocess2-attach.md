---
description: セッション デバッグ マネージャー (SDM) をプロセスにアタッチします。
title: IDebugProcess2::Attach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Attach
helpviewer_keywords:
- IDebugProcess2::Attach
ms.assetid: 40d78417-fde2-45c3-96c9-16e06bd9008d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c518a91ae6b6de32926f922d55943d7d950b4013
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071702"
---
# <a name="idebugprocess2attach"></a>IDebugProcess2::Attach
セッション デバッグ マネージャー (SDM) をプロセスにアタッチします。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   GUID*                 rgguidSpecificEngines,
   DWORD                 celtSpecificEngines,
   HRESULT*              rghrEngineAttach
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   Guid[]               rgguidSpecificEngines,
   uint                 celtSpecificEngines,
   int[]                rghrEngineAttach
);
```

## <a name="parameters"></a>パラメーター
`pCallback`\
[入力] デバッグ イベント通知に使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`rgguidSpecificEngines`\
[入力] プロセス内で実行されているプログラムをデバッグするために使用するデバッグ エンジンの GUID の配列。 このパラメーターには、null 値を指定できます。 詳細については、「解説」を参照してください。

`celtSpecificEngines`\
[入力] `rgguidSpecificEngines` 配列内のデバッグ エンジンの数と `rghrEngineAttach` 配列のサイズ。

`rghrEngineAttach`\
[入力、出力] デバッグ エンジンによって返される HRESULT コードの配列。 この配列のサイズは、`celtSpecificEngines` パラメーターで指定します。 各コードは通常、`S_OK` または `S_ATTACH_DEFERRED` です。 後者は、DE が現在プログラムにアタッチされていないことを示します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 次の表に、可能性のあるその他の値を示します。

|値|説明|
|-----------|-----------------|
|`E_ATTACH_DEBUGGER_ALREADY_ATTACHED`|指定されたプロセスは既にデバッガーにアタッチされています。|
|`E_ATTACH_DEBUGGEE_PROCESS_SECURITY_VIOLATION`|アタッチ プロシージャ中にセキュリティ違反が発生しました。|
|`E_ATTACH_CANNOT_ATTACH_TO_DESKTOP`|デスクトップ プロセスをデバッガーにアタッチすることはできません。|

## <a name="remarks"></a>解説
 プロセスにアタッチすると、そのプロセス内で実行されているプログラムのうち、`rgguidSpecificEngines` 配列で指定されたデバッグ エンジン (DE) でデバッグ可能なすべてのプログラムに SDM がアタッチされます。 プロセス内のすべてのプログラムにアタッチするには、`rgguidSpecificEngines` パラメーターを null 値に設定するか、配列内に `GUID_NULL` を含めます。

 プロセス内で発生するすべてのデバッグ イベントは、指定された [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクトに送信されます。 この `IDebugEventCallback2` オブジェクトは、SDM がこのメソッドを呼び出すときに渡されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
