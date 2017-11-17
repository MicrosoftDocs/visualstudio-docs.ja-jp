---
title: "normalize メソッド (String) (JavaScript) |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-client-threshold
ms.reviewer: 
ms.suite: 
ms.technology: devlang-javascript
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: d50077c1-b5fa-4e7a-9c9d-dc66cfc423ac
caps.latest.revision: "4"
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: aece38339ea1ce8924f404938b2d35d07504d539
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2017
---
# <a name="normalize-method-string-javascript"></a>normalize メソッド (String) (JavaScript)
指定した文字列の Unicode 正規化形式を返します。  
  
## <a name="syntax"></a>構文  
  
```  
stringObj.normalize([form]);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `stringObj`  
 必須です。 テスト対象の String オブジェクト。  
  
 `form`  
 省略可能です。 Unicode 正規化形式の値。  
  
## <a name="return-value"></a>戻り値  
 指定した文字列の Unicode 正規化形式。  
  
## <a name="exceptions"></a>例外  
 `form` がサポートされていない値の場合は、`RangeError` がスローされます。  
  
## <a name="remarks"></a>コメント  
 `stringObj` が文字列ではない場合、まず文字列に変換してから、メソッドは文字列の Unicode 正規化形式を返そうとします。  
  
 `form`指定した値に対応する"NFC"、"NFD"、"NFKC"、"NFKD"、または Unicode 正規化形式の値指定する必要があります[Unicode Standard Annex #15](http://www.unicode.org/reports/tr15/)です。 `form` の既定値は "NFC" です。  
  
## <a name="example"></a>例  
 次のコード例は、`normalize` メソッドの使用法を示しています。  
  
```JavaScript  
// ANGSTORM SIGN and LATIN CAPITAL A WITH RING ABOVE is canonically equivalent  
"\u212b".normalize("NFC") === "\u00c5";  
  
// Decomposed, ANGSTOM SIGN is LATIN CAPITAL A followed by COMBINING RING ABOVE  
"\u212b".normalize("NFD") === "\u0041\u030a"  
  
// Normalization Form C will combine the result back into the precombined character  
"\u0041\u030a".normalize("NFC") === "\u00c5"  
  
// LATIN SMALL LIGATURE FI is compatibility equivalent with LATIN SMALL LETTER F followed by  
// LATIN SMALL LETTER I.  
"\ufb01".normalize("NFKD") === "fi";  
  
// Same mapping in NFKC  
"\ufb01".normalize("NFKC") === "fi";  
  
// NFKC will not recombine compatibility characters.  
"fi".normalize("NFKC") === "fi";  
```  
  
## <a name="requirements"></a>要件  
 [!INCLUDE[jsv12](../../javascript/reference/includes/jsv12-md.md)]