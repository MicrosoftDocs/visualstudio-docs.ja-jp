---
title: "コンパイラ エラー CS0186 | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0186"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0186"
ms.assetid: b8afca3e-0fb9-44c5-b4bb-abe3ef134e85
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0186
null はこのコンテキストでは使用できません。  
  
 次の例では CS0186 が生成されます。  
  
```  
// CS0186.cs using System; using System.Collections; class MyClass { static void Main() { // Each of the following lines generates CS0186: foreach (int i in null) {}   // CS0186 foreach (int i in (IEnumerable) null) { };   // CS0186 } }  
```