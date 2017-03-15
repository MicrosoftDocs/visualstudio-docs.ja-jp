---
title: "コンパイラ エラー CS0601 | Microsoft Docs"
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
  - "CS0601"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0601"
ms.assetid: 20666d6f-e435-4f2d-8eca-084b7d6b57d8
caps.latest.revision: 6
caps.handback.revision: 6
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0601
static または extern に指定されているメソッドでは、DllImport 属性を指定する必要があります  
  
 `DllImport` 属性は、適切なアクセス キーワードが含まれていないメソッドで使用されていました。  
  
 次の例では CS0601 が生成されます。  
  
```  
// CS0601.cs using System.Runtime.InteropServices; using System.Text; public class C { [DllImport("KERNEL32.DLL")] extern int GetCurDirectory(int bufSize, StringBuilder buf);   // CS0601 // Try the following line instead: // static extern int GetCurDirectory(int bufSize, StringBuilder buf); } public class MainClass { public static void Main () { } }  
```