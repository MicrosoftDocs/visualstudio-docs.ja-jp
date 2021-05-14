---
description: このプロセスでコードを実行している次のプログラムが停止し、IDebugBreakEvent2 イベント オブジェクトを送信するように要求します。
title: IDebugProcess2::CauseBreak | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CauseBreak
helpviewer_keywords:
- IDebugProcess2::CauseBreak
ms.assetid: efda8865-2319-4d53-90bf-6d9d74cd5195
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c79fbc17f02a49a1bbab416473bb99e201c24526
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071676"
---
# <a name="idebugprocess2causebreak"></a>IDebugProcess2::CauseBreak
このプロセスでコードを実行している次のプログラムが停止し、[IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) イベント オブジェクトを送信するように要求します。

## <a name="syntax"></a>構文

```cpp
HRESULT CauseBreak( 
   void
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
