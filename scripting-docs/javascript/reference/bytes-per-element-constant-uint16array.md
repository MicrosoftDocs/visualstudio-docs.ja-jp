---
title: BYTES_PER_ELEMENT 定数 (Uint16Array) |Microsoft ドキュメント
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-javascript
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4e5e8a70-f8b9-4e3c-b9f3-0d1249963c28
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4a437564d98120a74e43df81670ade92dadba792
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
ms.locfileid: "24634122"
---
# <a name="bytesperelement-constant-uint16array"></a>BYTES_PER_ELEMENT 定数 (Uint16Array)
配列の各要素のサイズ (バイト単位)。  
  
## <a name="syntax"></a>構文  
  
```JavaScript  
var arraySize = uint16Array.BYTES_PER_ELEMENT;  
```  
  
## <a name="example"></a>例  
 次の例は、配列の要素のサイズの取得方法を示します。  
  
```JavaScript  
var req = new XMLHttpRequest();  
    req.open('GET', "http://www.example.com");  
    req.responseType = "arraybuffer";  
    req.send();  
  
    req.onreadystatechange = function () {  
        if (req.readyState === 4) {  
            var buffer = req.response;  
            var dataView = new DataView(buffer);  
            var intArr = new Uint16Array(buffer.byteLength / 2);  
            alert(intArr.BYTES_PER_ELEMENT);  
        }  
    }  
  
```  
  
## <a name="requirements"></a>要件  
 [!INCLUDE[jsv10](../../javascript/reference/includes/jsv10-md.md)]