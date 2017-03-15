---
title: "コンパイラ エラー CS0272 | Microsoft Docs"
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
  - "CS0272"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0272"
ms.assetid: 16a9aab6-922a-45a3-a0ef-f32e99f3950f
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0272
set アクセサーにアクセスできないため、プロパティまたはインデクサー 'property\/indexer' はこのコンテキストでは使用できません  
  
 このエラーは、`set` アクセサーがプログラム コードにアクセスできないと発生します。 このエラーを解決するには、アクセサーのアクセシビリティを増やすか、呼び出し元の場所を変更します。 詳細については、「[アクセサーのアクセシビリティの制限](/dotnet/csharp/programming-guide/classes-and-structs/restricting-accessor-accessibility)」を参照してください。  
  
## 使用例  
 次の例では、CS0272 が生成されます。  
  
```  
// CS0272.cs public class MyClass { public int Property { get { return 0; } private set { } } } public class Test { static void Main() { MyClass c = new MyClass(); c.Property = 10;      // CS0272 // To resolve, remove the previous line // or use an appropriate modifier on the set accessor. } }  
```