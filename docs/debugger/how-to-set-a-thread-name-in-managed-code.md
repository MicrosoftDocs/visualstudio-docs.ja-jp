---
title: 'How to: Set a Thread Name in Managed Code | Microsoft Docs'
ms.custom: 
ms.date: 04/27/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Thread.Name property
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c0c4d74a-0314-4b71-81c9-b0b019347ab8
caps.latest.revision: 28
author: mikejo5000
ms.author: mikejo
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
ms.openlocfilehash: d3398729e3b32842dc47cff2d191a18085d29626
ms.contentlocale: ja-jp
ms.lasthandoff: 08/23/2017

---
# <a name="how-to-set-a-thread-name-in-managed-code"></a>How to: Set a Thread Name in Managed Code
Thread naming is possible in any edition of Visual Studio. Thread naming is useful for keeping track of threads in the **Threads** window.
  
 To set a thread name in managed code, use the <xref:System.Threading.Thread.Name%2A> property.  
  
## <a name="example"></a>Example  

```cs
public class Needle
{
    // This method will be called when the thread is started.  
    public void Baz()
    {
        Console.WriteLine("Needle Baz is running on another thread");
    }
}

public void Main()
{
    Console.WriteLine("Thread Simple Sample");
    Needle oNeedle = new Needle();
    // Create a Thread object.   
    System.Threading.Thread oThread = new System.Threading.Thread(oNeedle.Baz);
    // Set the Thread name to "MyThread".  
    oThread.Name = "MyThread";
    // Starting the thread invokes the ThreadStart delegate  
    oThread.Start();
}
```

```VB 
Public Class Needle  
    ' This method will be called when the thread is started.  
    Sub Baz()  
        Console.WriteLine("Needle Baz is running on another thread")  
    End Sub  
End Class  
  
Sub Main()  
    Console.WriteLine("Thread Simple Sample")  
    Dim oNeedle As New Needle()  
   ' Create a Thread object.   
    Dim oThread As New System.Threading.Thread(AddressOf oNeedle.Baz)  
    ' Set the Thread name to "MyThread".  
    oThread.Name = "MyThread"  
    ' Starting the thread invokes the ThreadStart delegate  
    oThread.Start()  
End Sub  
```  
  
## <a name="see-also"></a>See Also  
 [Debug Multithreaded Applications](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [How to: Set a Thread Name in Native Code](../debugger/how-to-set-a-thread-name-in-native-code.md)
