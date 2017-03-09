---
title: "コンパイラ エラー CS1007 | Microsoft Docs"
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
  - "CS1007"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1007"
ms.assetid: b56ee2c6-8e79-4b9b-8c59-194bdb22bc3e
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1007
プロパティ アクセサーは既に定義されています。  
  
 [プロパティ](/dotnet/csharp/programming-guide/classes-and-structs/using-properties)を宣言する場合、そのアクセサー メソッドも宣言する必要があります。 ただし、プロパティは複数の `get` アクセサー メソッドまたは複数の `set` アクセサー メソッドを持つことはできません。  
  
## 使用例  
 次の例では CS1007 が生成されます。  
  
```  
// CS1007.cs public class clx { public int MyProperty { get { return 0; } get   // CS1007, this is the second get method { return 0; } } public static void Main() {} }  
```