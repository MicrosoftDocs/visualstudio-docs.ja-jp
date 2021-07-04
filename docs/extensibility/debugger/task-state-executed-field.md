---
description: タスクは実行中で、まだ完了していません。
title: TASK_STATE_EXECUTED フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TASK_STATE_EXECUTED field, Task class [.NET Framework debug engines]
ms.assetid: 75b8f9d0-b908-40d0-b109-70feaed2ab0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ca0d2f578cc4e20b71e562d5b82245995bfd2969
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902853"
---
# <a name="task_state_executed-field"></a>TASK_STATE_EXECUTED フィールド
タスクは実行中で、まだ完了していません。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_EXECUTED = int32(0x00020000)
```

## <a name="remarks"></a>解説
 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md) フィールドにこの値が含まれている場合、<xref:System.Threading.Tasks.Task.Status%2A> プロパティによって <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> が返されます。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
