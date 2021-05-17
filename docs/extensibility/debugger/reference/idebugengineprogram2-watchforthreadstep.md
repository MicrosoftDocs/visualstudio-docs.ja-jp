---
description: 指定されたスレッドで実行が発生するのを監視します (または実行の監視を停止します)。
title: IDebugEngineProgram2::WatchForThreadStep | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2::WatchForThreadStep
helpviewer_keywords:
- IDebugEngineProgram2::WatchForThreadStep
ms.assetid: b70922a3-1313-409a-b3b7-50c7cd13e394
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ddf7de557a5059a83aabdbfad7045e8dacbc71b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093835"
---
# <a name="idebugengineprogram2watchforthreadstep"></a>IDebugEngineProgram2::WatchForThreadStep
指定されたスレッドで実行が発生するのを監視します (または実行の監視を停止します)。

## <a name="syntax"></a>構文

```cpp
HRESULT WatchForThreadStep( 
   IDebugProgram2* pOriginatingProgram,
   DWORD           dwTid,
   BOOL            fWatch,
   DWORD           dwFrame
);
```

```csharp
int WatchForThreadStep( 
   IDebugProgram2 pOriginatingProgram,
   uint           dwTid,
   int            fWatch,
   uint           dwFrame
);
```

## <a name="parameters"></a>パラメーター
`pOriginatingProgram`\
[入力] ステップ実行されているプログラムを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`dwTid`\
[入力] 監視するスレッドの識別子を指定します。

`fWatch`\
[入力] ゼロ以外 (`TRUE`) は、`dwTid` で識別されるスレッドで実行の監視を開始することを意味します。それ以外の場合、ゼロ (`FALSE`) は `dwTid` での実行の監視を停止することを意味します。

`dwFrame`\
[入力] ステップの種類を制御するフレーム インデックスを指定します。 この値がゼロ (0) の場合、ステップの種類は "ステップ イン" であり、プログラムは `dwTid` で識別されるスレッドが実行されるたびに停止します。 `dwFrame` がゼロ以外の場合、ステップの種類は "ステップ オーバー" であり、プログラムは、`dwTid` で識別されるスレッドが、スタック上でインデックスが `dwFrame` 以上のフレームで実行されている場合にのみ停止します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 セッション デバッグ マネージャー (SDM) は、`pOriginatingProgram` パラメーターで識別されるプログラムをステップ実行するときに、このメソッドを呼び出すことによって、アタッチされている他のすべてのプログラムに通知します。

 このメソッドは、同じスレッドのステップ実行にのみ適用できます。

## <a name="see-also"></a>関連項目
- [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
