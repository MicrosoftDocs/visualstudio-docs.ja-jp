---
title: "コンパイラ エラー CS1575 | Microsoft Docs"
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
  - "CS1575"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1575"
ms.assetid: 76a9c57c-8f79-482e-9ae8-c70e8f199dd7
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1575
stackalloc の式は型の後に \[\] が必要です  
  
 [stackalloc](/dotnet/csharp/language-reference/keywords/stackalloc) を使用して要求する割り当てのサイズは、角かっこで囲んで指定する必要があります。  
  
 次の例では CS1575 が生成されます。  
  
```  
// CS1575.cs // compile with: /unsafe public class MyClass { unsafe public static void Main() { int *p = stackalloc int (30);   // CS1575 // try the following line instead // int *p = stackalloc int [30]; } }  
```