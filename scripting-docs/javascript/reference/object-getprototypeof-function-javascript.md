---
title: "Object.getPrototypeOf 関数 (JavaScript) | Microsoft Docs"
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
helpviewer_keywords: 
  - "getPrototypeOf 関数 [JavaScript]"
  - "Object.getPrototypeOf 関数 [JavaScript]"
ms.assetid: 1c59cd7a-a7e2-4c5c-83ec-e6bd2b104d9f
caps.latest.revision: 9
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
caps.handback.revision: 9
---
# Object.getPrototypeOf 関数 (JavaScript)
オブジェクトのプロトタイプを返します。  
  
## 構文  
  
```javascript  
Object.getPrototypeOf(object)  
```  
  
#### パラメーター  
 `object`  
 必須です。  プロトタイプを参照するオブジェクト。  
  
## 戻り値  
 `object` 引数のプロトタイプ。  プロトタイプもオブジェクトです。  
  
## 例外  
 `object` 引数がオブジェクトではない場合は、`TypeError` 例外がスローされます。  
  
## 使用例  
 `Object.getPrototypeOf` 関数の使用例を次に示します。  
  
```javascript  
// Create a constructor function.  
function Pasta(grain, width) {  
    this.grain = grain;  
    this.width = width;  
}  
// Create an object from the pasta constructor.  
var spaghetti = new Pasta("wheat", 0.2);  
  
// Obtain the prototype from the object.  
var proto = Object.getPrototypeOf(spaghetti);  
  
// Add a property to the prototype and validate that  
// the original object has the property.  
proto.foodgroup = "carbohydrates";  
document.write(spaghetti.foodgroup + " ");  
  
// Verify that the prototype obtained from the object  
// is the same as the prototype of the constructor.  
var result = (proto === Pasta.prototype);  
document.write(result + " ");  
  
// Verify that prototype obtained from the object  
// is a prototype of the original object.  
var result = proto.isPrototypeOf(spaghetti);  
document.write(result);  
  
// Output: carbohydrates true true  
```  
  
## 使用例  
 `Object.getPrototypeOf` 関数を使用してデータ型を検証する例を次に示します。  
  
```javascript  
var reg = /a/;  
var result = (Object.getPrototypeOf(reg) === RegExp.prototype);  
document.write(result + " ");  
  
var err = new Error("an error");  
var result = (Object.getPrototypeOf(err) === Error.prototype);  
document.write(result);  
  
// Output: true true  
  
```  
  
## 必要条件  
 [!INCLUDE[jsv9](../../javascript/includes/jsv9-md.md)]  
  
## 参照  
 [prototype プロパティ \(Object\)](../../javascript/reference/prototype-property-object-javascript.md)   
 [isPrototypeOf メソッド \(Object\)](../../javascript/reference/isprototypeof-method-object-javascript.md)