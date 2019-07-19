---
title: JavaScript IntelliSense の JSDoc コメントを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: a0dadc81-3755-4a47-bcee-c1010819ff2a
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f4d300651731b38b9b86421d36d9de169dc6464d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188783"
---
# <a name="create-jsdoc-comments-for-javascript-intellisense"></a>JavaScript IntelliSense の JSDoc コメントを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IntelliSense in Visual Studio は、標準的な JSDoc コメントを使用してスクリプトに追加する情報を表示します。 JSDoc コメントを使用すると、関数、フィールド、変数などのコード要素についての情報を指定できます。  

## <a name="jsdoc-comment-tags"></a>JSDoc コメント用のタグ  
 次の標準的な JSDoc コメント タグは、コードについての情報を表示するために IntelliSense によって使用されます。  

|  JSDoc タグ   |                       構文                        |                                                     メモ                                                      |
|--------------|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| @deprecated  |              @deprecated *説明*              |                                   非推奨の関数またはメソッドを指定します。                                   |
| @description |             @description *説明*              |                              関数またはメソッドの説明を指定します。                               |
|    @param    | @param {*型*} *パラメーター名*<em>説明</em> | 関数またはメソッドのパラメーターの情報を指定します。<br /><br /> TypeScript もサポートしています。@paramTagします。 |
|  @property   |          @property {*型*} *プロパティ名*          |   オブジェクトで定義されているフィールドまたはメンバーについて、説明を含む情報を指定します。    |
|   @returns   |                  @returns {*型*}                  |           戻り値を指定します。<br /><br /> TypeScript を使用して@returnTypeの代わりに@returnsします。           |
|   @summary   |               @summary *説明*                |                   関数またはメソッドの説明を指定します (同じ@description)。                   |
|    @type     |                   @type {*型*}                    |                                定数または変数の種類を指定します。                                |
|   @typedef   |         @typedef {*型*} *カスタム型名*          |                                            カスタム型を指定します。                                            |

### <a name="examples"></a>使用例  
 次の例では、使用、 @description、 @param、および@returnJSDoc タグという名前の関数`getArea`します。  

```javascript  
/** @description Determines the area of a circle that has the specified radius parameter.  
 * @param {number} radius The radius of the circle.  
 * @return {number}  
 */  
function getArea(radius) {  
    var areaVal;  
    areaVal = Math.PI * radius * radius;  
    return areaVal;  
}  
```  

 前の例では、IntelliSense は説明、パラメーター、および `getArea` の始めかっこを入力したときに返す情報を表示します。  

 ![関数の IntelliSense 情報](../ide/media/js-intellisense-jsdoc-comments.png "JS_IntelliSense_JSDoc_Comments")  

 次の例は、使用する方法を示します、@typedefにタグを付ける、@propertyタグ。  

```javascript  
/**  
  * @typedef {object} Weather  
  * @property {string} current The current weather.  
  */  
function getForecast(Weather) {  
}  

var w = new Weather();  
```  

 次の例では、使用、 @type JSDoc タグ。 この例で示すように、最初のアスタリスクのペア (\*\*) の後に続く 1 つのアスタリスク (*) は必須ではありません。  

```javascript  
/**  
    @type {string}  
*/  
const RED = 'FF0000';  

```  

 次の例は、使用する方法を示します、 @deprecated JSDoc タグ。  

```javascript  
/**  
 * @deprecated since version 2.0  
 */  
function old() {  
}  
```
