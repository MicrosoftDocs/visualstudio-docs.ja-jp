---
title: "コンパイラ エラー CS0551 | Microsoft Docs"
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
  - "CS0551"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0551"
ms.assetid: fb456ecf-dff3-4e39-b9b3-de23d81dadea
caps.latest.revision: 8
caps.handback.revision: 8
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0551
明示的なインターフェイス実装 'implementation' のアクセサー 'accessor' がありません  
  
 インターフェイスのプロパティを明示的に実装するクラスは、インターフェイスが定義するすべてのアクセサーを実装する必要があります。  
  
 詳細については、「[プロパティの使用](/dotnet/csharp/programming-guide/classes-and-structs/using-properties)」を参照してください。  
  
## 使用例  
 次の例では CS0551 が生成されます。  
  
```  
// CS0551.cs // compile with: /target:library interface ii { int i { get; set; } } public class a : ii { int ii.i { set {} }   // CS0551 // OK int ii.i { set {} get { return 0; } } }  
```