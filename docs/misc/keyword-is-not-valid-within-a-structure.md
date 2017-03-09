---
title: "&#39;&lt;keyword&gt;&#39; は、構造体内では有効ではありません | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30044"
  - "vbc30044"
helpviewer_keywords: 
  - "BC30044"
ms.assetid: 252510cf-e084-47e4-9592-4aa8f94fabe4
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;&lt;keyword&gt;&#39; は、構造体内では有効ではありません
構造体は、参照型ではなく、値型です。 構造体は、クラスから作成されたインスタンスではないため、`Me`、`MyClass`、および `MyBase` キーワードは構造体で意味がありません。  
  
 **エラー ID:** BC30044  
  
### このエラーを解決するには  
  
-   構造体をクラスに変更するか、またはプロシージャからキーワードを削除します。  
  
## 参照  
 [Me](http://msdn.microsoft.com/ja-jp/a65973c7-cf06-4547-9b25-9fba885525c2)   
 [MyClass \- 削除](http://msdn.microsoft.com/ja-jp/5db36f9b-f796-4b6a-ba34-cac1fde6eb62)   
 [MyBase \- 削除](http://msdn.microsoft.com/ja-jp/52491d06-6451-4f6f-9aa6-8fab59bbc2b9)   
 [Inheritance Basics](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)