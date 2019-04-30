---
title: アクティブ スクリプト Profiler インターフェイス |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ab8a1f0d-393c-4d6a-94c1-d5b8aa76788c
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eeadf0de5563a4882c067960559414167e729173
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422240"
---
# <a name="active-script-profiler-interfaces"></a>アクティブ スクリプト プロファイラーのインターフェイス
アクティブ スクリプトのプロファイラーのインターフェイスによって、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] エンジンからプロファイリング イベントを受け取ることができます。  
  
 activprof.h ヘッダー ファイルは、このセクションで示されるインターフェイスを提供します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次のインターフェイスはプロファイリングを有効にします。  
  
- [IActiveScriptProfilerControl インターフェイス](../../winscript/reference/iactivescriptprofilercontrol-interface.md)  
  
- [IActiveScriptProfilerControl2 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)  
  
- [IActiveScriptProfilerControl3 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol3-interface.md)  
  
- [IActiveScriptProfilerControl5 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol5-interface.md)  
  
- [IActiveScriptProfilerCallback インターフェイス](../../winscript/reference/iactivescriptprofilercallback-interface.md)  
  
- [IActiveScriptProfilerCallback2 インターフェイス](../../winscript/reference/iactivescriptprofilercallback2-interface.md)  
  
- [IActiveScriptProfilerCallback3 インターフェイス](../../winscript/reference/iactivescriptprofilercallback3-interface.md)  
  
- [IActiveScriptProfilerHeapEnum インターフェイス](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)  
  
  次のセクションで、プロファイリングに使用される列挙型の一覧を示します。  
  
- [アクティブ スクリプト プロファイラーの定数、列挙型、および構造体](../../winscript/reference/active-script-profiler-constants-enumerations-and-structures.md)  
  
> [!NOTE]
> アクティブ スクリプトのプロファイラーのインターフェイスは、最初に Internet Explorer 8 と共にリリースされました。 `IActiveScriptProfilerControl2` および `IActiveScriptProfilerCallback2` インターフェイスは、最初に Internet Explorer 9 と共にリリースされました。 [IActiveScriptProfilerControl3 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol3-interface.md)、 [IActiveScriptProfilerCallback3 インターフェイス](../../winscript/reference/iactivescriptprofilercallback3-interface.md)、および[IActiveScriptProfilerHeapEnum インターフェイス](../../winscript/reference/iactivescriptprofilerheapenum-interface.md)インターフェイスが最初に、Internet Explorer 10 と共にリリースされました。 [IActiveScriptProfilerControl5 インターフェイス](../../winscript/reference/iactivescriptprofilercontrol5-interface.md)Internet Explorer 11 で初めてリリースされました。  
>   
> Internet Explorer 8 と Internet Explorer 9 では、[!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] 言語だけが、これらのインターフェイスを使用してスクリプト プロファイリングをサポートします。  
  
## <a name="see-also"></a>関連項目  
 [Windows スクリプト インターフェイスのリファレンス](../../winscript/reference/windows-script-interfaces-reference.md)