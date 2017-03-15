---
title: "コンパイラの警告 (レベル 1) CS1723 | Microsoft Docs"
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
  - "CS1723"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1723"
ms.assetid: d359be86-7daf-4b59-99a3-10b072336bca
caps.latest.revision: 5
caps.handback.revision: 5
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラの警告 (レベル 1) CS1723
'param' の XML コメントに型パラメーターを参照する cref 属性 'attribute' があります。  
  
 このエラーは、型パラメーターを参照する XML コメントによって生成されます。  
  
## 使用例  
 次の例では、CS1723 エラーが生成されます。  
  
```  
// CS1723.cs // compile with: /t:library /doc:filename.XML ///<summary>A generic list class.</summary> ///<see cref="T" />   // CS1723 // To resolve comment the previous line. public class List<T> { }  
```