---
title: "コンパイラ エラー CS2020 | Microsoft Docs"
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
  - "CS2020"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS2020"
ms.assetid: b2db7a05-5965-4a9b-86c3-0c4792b29a6c
caps.latest.revision: 7
caps.handback.revision: 7
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS2020
入力ファイルの最初のセットのみが、module 以外のターゲットをビルドすることができます。  
  
 複数出力のコンパイルでは、最初の出力ファイルを、[\/target:exe](../Topic/-target:exe%20\(C%23%20Compiler%20Options\).md)、[\/target:winexe](../Topic/-target:winexe%20\(C%23%20Compiler%20Options\).md)、または [\/target:library](../Topic/-target:library%20\(C%23%20Compiler%20Options\).md) を使用して構築する必要があります。 その後の出力ファイルは、[\/target:module](../Topic/-target:module%20\(C%23%20Compiler%20Options\).md) を使用して構築する必要があります。