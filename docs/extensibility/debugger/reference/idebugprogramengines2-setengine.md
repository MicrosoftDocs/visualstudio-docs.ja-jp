---
title: IDebugProgramEngines2::SetEngine | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- IDebugProgramEngines2::SetEngine
helpviewer_keywords:
- IDebugProgramEngines2::SetEngine
ms.assetid: c05857ee-89cf-455e-8f1e-300cce4a2eab
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: MT
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: 8164b95af3f67faec8aa76be34653ca9d679d4bc
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="idebugprogramengines2setengine"></a>IDebugProgramEngines2::SetEngine
Tells the program or program node which debug engine (DE) to use to debug this program.  
  
## <a name="syntax"></a>Syntax  
  
```cpp#  
HRESULT SetEngine(   
   REFGUID guidEngine  
);  
```  
  
```cs  
int SetEngine(   
   ref Guid guidEngine  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `guidEngine`  
 [in] The GUID of the DE.  
  
## <a name="return-value"></a>Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## <a name="see-also"></a>See Also  
 [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
