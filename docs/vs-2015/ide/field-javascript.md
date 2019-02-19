---
title: '&lt;フィールド&gt;(JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <field> JavaScript XML tag
- field JavaScript XML tag
ms.assetid: c494bae0-3095-42a3-aa0a-4c415188c65c
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b2fe09070261460b7b83f54de44a07cf96d40cf2
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54766557"
---
# <a name="ltfieldgt-javascript"></a>&lt;フィールド&gt;(JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オブジェクトで定義されているフィールドまたはメンバーについて、説明などのドキュメント化情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
<field name="fieldName" static="true|false"  
    type="FieldType" integer="true|false"  
    domElement="true|false" mayBeNull="true|false"  
    elementType="ArrayElementType" elementInteger="true|false"  
    elementDomElement="true|false" elementMayBeNull="true|false"  
    helpKeyword="keyword" locid="descriptionID"  
    value="code">description  
</field>  
```  
  
#### <a name="parameters"></a>パラメーター  
 `name`  
 フィールドまたはメンバーの名前。 `<field>` 要素がコンストラクター関数で使用されている場合は、そのタグが適用されるメンバーを定義する `name` が必要になります。 直接 `<field>` 要素がフィールドの注釈として使用されている場合、この属性は無視され、Visual Studio で使用される名前が、ソース コード内の実際のフィールドの名前になります。  
  
 `static`  
 任意。 フィールドがコンストラクター関数のメンバーであるか、コンストラクター関数によって返されるオブジェクトのメンバーであるかを指定します。 コンストラクター関数のメンバーとしてフィールドを処理する場合は、`true` に設定します。 コンストラクター関数によって返されるオブジェクトのメンバーとしてフィールドを処理する場合は、`false` に設定します。  
  
 `type`  
 任意。 フィールドのデータ型。 型は以下のいずれかです。  
  
- `Number` や `Object` など、ECMAScript 5 仕様に含まれる ECMAScript 言語の型。  
  
- `HTMLElement`、`Window`、`Document` などの DOM オブジェクト。  
  
- JavaScript のコンストラクター関数。  
  
  `integer`  
  任意。 `type` が `Number` である場合に、フィールドが整数かどうかを指定します。 フィールドが整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `domElement`  
  任意。 この属性は非推奨とされました。この属性より `type` 属性が優先されます。 この属性は、ドキュメント化されたフィールドが DOM 要素であるかどうかを指定します。 フィールドが DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `type` 属性が設定されておらず `domElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、ドキュメント化されたフィールドが `HTMLElement` として処理されます。  
  
  `mayBeNull`  
  任意。 ドキュメント化されたフィールドを null に設定できるかどうかを指定します。 フィールドを null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `elementType`  
  任意。 `type` が `Array` であれば、この属性は、配列内の要素の型を指定します。  
  
  `elementInteger`  
  任意。 `type` が `Array` であり、`elementType` が `Number` である場合、この属性は、配列内の要素が整数であるかどうかを指定します。 配列内の要素が整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `elementDomElement`  
  任意。 この属性は非推奨とされました。この属性より `elementType` 属性が優先されます。 `type` が `Array` である場合、この属性は、配列内の要素が DOM 要素であるかどうかを指定します。 要素が DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `elementType` 属性が設定されておらず `elementDomElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、配列内の各要素が `HTMLElement` として処理されます。  
  
  `elementMayBeNull`  
  任意。 `type` が `Array` である場合、配列内の要素を null に設定できるかどうかを指定します。 配列内の要素を null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。  
  
  `helpKeyword`  
  任意。 F1 ヘルプのキーワード。  
  
  `locid`  
  任意。 フィールドに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 識別子の型で指定された形式によって異なります、 [ \<loc >](../ide/loc-javascript.md)タグ。  
  
  `value`  
  任意。 関数コード自体ではなく、IntelliSense による使用のための評価が必要なコードを指定します。 `<field>` では、コンストラクター関数でこの属性がサポートされますが、オブジェクト リテラルではサポートされません。 フィールドの型が定義されていない場合に、この属性を使用して型情報を提供できます。 たとえば、使用することができます`value=’1’`フィールド型を数値として処理します。  
  
  `description`  
  任意。 フィールドの説明。  
  
## <a name="remarks"></a>コメント  
 コンストラクター関数内のフィールドをドキュメント化する場合は、`name` 属性が必要です。 それ以外のすべてのシナリオでは、`<field>` 要素の属性はすべて省略可能です。  
  
 コンストラクター関数をドキュメント化する場合は、`<field>` 要素をフィールド宣言の直前に記述する必要があります。 `name` 属性は、ソース コードで使用されているフィールド名と一致する必要があります。 オブジェクトのメンバーの場合、`name` 要素がオブジェクト メンバー宣言の直前にあれば、`<field>` 属性は省略できます。  
  
## <a name="example"></a>例  
 `<field>` 要素を使用する方法を次のコード例に示します。  
  
```javascript  
// Use of <field> in an object definition.  
var Rectangle = {  
    /// <field type='Number'>The width of the rectangle.</field>  
    wid: 5,  
    /// <field type='Number'>The length of the rectangle.</field>  
    len: 0,  
    /// <field type='Number'>Returns the area of the rectangle.</field>  
    getArea: function (wid, len) {  
        return len * wid;  
    }  
}  
  
// Use of <field> in a constructor function.  
// The name attribute is required.  
function Engine() {  
    /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>  
    this.HorsePower = 150;  
}  
```  
  
## <a name="example"></a>例  
 次の例は、`<field>` 属性を `static` に設定して `true` 要素を使用する方法を示しています。  
  
```javascript  
function Engine() {  
    /// <field name='HorsePower' static='true' type='Number'>static field desc.</field>  
}  
  
Engine.HorsePower = 140;  
// IntelliSense on the field is available here.  
Engine.  
  
```  
  
## <a name="example"></a>例  
 次の例は、`<field>` 属性を `static` に設定して `false` 要素を使用する方法を示しています。  
  
```javascript  
function Engine() {  
    /// <field name='HorsePower' static='false' type='Number'>Non-static field desc.</field>  
}  
  
Engine.HorsePower = 140;  
var eng = new Engine();  
// IntelliSense on the field is available here.  
eng.  
  
```  
  
## <a name="example"></a>例  
 次の例は、`<field>` 属性を指定して `value` 要素を使用する方法を示しています。  
  
```javascript  
function calculator(a) {  
    /// <field name='f' value='1'/>  
}  
new calculator().f.   // Completion list for a Number.  
  
```  
  
## <a name="see-also"></a>関連項目  
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)
