---
description: 現在アクティブなすべての System.Threading.Tasks.TaskScheduler オブジェクトの配列を取得します。
title: GetTaskSchedulersForDebugger メソッド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58cb913f5dbc729c297de8a34aa5dd4c3c99b48a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900916"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger メソッド
現在アクティブなすべての <xref:System.Threading.Tasks.TaskScheduler> オブジェクトの配列を取得します。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (*mscorlib.dll* 内)

 この内部メンバーには、.NET Framework からはアクセスできないため、次の構文では共通中間言語 (CIL) を使用しています。

## <a name="syntax"></a>構文

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>戻り値
 この <xref:System.AppDomain> 内で現在アクティブなすべての <xref:System.Threading.Tasks.TaskScheduler> オブジェクトの配列。

## <a name="remarks"></a>解説
 このメソッドはスレッド セーフではなく、<xref:System.Threading.Tasks.TaskScheduler> の他のインスタンスと同時に使用することはできません。 デバッガーで他のすべてのスレッドが中断されている場合にのみ、このメソッドをデバッガーから呼び出します。

## <a name="see-also"></a>関連項目
- [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)
