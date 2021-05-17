---
description: プログラム (1 つまたは複数) にデバッグ エンジン (DE) をアタッチします。
title: IDebugEngine2::Attach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 38275cc623fcb8b30646c9d84ef194f584369ef2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093913"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
プログラム (1 つまたは複数) にデバッグ エンジン (DE) をアタッチします。 DE が SDM に対してインプロセスで実行されているときに、セッション デバッグ マネージャー (SDM) によって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT Attach( 
   IDebugProgram2**      pProgram,
   IDebugProgramNode2**  rgpProgramNodes,
   DWORD                 celtPrograms,
   IDebugEventCallback2* pCallback,
   ATTACH_REASON         dwReason
);
```

```csharp
int Attach( 
   IDebugProgram2[]     pProgram,
   IDebugProgramNode2[] rgpProgramNodes,
   uint                 celtPrograms,
   IDebugEventCallback2 pCallback,
   Enum_ATTACH_REASON   dwReason
);
```

## <a name="parameters"></a>パラメーター
`pProgram`\
[入力] アタッチするプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトの配列。 これらはポート プログラムです。

`rgpProgramNodes`\
[入力] プログラムごとに 1 つのプログラム ノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの配列。 この配列のプログラム ノードは、`pProgram` と同じプログラムを表します。 プログラム ノードは、アタッチするプログラムを DE が識別できるように指定されます。

`celtPrograms`\
[入力] `pProgram` および `rgpProgramNodes` 配列内のプログラムまたはプログラム ノードの数。

`pCallback`\
[入力] デバッグ イベントを SDM に送信するために使用される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクト。

`dwReason`\
[入力] これらのプログラムをアタッチする理由を指定する [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) 列挙型の値。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 プログラムにアタッチする理由には、次の 3 つがあります。

- `ATTACH_REASON_LAUNCH` は、ユーザーがプログラムを含むプロセスを起動したため、DE がそれにアタッチしていることを示します。

- `ATTACH_REASON_USER` は、ユーザーが DE にプログラム (またはプログラムが含まれているプロセス) にアタッチするよう明示的に要求したことを示します。

- `ATTACH_REASON_AUTO` は、特定のプロセス内の他のプログラムを既にデバッグ中のため、DE が特定のプログラムにアタッチしていることを示します。 これは、自動アタッチとも呼ばれます。

  このメソッドが呼び出された場合、DE は次のイベントを、次の順序で送信する必要があります。

1. [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) (デバッグ エンジンの特定のインスタンスに対してまだ送信されていない場合)

2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)

3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)

   さらに、アタッチする理由が `ATTACH_REASON_LAUNCH` の場合、DE では [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) イベントを送信する必要があります。

   DE では、デバッグ中のプログラムに対応する [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトを取得した後、任意のプライベート インターフェイスに対してクエリを実行できます。

   `pProgram` または `rgpProgramNodes` によって指定された配列内のプログラム ノードのメソッドを呼び出す前に、プログラム ノードを表す `IDebugProgram2` インターフェイスで、必要に応じて偽装を有効にする必要があります。 ただし、通常、この手順は必要ありません。 詳細については、[セキュリティの問題](../../../extensibility/debugger/security-issues.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)
- [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)
