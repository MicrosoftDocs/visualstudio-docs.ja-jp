---
description: このプログラムで実行されているすべてのスレッドを停止します。
title: IDebugEngineProgram2::Stop | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::Stop
helpviewer_keywords:
- IDebugEngineProgram2::Stop
ms.assetid: 6e1c3d56-fb67-4a5b-80f9-8ee5131972bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7263756a0a8bacbbc6f90e327916cec8868d8f5c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077370"
---
# <a name="idebugengineprogram2stop"></a>IDebugEngineProgram2::Stop
このプログラムで実行されているすべてのスレッドを停止します。

## <a name="syntax"></a>構文

```cpp
HRESULT Stop( 
   void 
);
```

```csharp
int Stop();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドは、このプログラムがマルチプログラム環境でデバッグされているときに呼び出されます。 他のプログラムからの停止イベントが受信されると、このメソッドがこのプログラムで呼び出されます。 このメソッドの実装は非同期である必要があります。つまり、このメソッドから戻る前に、すべてのスレッドを停止することは必要とされません。 このメソッドの実装は、このプログラムで [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md) メソッドを呼び出すだけという簡単な場合もあります。

 実装者は、プログラムが停止したときに [IDebugStopCompleteEvent2](../../../extensibility/debugger/reference/idebugstopcompleteevent2.md) を送信する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
