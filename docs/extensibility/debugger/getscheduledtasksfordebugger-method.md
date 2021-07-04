---
description: すべてのスケジュールされたタスクの配列を取得します。
title: GetScheduledTasksForDebugger メソッド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetScheduledTasksForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 7c9b4cde-6e4a-4cef-929f-7d02b1da5762
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 51da481edb636450770d0cff569b9ef411e17cf6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900955"
---
# <a name="getscheduledtasksfordebugger-method"></a>GetScheduledTasksForDebugger メソッド
すべてのスケジュールされたタスクの配列を取得します。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.method assembly hidebysig instance class System.Threading.Tasks.Task[] GetScheduledTasksForDebugger() cil managed
```

## <a name="return-value"></a>戻り値
 すべてのスケジュールされたタスクの配列。 各タスクは実行中であるか、実行が完了しています。

## <a name="remarks"></a>解説
 このメソッドはスレッド セーフではなく、<xref:System.Threading.Tasks.TaskScheduler> の他のインスタンスと同時に使用することはできません。 デバッガーで他のすべてのスレッドが中断されている場合にのみ、このメソッドをデバッガーから呼び出します。

## <a name="see-also"></a>関連項目
- [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
