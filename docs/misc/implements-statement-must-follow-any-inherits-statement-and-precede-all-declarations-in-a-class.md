---
title: "&#39;Implements&#39; ステートメントは、&#39;Inherits&#39; ステートメントの後およびクラス内のすべての宣言の前に記述しなければなりません | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc31053"
  - "vbc31053"
helpviewer_keywords: 
  - "BC31053"
ms.assetid: 8036a1a1-7e31-4c49-b74b-01601a548f3e
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;Implements&#39; ステートメントは、&#39;Inherits&#39; ステートメントの後およびクラス内のすべての宣言の前に記述しなければなりません
`Implements` ステートメントを無効な場所に記述しました。  
  
 **エラー ID:** BC31053  
  
### このエラーを解決するには  
  
-   `Implements` ステートメントを `Inherits` ステートメントの直後かつどの宣言よりも前に配置します。 例:  
  
    ```  
    Class Derived Inherits Base Implements One Sub SubOne() Implements One.Method1 ' Add code to implement the method. End Sub End Class  
    ```  
  
## 参照  
 [Interfaces](/dotnet/visual-basic/programming-guide/language-features/interfaces/index)   
 [Implements](/dotnet/visual-basic/language-reference/statements/implements-clause)