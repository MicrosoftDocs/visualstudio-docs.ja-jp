---
description: タスクは、実行状態に到達する前に取り消されたか、または取り消しが確認され、例外なしで完了しました。
title: TASK_STATE_CANCELED Field | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TASK_STATE_CANCELED field, Task class [.NET Framework debug engines]
ms.assetid: f4f5a96a-8230-493d-9696-8d2716bda261
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 90b3c048edb4e52a426a2fd40d8bfd31168fea7d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900175"
---
# <a name="task_state_canceled-field"></a>TASK_STATE_CANCELED フィールド
タスクは、実行状態に到達する前に取り消されたか、または取り消しが確認され、例外なしで完了しました。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_CANCELED = int32(0x00800000)
```

## <a name="remarks"></a>解説
 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md) フィールドにこの値が含まれている場合、<xref:System.Threading.Tasks.Task.Status%2A> プロパティによって <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> が返されます。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
