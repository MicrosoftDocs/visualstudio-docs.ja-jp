---
title: "コンパイラ エラー CS1510 | Microsoft Docs"
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
  - "CS1510"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1510"
ms.assetid: 3f5a69f1-7672-4194-a4ee-5753370fc736
caps.latest.revision: 10
caps.handback.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1510
ref または out 引数は、割り当て可能な変数でなければなりません。  
  
 メソッド呼び出しで [ref](/dotnet/csharp/language-reference/keywords/ref) パラメーターとして渡すことができるのは、変数のみです。`ref` 値はポインターを渡すことに似ています。  
  
## 使用例  
 次の例では CS1510 が生成されます。  
  
```  
// CS1510.cs public class C { public static int j = 0; public static void M(ref int j) { j++; } public static void Main () { M (ref 2);   // CS1510, can't pass a number as a ref parameter // try the following to resolve the error // M (ref j); } }  
```