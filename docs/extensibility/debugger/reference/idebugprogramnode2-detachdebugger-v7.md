---
title: IDebugProgramNode2::D etachDebugger_V7 |Microsoft Docs
description: このメソッドは、Visual Studio 2005 より前に使用されていたデタッチメソッドの古い形式です。
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
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053556"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> れ. 使用しないでください。

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

実装は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="remarks"></a>注釈

> [!WARNING]
> Visual Studio 2005 の時点では、このメソッドは使用されなくなり、常にを返す必要があり `E_NOTIMPL` ます。

このメソッドは、デバッガーが予期せず終了したときに呼び出されます。 このメソッドが呼び出されると、DE は、ユーザーがそのプログラムからデタッチした場合と同様にプログラムを再開します。 これ以上デバッグイベントを送信することはできません。 プログラムは、デバッガーの別のインスタンスからアタッチできる状態である必要があります。

## <a name="see-also"></a>こちらもご覧ください

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
