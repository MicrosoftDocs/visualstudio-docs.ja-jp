---
title: "valueOf メソッド (Array) | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "windows-client-threshold"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-javascript"
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
dev_langs: 
  - "JavaScript"
  - "TypeScript"
  - "DHTML"
ms.assetid: b694fe65-1297-4580-8af2-406932c06454
caps.latest.revision: 2
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 2
---
# valueOf メソッド (Array)
指定されたオブジェクトのプリミティブ値を返します。  
  
## 構文  
  
```  
  
array.valueOf()  
```  
  
#### パラメーター  
 このメソッドにパラメーターはありません。  
  
## 戻り値  
 配列のインスタンスを返します。  
  
## 解説  
 インスタンス化された配列オブジェクトがこのメソッドの戻り値と同じ例を次に示します。  
  
```javascript  
var arr = [1, 2, 3, 4];  
var s = arr.valueOf();  
  
if (arr === s)  
document.write("same");  
else  
document.write("different");  
  
// Output:  
// same  
  
```  
  
## 必要条件  
 [!INCLUDE[jsv2](../../javascript/reference/includes/jsv2-md.md)]