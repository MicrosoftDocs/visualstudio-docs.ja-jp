---
redirect_url: /visualstudio/csharp-ide/refactoring/extract-interface
title: Extract Interface Refactoring (C#) | Microsoft Docs
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Interface
- Extract Interface refactoring operation [C#]
ms.assetid: 7d0aa225-3b33-4331-9652-5a67cac6f3d0
caps.latest.revision: 25
author: BillWagner
ms.author: wiwagn
manager: wpickett
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
ms.sourcegitcommit: 4a36302d80f4bc397128e3838c9abf858a0b5fe8
ms.openlocfilehash: 2976187778d144259b697b5253c78d4afe65b4ff
ms.contentlocale: ja-jp
ms.lasthandoff: 08/28/2017

---
# <a name="extract-interface-refactoring-c"></a>Extract Interface Refactoring (C#)
Extract Interface is a refactoring operation that provides an easy way to create a new interface with members that originate from an existing class, struct, or interface.  
  
 When several clients use the same subset of members from a class, struct, or interface, or when multiple classes, structs, or interfaces have a subset of members in common, it can be useful to embody the subset of members in an interface. For more information about using interfaces, see [Interfaces](/dotnet/csharp/programming-guide/interfaces/index).  
  
 Extract Interface generates an interface in a new file and positions the cursor at the beginning of the new file. You can specify which members to extract into the new interface, the name of the new interface, and the name of the generated file using the **Extract Interface** dialog box.  
  
### <a name="to-use-extract-interface"></a>To use Extract Interface  
  
1.  Create a console application named `ExtractInterface`, and then replace `Program` with the following code  
  
    ```csharp  
    // Invoke Extract Interface on ProtoA.  
    // Note:  the extracted interface will be created in a new file.  
    class ProtoA  
    {  
        public void MethodB(string s) { }  
    }  
    ```  
  
2.  With the cursor positioned in `MethodB`, and click **Extract Interface** on the **Refactor** menu.  
  
     The **Extract Interface** dialog box appears.  
  
     You can also type the keyboard shortcut CTRL+R, I to display the **Extract Interface** dialog box.  
  
     You can also right-click the mouse, point to **Refactor**, and then click **Extract Interface** to display the **Extract Interface** dialog box.  
  
3.  Click **Select All**.  
  
4.  Click **OK**.  
  
     You see the new file, IProtoA.cs, and the following code:  
  
    ```csharp  
    using System;  
    namespace TopThreeRefactorings  
    {  
        interface IProtoA  
        {  
            void MethodB(string s);  
        }  
    }  
    ```  
  
## <a name="remarks"></a>Remarks  
 This feature is only accessible when the cursor is positioned in the class, struct, or interface that contains the members that you would like to extract. When the cursor is in this position, invoke the Extract Interface refactoring operation.  
  
 When you invoke extract interface on a class or on a struct, the bases and interfaces list is modified to include the new interface name. When you invoke extract interface on an interface, the bases and interfaces list is not modified.  
  
## <a name="see-also"></a>See Also  
 [Refactoring (C#)](refactoring-csharp.md)
