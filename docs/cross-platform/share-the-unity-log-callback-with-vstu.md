---
title: Share the Unity Log Callback with VSTU | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5d71f906-6e50-4399-b59b-d38c6dfef7ee
caps.latest.revision: 2
author: ghogen
ms.author: ghogen
manager: ghogen
translation.priority.ht:
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
ms.translationtype: HT
ms.sourcegitcommit: ff8ecec19f8cab04ac2190f9a4a995766f1750bf
ms.openlocfilehash: e598b0f08bd0703bdec3b1abb380fb127df550ae
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="share-the-unity-log-callback-with-vstu"></a>Share the Unity Log Callback with VSTU
Visual Studio Tools for Unity registers a log callback with Unity to be able to stream its console to Visual Studio. If your editor scripts also register a log callback with Unity, the VSTU callback might interfere with your callback. To prevent this possibility, use the `VisualStudioIntegration.LogCallback` event to cooperate with VSTU.  
  
## <a name="demonstrates"></a>Demonstrates  
 How to share the Unity Log Callback created by Visual Studio Tools for Unity.  
  
## <a name="example"></a>Example  
  
```cs  
using System;  
  
using UnityEngine;  
using UnityEditor;  
  
using SyntaxTree.VisualStudio.Unity.Bridge;  
  
[InitializeOnLoad]  
public class LogCallbackHook  
{  
    static LogCallbackHook()  
    {  
        VisualStudioIntegration.LogCallback += (string condition, string trace, LogType type) =>  
        {  
            // place code that implements your log callback here  
        };  
    }  
}  
```  
  
## <a name="see-also"></a>See Also  
 [Example: Project File Generation](../cross-platform/customize-project-files-created-by-vstu.md)
