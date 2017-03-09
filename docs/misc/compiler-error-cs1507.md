---
title: "コンパイラ エラー CS1507 | Microsoft Docs"
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
  - "CS1507"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS1507"
ms.assetid: e1be3aba-81dc-4f65-87a4-d3f90b82dc7d
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS1507
モジュールをビルド中にリソース ファイル 'file' にリンクできません  
  
 [\/target:module](../Topic/-target:module%20\(C%23%20Compiler%20Options\).md) と同じコンパイルで [\/linkresource](/dotnet/csharp/language-reference/compiler-options/linkresource-compiler-option) が使用されましたが、これは許可されていません。 たとえば、次のオプションでは CS1507 が生成されます。  
  
```  
csc /linkresource:rf.resource /target:module in.cs  
```  
  
 ただし、リソースの埋め込み \([\/resource](/dotnet/csharp/language-reference/compiler-options/resource-compiler-option)\) は許可されます。