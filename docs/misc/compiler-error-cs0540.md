---
title: "コンパイラ エラー CS0540 | Microsoft Docs"
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
  - "CS0540"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0540"
ms.assetid: 2da2cd4a-0ff1-45ea-bb72-ea078bc95dea
caps.latest.revision: 12
caps.handback.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0540
'interface member' : 含む型は、インターフェイス 'interface' を実装しません  
  
 インターフェイス メンバーを、[インターフェイス](/dotnet/csharp/language-reference/keywords/interface)から派生していない[クラス](/dotnet/csharp/language-reference/keywords/class)に実装しようとしました。 インターフェイス メンバーの実装を削除するか、インターフェイスをクラスの基底クラス リストに追加する必要があります。  
  
## 使用例  
 次の例では CS0540 が生成されます。  
  
```  
// CS0540.cs interface I { void m(); } public class Clx { void I.m() {}   // CS0540 } // OK public class Cly : I { void I.m() {} public static void Main() {} }  
```  
  
## 使用例  
 次の例では CS0540 が生成されます。  
  
```  
// CS0540_b.cs using System; class C { void IDisposable.Dispose() {}   // CS0540 } class D : IDisposable { void IDisposable.Dispose() {} public void Dispose() {} static void Main() { using (D d = new D()) {} } }  
```