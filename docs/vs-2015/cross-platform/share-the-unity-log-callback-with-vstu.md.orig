---
title: Unity のログ コールバックを VSTU と共有する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 5d71f906-6e50-4399-b59b-d38c6dfef7ee
caps.latest.revision: 5
author: conceptdev
ms.author: crdun
manager: jillfra
ms.openlocfilehash: 5e4fcfdc35e9329429421fd03a941e611e6b5b8f
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54789170"
---
# <a name="share-the-unity-log-callback-with-vstu"></a>Unity のログ コールバックを VSTU と共有する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Visual Studio Tools for Unity では、Unity コンソールを Visual Studio にストリーミングできるよう、Unity にログ コールバックを登録します。 エディターのスクリプトもログ コールバックを Unity に登録すると、そのコールバックが VSTU コールバックから影響を受けることがあります。 この可能性を回避するには、`VisualStudioIntegration.LogCallback` イベントを使用して VSTU と連携します。  
  
## <a name="demonstrates"></a>使用例  
 Visual Studio Tools for Unity によって作成されるログ コールバックを共有する方法を示します。  
  
## <a name="example"></a>例  
  
```csharp  
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
  
## <a name="see-also"></a>関連項目  
 [例: プロジェクト ファイルの生成](../cross-platform/customize-project-files-created-by-vstu.md)
