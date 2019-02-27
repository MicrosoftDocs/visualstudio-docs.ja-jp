---
title: 予期しない量指定子 (JavaScript) |Microsoft Docs
ms.date: 01/18/2017
ms.prod: visual-studio-windows
ms.technology: vs-javascript
ms.topic: reference
f1_keywords:
- VS.WebClient.Help.SCRIPT5018
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: ba6d34f9-2d6f-486c-a929-6cd9818be322
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f18195f344adca16fce7403d225c42826a2af544
ms.sourcegitcommit: 23feea519c47e77b5685fec86c4bbd00d22054e3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2019
ms.locfileid: "56843404"
---
# <a name="unexpected-quantifier-javascript"></a>予期しない量指定子です (JavaScript)
検索、正規表現パターンを作成すると、無効な繰り返しのパターン要素が作成されます。 たとえば、パターン  
  
```js
/^+/  
```  
  
 できませんので、要素 ^ (入力の先頭) は、繰り返し要素を含めることはできません。 次の表では、繰り返しの要因を持つことができない要素を示します。  
  
|要素|説明|  
|-------------|-----------------|  
|^|入力の先頭|  
|$|入力の終了|  
|\b|ワード境界|  
|\B|ワード境界以外|  
|*|0 個以上の繰り返し|  
|+|1 つ以上の繰り返し|  
|?|0 個または 1 回の繰り返し|  
|{n}|n 回の繰り返し|  
|{n}|n またはそれ以上の繰り返し|  
|{n,m}|N m 繰り返しからから|  
  
### <a name="to-correct-this-error"></a>このエラーを解決するには  
  
-   検索パターンに要素には、法的な繰り返し要素のみが含まれています。 確認してください。  
  
## <a name="see-also"></a>関連項目  
 [Regular Expression オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)   
 [正規表現構文 (JavaScript)](https://msdn.microsoft.com/library/1400241x)