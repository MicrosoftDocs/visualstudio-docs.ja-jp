---
title: IDebugProgramNode2::DetachDebugger_V7 | Microsoft Docs
description: このメソッドは、Visual Studio 2005 より前に使用されていた、以前の非推奨になった形式の detach メソッドです。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 16630be49dd884f8bcc82da2fead158eb3a25e5e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053556"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 非推奨。 使用しないでください。

## <a name="syntax"></a>構文

```cpp
HRESULT DetachDebugger_V7 (
   void 
);
```

```csharp
int DetachDebugger_V7 ();
```

## <a name="return-value"></a>戻り値

実装では、常に `E_NOTIMPL` を返す必要があります。

## <a name="remarks"></a>解説

> [!WARNING]
> Visual Studio 2005 以降では、このメソッドは使用されなくなり、常に `E_NOTIMPL` を返す必要があります。

このメソッドは、デバッガーが予期せず終了したときに呼び出されます。 このメソッドが呼び出されると、DE によって、ユーザーがそのプログラムからデタッチした場合と同様にプログラムが再開されます。 これ以上デバッグ イベントを送信することはできません。 プログラムは、デバッガーの別のインスタンスからアタッチできる状態である必要があります。

## <a name="see-also"></a>関連項目

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
