---
title: "コンパイラ エラー CS1663 | Microsoft Docs"
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
  - "CS1663"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1663"
ms.assetid: 013f36ac-8925-4cee-9008-54fa7ad1324b
caps.latest.revision: 10
caps.handback.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1663
固定サイズ バッファーの型は次のうちの 1 つでなければなりません: bool、byte、short、int、long、char、sbyte、ushort、uint、ulong、float または double  
  
 固定サイズのバッファーは、リストされている以外の型にすることはできません。 このエラーを回避するには、別の型を使用するか、または固定配列を使用しないようにします。  
  
## 使用例  
 次の例では CS1663 が生成されます。  
  
```  
// CS1663.cs // compile with: /unsafe /target:library unsafe struct C { fixed string ab[10];   // CS1663 }  
```