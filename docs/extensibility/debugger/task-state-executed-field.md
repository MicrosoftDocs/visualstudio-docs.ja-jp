---
description: タスクは実行中で、まだ完了していません。
title: TASK_STATE_EXECUTED Field |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_EXECUTED field, Task class [.NET Framework debug engines]
ms.assetid: 75b8f9d0-b908-40d0-b109-70feaed2ab0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f035d0a55c1884deceb1a8312ff74fe0dd615bfb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079307"
---
# <a name="task_state_executed-field"></a>TASK_STATE_EXECUTED フィールド
タスクは実行中で、まだ完了していません。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_EXECUTED = int32(0x00020000)
```

## <a name="remarks"></a>解説
 [M_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドにこの値が含まれている場合、 <xref:System.Threading.Tasks.Task.Status%2A> プロパティはを返し <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> ます。

## <a name="see-also"></a>こちらもご覧ください
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
