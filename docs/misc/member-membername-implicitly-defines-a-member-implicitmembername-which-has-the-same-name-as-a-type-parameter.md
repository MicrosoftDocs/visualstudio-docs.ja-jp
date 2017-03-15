---
title: "メンバー &#39;&lt;membername&gt;&#39; は、型パラメーターと同じ名前のメンバー &#39;&lt;implicitmembername&gt;&#39; を暗黙的に定義します | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "BC32070"
  - "vbc32070"
helpviewer_keywords: 
  - "BC32070"
ms.assetid: cc0b3fcf-c141-47e2-9b33-d2b91c8bf2d6
caps.latest.revision: 10
caps.handback.revision: 10
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# メンバー &#39;&lt;membername&gt;&#39; は、型パラメーターと同じ名前のメンバー &#39;&lt;implicitmembername&gt;&#39; を暗黙的に定義します
ジェネリック クラスのメンバーが、クラスの型パラメーターと同じ名前を持つ暗黙的なメンバーを生成します。  
  
 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] コンパイラは、宣言されている特定のプログラミング要素に対応する暗黙的なメンバーを作成します。 これらの暗黙的なメンバー、つまり*合成*メンバーの概要を次の表に示します。  
  
|宣言された要素|暗黙的に作成されるメンバー|  
|-------------|-------------------|  
|列挙型|`value__` のメンバー|  
|イベント|`add_<eventname>` プロシージャ<br /><br /> `remove_<eventname>` プロシージャ<br /><br /> `<eventname>Event` のフィールド<br /><br /> `<eventname>EventHandler` デリゲート|  
|プロパティ|`get_<propertyname>` プロシージャ<br /><br /> `set_<propertyname>` プロシージャ|  
|`My.` コレクション変数|`m_<variablename>` `Static` 変数<br /><br /> `<variablename>` プロパティ<br /><br /> `get_<variablename>` プロシージャ<br /><br /> `set_<variablename>` プロシージャ|  
|`WithEvents` 変数|`_<variablename>` 変数<br /><br /> `<variablename>` プロパティ<br /><br /> `get_<variablename>` プロシージャ<br /><br /> `set_<variablename>` プロシージャ|  
  
 名前競合の可能性があるため、宣言するプログラミング要素に名前を付ける場合は、これらの暗黙的なメンバーのいずれかと同じ形式を使用することは避ける必要があります。 たとえば、`get_` または `set_` で始まる要素名を避ける必要があります。  
  
 **エラー ID:** BC32070  
  
### このエラーを解決するには  
  
-   型パラメーターの名前を変更できる場合は、上記の表に示した名前との競合を避けるために、型パラメーターの名前を変更します。  
  
-   型パラメーターの名前を保持する必要がある場合は、上記の表に示した名前との競合を避けるために、クラス メンバーの名前を変更します。  
  
## 参照  
 [Declared Element Names](/dotnet/visual-basic/programming-guide/language-features/declared-elements/declared-element-names)   
 [Visual Basic におけるジェネリック型](/dotnet/visual-basic/programming-guide/language-features/data-types/generic-types)   
 [Type List](/dotnet/visual-basic/language-reference/statements/type-list)