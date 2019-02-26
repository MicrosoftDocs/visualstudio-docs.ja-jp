---
title: m_stateFlags フィールド |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_stateFlags field, Task class [.NET Framework debug engines]
ms.assetid: 82b20efc-08f2-4cd2-91f6-4e01e3da906b
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b6766fa98d6141005ed88d623ef8608035593a2a
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56704593"
---
# <a name="mstateflags-field"></a>m_stateFlags フィールド
現在の状態に関する情報を格納、<xref:System.Threading.Tasks.Task>オブジェクト。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (で*mscorlib.dll*)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文には共通中間言語 (CIL) が提供されます。

## <a name="syntax"></a>構文

```csharp
.field assembly int32 modreq(System.Runtime.CompilerServices.IsVolatile) m_stateFlags
```

## <a name="remarks"></a>Remarks
 通常、使用、<xref:System.Threading.Tasks.Task.Status%2A?displayProperty=fullName>プロパティをこの値にアクセスします。

 このメンバーは、次の値の任意の組み合わせを指定できます。

-   [TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)

-   [TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)

-   [TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)

-   [TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)

-   [TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)