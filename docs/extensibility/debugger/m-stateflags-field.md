---
description: System.Threading.Tasks.Task オブジェクトの現在の状態に関する情報を格納します。
title: m_stateFlags フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- m_stateFlags field, Task class [.NET Framework debug engines]
ms.assetid: 82b20efc-08f2-4cd2-91f6-4e01e3da906b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0bf584511bc2f0ee43429abe83dea3d7a45259d9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898914"
---
# <a name="m_stateflags-field"></a>m_stateFlags フィールド
<xref:System.Threading.Tasks.Task> オブジェクトの現在の状態に関する情報を格納します。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.field assembly int32 modreq(System.Runtime.CompilerServices.IsVolatile) m_stateFlags
```

## <a name="remarks"></a>解説
 この値にアクセスするには、通常 <xref:System.Threading.Tasks.Task.Status%2A?displayProperty=fullName> プロパティを使用します。

 このメンバーには、次の値の任意に組み合わせが可能です。

- [TASK_STATE_EXECUTED](../../extensibility/debugger/task-state-executed-field.md)

- [TASK_STATE_FAULTED](../../extensibility/debugger/task-state-faulted-field.md)

- [TASK_STATE_CANCELED](../../extensibility/debugger/task-state-canceled-field.md)

- [TASK_STATE_WAITING_ON_CHILDREN](../../extensibility/debugger/task-state-waiting-on-children-field.md)

- [TASK_STATE_RAN_TO_COMPLETION](../../extensibility/debugger/task-state-ran-to-completion-field.md)

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
