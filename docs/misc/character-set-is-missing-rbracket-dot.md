---
title: "Character set is missing &#39;]&#39;. | Microsoft Docs"
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
  - "vs.message.VS_E_RE_SETMISSINGCLOSE"
  - "vs.message.0x800A00C0"
ms.assetid: 97d2436c-498d-4eb0-a08c-8efcc7797fc0
caps.latest.revision: 6
caps.handback.revision: 6
author: "mikeblome"
ms.author: "mblome"
manager: "douge"
---
# Character set is missing &#39;]&#39;.
このエラーが発生するのは一般的に、検索文字列または置換文字列で正規表現の右かっこ \(`]`\) が不足している場合です。  
  
### このエラーを解決するには  
  
1.  リテラル文字 `]` を検索する場合は、「`\]`」を使用します。  
  
2.  文字セットを対応させる場合は、不足しているかっこ「`]`」を入力します。  
  
## 参照  
 [Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)   
 [NIB: Find and Replace, Quick Find](http://msdn.microsoft.com/ja-jp/dad03582-4931-4893-83ba-84b37f5b1600)   
 [\[フォルダーを指定して検索\]](../ide/find-in-files.md)