---
title: "コンパイラの警告 (レベル 3) CS0665 | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0665"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0665"
ms.assetid: bddff69b-e74e-45ce-8472-16ee53ae4609
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラの警告 (レベル 3) CS0665
条件式の割り当ては常に定数です。\=\= を使用するつもりで \= を使用しましたか?  
  
 条件式で、[\=\= operator](/dotnet/csharp/language-reference/operators/equality-comparison-operator) ではなく [\= operator](/dotnet/csharp/language-reference/operators/assignment-operator) が使用されています。  
  
 次の例では CS0665 が生成されます。  
  
```  
// CS0665.cs // compile with: /W:3 class Test { public static void Main() { bool i = false; if (i = true)   // CS0665 // try the following line instead // if (i == true) { } System.Console.WriteLine(i); } }  
```