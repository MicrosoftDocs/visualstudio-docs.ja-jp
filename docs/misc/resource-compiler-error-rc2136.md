---
title: "リソース コンパイラ エラー RC2136 | Microsoft Docs"
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
  - "RC2136"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "RC2136"
ms.assetid: 4e9b2ff1-402c-4ec4-8610-fc8fd5f213c0
caps.latest.revision: 6
caps.handback.revision: 6
author: "corob-msft"
ms.author: "corob"
manager: "douge"
---
# リソース コンパイラ エラー RC2136
missing '\=' in EXSTYLE\=\<flags\>  
  
 **EXSTYLE** \(拡張スタイル フラグ\) ステートメントに等号 \(**\=**\) がありません。**EXSTYLE** を **DIALOG** ステートメントや **MENU** ステートメントに埋め込む場合は、次の書式にする必要があります。  
  
```  
EXSTYLE=FLAGS  
```