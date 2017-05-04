---
title: "VBArray が必要です。 | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "windows-client-threshold"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "javascript"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VS.WebClient.Help.SCRIPT5013"
dev_langs: 
  - "JavaScript"
  - "TypeScript"
  - "DHTML"
ms.assetid: f2998d7d-13a4-4bbe-b872-3ff3316551e4
caps.latest.revision: 6
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 6
---
# VBArray が必要です。
Visual Basic safeArray が必要な場合に、それ以外のオブジェクトを指定しました。  
  
```  
new VBArray(safeArray);  
```  
  
 VBArray は読み取り専用で、直接作成することはできません。  safeArray 引数は VBArray 値で、`VBArray` コンストラクターに渡される前に取得しておく必要があります。  この値は、既存の ActiveX またはその他のオブジェクトから取得できます。  
  
### このエラーを解決するには  
  
-   **VBArray** コンストラクターには、**VBArray** オブジェクトのみを渡します。  
  
## 参照  
 [VBArray オブジェクト](../../javascript/reference/vbarray-object-javascript.md)   
 [配列の使用](../../javascript/advanced/using-arrays-javascript.md)