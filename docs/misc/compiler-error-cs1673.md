---
title: "コンパイラ エラー CS1673 | Microsoft Docs"
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
  - "CS1673"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1673"
ms.assetid: 5c7dd58b-dcbc-45c9-be36-7d15fafaa067
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1673
構造体内の匿名メソッド、ラムダ式、およびクエリ式は、'this' のインスタンス メンバーにアクセスできません。 'this' を匿名メソッド、ラムダ式、またはクエリ式の外部のローカル変数にコピーし、このローカルを代わりに使用します。  
  
 次の例では CS1673 が生成されます。  
  
```  
// CS1673.cs delegate int MyDelegate(); public struct S { int member; public int F(int i) { member = i; // Try assigning to a local variable // S s = this; MyDelegate d = delegate() { i = this.member;  // CS1673 // And use the local variable instead of "this" // i =  s.member; return i; }; return d(); } } class CMain { public static void Main() { } }  
```