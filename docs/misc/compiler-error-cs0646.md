---
title: "コンパイラ エラー CS0646 | Microsoft Docs"
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
  - "CS0646"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0646"
ms.assetid: 48ea306f-b4a0-4988-8d2b-ca9d38e9bdad
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0646
インデクサーを含む型に対して DefaultMember 属性を指定できません。  
  
 クラスまたはその他の型で **System.Reflection.DefaultMemberAttribute** を指定する場合は、インデクサーを含めることはできません。 詳細については、「[プロパティ](/dotnet/csharp/programming-guide/classes-and-structs/properties)」を参照してください。  
  
 次の例では CS0646 が生成されます。  
  
```  
// CS0646.cs // compile with: /target:library [System.Reflection.DefaultMemberAttribute("x")]   // CS0646 class MyClass { public int this[int index]   // an indexer { get { return 0; } } public int x = 0; } // OK [System.Reflection.DefaultMemberAttribute("x")] class MyClass2 { public int prop { get { return 0; } } public int x = 0; } class MyClass3 { public int this[int index]   // an indexer { get { return 0; } } public int x = 0; }  
```