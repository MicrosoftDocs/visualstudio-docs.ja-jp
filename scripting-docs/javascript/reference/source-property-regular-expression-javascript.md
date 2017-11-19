---
title: "source プロパティ (Regular Expression) (JavaScript) |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: source
dev_langs:
- JavaScript
- TypeScript
- DHTML
helpviewer_keywords: Source property
ms.assetid: d58ac57e-fcde-49d1-bbba-e8c4218448c4
caps.latest.revision: "9"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 05bf118aec0f31de11a3df6f4b875fad3092e53d
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
---
# <a name="source-property-regular-expression-javascript"></a>source プロパティ (Regular Expression) (JavaScript)
正規表現パターンのテキストを返します。 読み取り専用です。 `rgExp`引数は、**正規表現**オブジェクト。 変数の名前またはリテラルを指定できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
rgExp.source  
```  
  
## <a name="example"></a>例  
 次の例では、使用、**ソース**プロパティ。  
  
```JavaScript  
function SourceDemo(re, s){  
   var s1;  
   // Test string for existence of regular expression.  
   if (re.test(s))  
      s1 = " contains ";  
   else  
      s1 = " does not contain ";  
   // Get the text of the regular expression itself.  
   return(s + s1 + re.source);  
}  
```  
  
## <a name="requirements"></a>要件  
 [!INCLUDE[jsv3](../../javascript/reference/includes/jsv3-md.md)]  
  
 **適用されます**: [Regular Expression オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)  
  
## <a name="see-also"></a>関連項目  
 [Regular Expression オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)   
 [Regular Expression オブジェクト](../../javascript/reference/regular-expression-object-javascript.md)   
 [正規表現の構文 (JavaScript)](http://msdn.microsoft.com/en-us/ab0766e1-7037-45ed-aa23-706f58358c0e)