---
title: 無効な置換関数の引数 |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5035
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 4727186f-facd-4aa6-9447-bbefbae83f07
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 46e01a4e6bb989fad2da6f979c79b7aba13df63a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007315"
---
# <a name="invalid-replacer-argument"></a>置換関数の引数が無効です。
呼び出しが試行された`JSON.stringify`引数が無効です。 `replacer`関数または配列を引数として使用することがあります。  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 変更、`replacer`関数または配列への引数。  
  
## <a name="example"></a>例  
 この例では、コードが実行時エラー`memberfilter`関数または配列ではなくオブジェクトです。  
  
```JavaScript  
var contact = new Object();  
contact.firstname = "Jesper";  
contact.surname = "Aaberg";  
contact.phone = ["555-0100", "555-0120"];  
  
var memberfilter = new Object();  
  
// This line will cause a runtime error.  
var jsontext = JSON.stringify(contact, memberfilter, "\t");  
```  
  
## <a name="see-also"></a>関連項目  
 [JSON オブジェクト](../../javascript/reference/json-object-javascript.md)   
 [JSON.parse 関数](../../javascript/reference/json-parse-function-javascript.md)   
 [JavaScript ランタイム エラー](../../javascript/reference/javascript-run-time-errors.md)