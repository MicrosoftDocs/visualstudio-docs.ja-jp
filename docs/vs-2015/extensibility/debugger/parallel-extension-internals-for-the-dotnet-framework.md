---
title: .NET Framework | の並列拡張機能の内部構造Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42c472190469e7d008fa8c525f50eabfaf37053f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65680935"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>.NET Framework の並列拡張機能の内部
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このセクションでは、.NET Framework に対する並列拡張のカスタムデバッガーを実装するのに役立つクラスの内部型、メソッド、およびフィールドについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md)  
 クラスの内部データメンバーについて説明し <xref:System.Threading.Tasks.Task?displayProperty=fullName> ます。  
  
 [TaskScheduler クラス](../../extensibility/debugger/taskscheduler-class-internal-members.md)  
 クラスの内部データメンバーについて説明し <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> ます。  
  
 [ContingentProperties クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md)  
 クラスの内部データメンバーについて説明し `System.Threading.Tasks.ContingentProperties` ます。  
  
 [AsyncTaskMethodBuilder 構造体](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md)  
 構造体の内部メンバーを記述し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> ます。  
  
 [AsyncTaskMethodBuilder\<TResult> 構造体](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md)  
 構造体の内部メンバーを記述し <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> ます。  
  
 [AsyncVoidMethodBuilder 構造体](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md)  
 構造体の内部メンバーを記述し <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> ます。  
  
## <a name="see-also"></a>参照  
 <xref:System.Threading.Tasks.Task?displayProperty=fullName>   
 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>   
 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)   
 [並列プログラミング](https://msdn.microsoft.com/library/4d83c690-ad2d-489e-a2e0-b85b898a672d)
