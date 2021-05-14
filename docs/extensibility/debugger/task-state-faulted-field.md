---
description: タスクはハンドルされない例外が発生したために終了しました。
title: TASK_STATE_FAULTED フィールド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_FAULTED field, Task class [.NET Framework debug engines]
ms.assetid: ced826ae-09a9-4acf-af00-a2343d396bb8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f01c222686ab2c03acc05dcd08beabd305119300
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079255"
---
# <a name="task_state_faulted-field"></a>TASK_STATE_FAULTED フィールド
タスクはハンドルされない例外が発生したために終了しました。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.field static assembly literal int32 TASK_STATE_FAULTED = int32(0x00400000)
```

## <a name="remarks"></a>解説
 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md) フィールドにこの値が含まれている場合、<xref:System.Threading.Tasks.Task.Status%2A> プロパティは <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> を返します。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
