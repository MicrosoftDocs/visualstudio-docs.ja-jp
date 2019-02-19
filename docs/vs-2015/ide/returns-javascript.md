---
title: '&lt;返します&gt;(JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- returns JavaScript XML tag
- <returns> JavaScript XML tag
ms.assetid: 10d97829-c0ae-40a5-b04c-d8b538cdefbc
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 81a9a42a104adb2a9d9a9aba483e2588d7332868
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54801777"
---
# <a name="ltreturnsgt-javascript"></a>&lt;返します&gt;(JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

関数またはメソッドの呼び出しの結果のドキュメント情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
<returns type="ValueType" integer="true|false"  
    domElement="true|false" mayBeNull="true|false"  
    elementType="ArrayElementType" elementInteger="true|false"  
    elementDomElement="true|false" elementMayBeNull="true|false"  
    locid="descriptionID" value="code">description  
</returns>  
```  
  
#### <a name="parameters"></a>パラメーター  
 `type`  
 任意。 戻り値のデータ型。 型は以下のいずれかです。  
  
- `Number` や `Object` など、ECMAScript 5 仕様に含まれる ECMAScript 言語の型。  
  
- `HTMLElement`、`Window`、`Document` などの DOM オブジェクト。  
  
- JavaScript のコンストラクター関数。  
  
  `integer`  
  任意。 `type` が `Number` である場合に、戻り値が整数かどうかを指定します。 戻り値が整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `domElement`  
  任意。 この属性は非推奨とされました。この属性より `type` 属性が優先されます。 この属性は、ドキュメント化された戻り値が DOM 要素であるかどうかを指定します。 戻り値が DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `type` 属性が設定されておらず `domElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、ドキュメント化された戻り値が `HTMLElement` として処理されます。  
  
  `mayBeNull`  
  任意。 ドキュメント化された戻り値を null に設定できるかどうかを指定します。 戻り値を null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `elementType`  
  任意。 `type` が `Array` であれば、この属性は、配列内の要素の型を指定します。  
  
  `elementInteger`  
  任意。 `type` が `Array` であり、`elementType` が `Number` である場合、この属性は、配列内の要素が整数であるかどうかを指定します。 配列内の要素が整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `elementDomElement`  
  任意。 この属性は非推奨とされました。この属性より `elementType` 属性が優先されます。 `type` が `Array` である場合、この属性は、配列内の要素が DOM 要素であるかどうかを指定します。 要素が DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `elementType` 属性が設定されておらず `elementDomElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、配列内の各要素が `HTMLElement` として処理されます。  
  
  `elementMayBeNull`  
  任意。 `type` が `Array` である場合、配列内の要素を null に設定できるかどうかを指定します。 配列内の要素を null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `locid`  
  任意。 戻り値に関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 識別子の型で指定された形式によって異なります、 [ \<loc >](../ide/loc-javascript.md)タグ。  
  
  `value`  
  任意。 関数コード自体ではなく、IntelliSense による使用のための評価が必要なコードを指定します。 たとえば、この属性を使用して、`Promise` などの非同期コールバックに IntelliSense を提供できます。 `value` 要素で `<returns>` 属性を使用すると、長いコードの実行をバイパスすることで IntelliSense のパフォーマンスを改善できます。  
  
  `description`  
  任意。 戻り値の説明。  
  
## <a name="remarks"></a>解説  
 `<returns>` 要素は、ステートメントの前の関数本体に配置する必要があります。  
  
## <a name="example"></a>例  
 `<returns>` 要素を使用する方法を次のコード例に示します。  
  
```javascript  
function areaFunction(radiusParam)  
{  
    /// <summary>Determines the area of a circle when provided a radius parameter.</summary>  
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>  
    /// <returns type="Number">The area.</returns>  
    var areaVal;  
    areaVal = Math.PI * radiusParam * radiusParam;  
    return areaVal;  
}  
  
// The following examples use the <remarks> element with a value attribute.  
  
function getJson(complete) {   
    /// <returns value='complete("")' ></returns>  
    var r = new XMLHttpRequest();   
    // . . .   
}   
  
getJson(function (json) {   
    json.  // IntelliSense for a String object is   
           // available here.  
});  
  
function calculate(x) {  
    /// <returns value='1'/>  
}  
calculate().  // Completion list for a Number.  
  
```  
  
## <a name="see-also"></a>関連項目  
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)
