---
title: "リソース コンパイラ エラー RC2149 | Microsoft Docs"
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
  - "RC2149"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "RC2149"
ms.assetid: f0057230-5594-4696-8895-0adab5ba7f64
caps.latest.revision: 6
caps.handback.revision: 6
author: "corob-msft"
ms.author: "corob"
manager: "douge"
---
# リソース コンパイラ エラー RC2149
文字列テーブルに数値定数がありません  
  
 `#define` ステートメントで定義される数値定数は、**STRINGTABLE** ステートメントの **BEGIN** キーワードの直後に置く必要があります。