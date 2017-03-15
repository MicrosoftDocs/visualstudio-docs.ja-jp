---
title: "コンパイラ エラー CS0575 | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0575"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0575"
ms.assetid: e8f20960-94a6-41d0-807c-d49ad198ccf6
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0575
クラスのみがデストラクターを含むことができます。  
  
 [構造体](/dotnet/csharp/language-reference/keywords/struct)にデストラクターを含めることはできません。  
  
 次の例では CS0575 が生成されます。  
  
```  
// CS0575.cs namespace x { public struct iii { ~iii()   // CS0575 { } public static void Main() { } } }  
```