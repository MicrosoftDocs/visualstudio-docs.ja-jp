---
title: "コンパイラ エラー CS1020 | Microsoft Docs"
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
  - "CS1020"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1020"
ms.assetid: e8860769-a847-4248-a37b-77a59863467c
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1020
オーバーロード可能な 2 項演算子が必要です。  
  
 [演算子のオーバーロード](/dotnet/csharp/programming-guide/statements-expressions-operators/overloadable-operators)の定義を試みましたが、演算子が 2 つのパラメーターを受け取る 2 項演算子ではありませんでした。  
  
 次の例では CS1020 が生成されます。  
  
```  
// CS1020.cs public class iii { public static int operator ++(iii aa, int bb)   // CS1020, change ++ to + { return 0; } public static void Main() { } }  
```