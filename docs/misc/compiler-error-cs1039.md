---
title: "コンパイラ エラー CS1039 | Microsoft Docs"
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
  - "CS1039"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1039"
ms.assetid: 266e9f7f-fe17-445a-aefd-6b7795167d68
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1039
未終了の文字列です  
  
 コンパイラは正しくない形式の[文字列](/dotnet/csharp/language-reference/keywords/string)リテラルを検出しました。  
  
## 使用例  
 次の例では CS1039 が生成されます。 エラーを解決するには、終了の引用符を追加します。  
  
```  
// CS1039.cs public class MyClass { public static void Main() { string b = @"hello, world;   // CS1039 } }  
```