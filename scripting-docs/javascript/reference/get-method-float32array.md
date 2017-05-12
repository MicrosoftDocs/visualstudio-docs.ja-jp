---
title: "get メソッド (Float32Array) | Microsoft Docs"
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
ms.assetid: f859481c-0bb8-43d3-9d54-38d303e44397
caps.latest.revision: 9
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 9
---
# get メソッド (Float32Array)
省略可能。  指定したインデックス位置にある要素を取得します。  
  
## 構文  
  
```javascript  
var value = float32Array.get(index);  
```  
  
## パラメーター  
 `value`  
 このメソッドで返される値。  
  
 `index`  
 配列内の要素を取得する位置のインデックス。  
  
## 使用例  
 次の例は、配列の先頭の要素の取得方法を示します。  
  
```javascript  
var req = new XMLHttpRequest();  
    req.open('GET', "http://www.example.com");  
    req.responseType = "arraybuffer";  
    req.send();  
  
    req.onreadystatechange = function () {  
        if (req.readyState === 4) {  
            var buffer = req.response;  
            var dataView = new DataView(buffer);  
            var floatArr = new Float32Array(buffer.byteLength / 4);  
            var element = floatArr.getFloat32(0);  
        }  
    }  
  
```  
  
## 必要条件  
 [!INCLUDE[jsv10](../../javascript/reference/includes/jsv10-md.md)]