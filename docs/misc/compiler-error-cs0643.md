---
title: "コンパイラ エラー CS0643 | Microsoft Docs"
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
  - "CS0643"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0643"
ms.assetid: beae30ff-15c2-413f-8f5c-504cdba2e57a
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0643
'arg' 属性引数の名前が重複しています  
  
 パラメーター `arg` がユーザー定義の属性で 2 回指定されました。 詳細については、「[属性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)」を参照してください。  
  
## 使用例  
 次の例では CS0643 が生成されます。  
  
```  
// CS0643.cs using System; using System.Runtime.InteropServices; [AttributeUsage(AttributeTargets.Class)] public class MyAttribute : Attribute { public MyAttribute() { } public int x; } [MyAttribute(x = 5, x = 6)]   // CS0643, error setting x twice // try the following line instead // [MyAttribute(x = 5)] class MyClass { } public class MainClass { public static void Main () { } }  
```