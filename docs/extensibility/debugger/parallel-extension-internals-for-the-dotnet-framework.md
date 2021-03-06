---
title: .NET Framework の並列拡張機能の内部 | Microsoft Docs
description: これらのリソースでは、.NET Framework の並列拡張機能用のカスタム デバッガーを実装するために使用されるクラスの内部型、メソッド、およびフィールドについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 858bf85e65cd761e7f881856286578495db6143a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903009"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>.NET Framework の並列拡張機能の内部
このセクションでは、.NET Framework の並列拡張機能用のカスタム デバッガーを実装するために役立つクラスの内部型、メソッド、およびフィールドについて説明します。

## <a name="in-this-section"></a>このセクションの内容
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md) <xref:System.Threading.Tasks.Task?displayProperty=fullName> クラスの内部データ メンバーについて説明します。

 [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md) <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> クラスの内部データ メンバーについて説明します。

 [ContingentProperties クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md) `System.Threading.Tasks.ContingentProperties` クラスの内部データ メンバーについて説明します。

 [AsyncTaskMethodBuilder 構造体](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md) <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> 構造体の内部メンバーについて説明します。

 [AsyncTaskMethodBuilder\<TResult> 構造体](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md) <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> 構造体の内部メンバーについて説明します。

 [AsyncVoidMethodBuilder 構造体](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md) <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> 構造体の内部メンバーについて説明します。

## <a name="see-also"></a>こちらもご覧ください
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [Visual Studio デバッガーの拡張性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [並列プログラミング](/dotnet/standard/parallel-programming/index)
