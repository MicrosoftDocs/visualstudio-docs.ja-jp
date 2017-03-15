---
title: "コンパイラ エラー CS0596 | Microsoft Docs"
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
  - "CS0596"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0596"
ms.assetid: 7cbf0db1-bb0b-4c50-b71e-16599a7e37d0
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0596
Guid 属性は Comimport 属性を使って指定する必要があります。  
  
 **ComImport** 属性を使用する場合には、**Guid** 属性が存在する必要があります。  
  
 次の例では CS0596 が生成されます。  
  
```  
// CS0596.cs using System.Runtime.InteropServices; namespace x { [ComImport]   // CS0596 // try the following line to resolve this CS0596 // [ComImport, Guid("00000000-0000-0000-0000-000000000001")] public class a { } public class b { public static void Main() { } } }  
```