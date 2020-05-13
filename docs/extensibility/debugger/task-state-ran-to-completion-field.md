---
title: TASK_STATE_RAN_TO_COMPLETIONフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_RAN_TO_COMPLETION field, Task class [.NET Framework debug engines]
ms.assetid: 0f4830af-fe0c-4141-b768-817f4e426b8c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4a898ff09ff45ae77da91e54ba22351e9f70978d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712626"
---
# <a name="task_state_ran_to_completion-field"></a>TASK_STATE_RAN_TO_COMPLETIONフィールド
タスクの実行は正常に完了しました。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 この内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_RAN_TO_COMPLETION = int32(0x02000000)
```

## <a name="remarks"></a>Remarks
 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドにこの値が含まれている<xref:System.Threading.Tasks.Task.Status%2A>場合、<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>プロパティは を返します。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
