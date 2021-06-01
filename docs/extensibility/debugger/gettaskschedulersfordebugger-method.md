---
description: 現在アクティブなすべての System.Threading.Tasks.TaskScheduler オブジェクトの配列を取得します。
title: GetTaskSchedulersForDebugger メソッド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d024e44dee8e7513d862e3d299c2ed2b9e53cd5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054856"
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
