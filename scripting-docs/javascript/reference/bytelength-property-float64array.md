---
title: "byteLength プロパティ (Float64Array) | Microsoft Docs"
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
ms.assetid: 892498c1-dd6c-4037-89c2-cae29f5d09f2
caps.latest.revision: 8
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 8
---
# byteLength プロパティ (Float64Array)
読み取り専用です。  構築時に固定された、この配列の ArrayBuffer の先頭からの長さ \(バイト単位\)。  
  
## 構文  
  
```javascript  
var arrayByteLength = float64Array.byteLength;  
```  
  
## 使用例  
 配列の長さ \(バイト\) を取得する方法の例を次に示します。  
  
```javascript  
var req = new XMLHttpRequest();  
    req.open('GET', "http://www.example.com");  
    req.responseType = "arraybuffer";  
    req.send();  
  
    req.onreadystatechange = function () {  
        if (req.readyState === 4) {  
            var buffer = req.response;  
            var dataView = new DataView(buffer);  
            var floatArr = new Float64Array(buffer.byteLength / 8);  
            alert(floatArr.byteLength);  
        }  
    }  
  
```  
  
## 必要条件  
 [!INCLUDE[jsv10](../../javascript/reference/includes/jsv10-md.md)]