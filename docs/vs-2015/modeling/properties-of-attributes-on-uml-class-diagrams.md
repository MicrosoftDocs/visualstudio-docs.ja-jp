---
title: クラス ダイアグラムの uml 属性のプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.logicalclassdiagram.attribute.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: ba01e064-7424-4e72-98fa-42fa1c30e153
caps.latest.revision: 21
author: alexhomer1
ms.author: gewarren
manager: douge
ms.openlocfilehash: a9cd12bb002efbf28443b8052382c29ed87036b0
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47538393"
---
# <a name="properties-of-attributes-on-uml-class-diagrams"></a>UML クラス図の属性のプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[uml の属性のプロパティにクラス ダイアグラム](https://docs.microsoft.com/visualstudio/modeling/properties-of-attributes-on-uml-class-diagrams)します。  
  
UML クラス図では、クラスとインターフェイスに *属性* を追加できます。 属性は、クラスまたはインターフェイスのインスタンスにアタッチできる値を定義するものです。  
  
 属性を追加するには、クラスまたはインターフェイスを右クリックし、 **[追加]** をポイントして、 **[属性]** をクリックします。  
  
 図にクラスの属性が表示されていない場合は、クラスまたはインターフェイスの上部にあるシェブロンをクリックして展開します。 **[属性]** ヘッダーが表示されたら、 **[+]** をクリックして属性セクションを展開します。  
  
## <a name="signature-of-an-attribute"></a>属性のシグネチャ  
 属性のシグネチャは、UML クラス図のクラスまたはインターフェイスで属性を表す行です。 属性のシグネチャの形式を次に示します。  
  
```  
+ AttributeName : TypeName [*]  
```  
  
 \+ パブリックな可視性を表します。 これ以外に指定できる値は、- (プライベート)、# (保護)、~ (パッケージ) です。  
  
 静的な属性の場合、`AttributeName` は下線付きで表示されます。  
  
 型を持たない属性の場合、`: TypeName` は省略されます。  
  
 `[*]` は、多重度を表します。 複数要素の接続性が 1 の場合は省略されます。  
  
## <a name="properties"></a>プロパティ  
 UML クラス図のクラスまたはインターフェイスの属性のプロパティを次の表に示します。  
  
 属性のプロパティを表示するには、図でクラスまたはインターフェイスの属性を右クリックし、 **[プロパティ]** をクリックします。 プロパティがプロパティ ウィンドウに表示されます。  
  
 属性のプロパティを表示するには、属性を右クリックし、 **[プロパティ]** をクリックします。  
  
|**Property**|**既定値**|説明|  
|------------------|-----------------|-----------------|  
|**既定値**|(空)|分類子がインスタンス化されるときの属性の値。|  
|**読み取り専用**|False|true の場合、属性の値は変更できません。|  
|**静的します。**|False|true の場合、この属性の単一の値がこの型のすべてのインスタンスで共有されます。<br /><br /> true の場合、図に表示される属性の名前に下線が付きます。|  
|**Name**|(新しい名前)|所有する分類子内で一意である必要があります。|  
|**Type**|(なし)|プリミティブ型 (たとえば、 **Integer**)、またはモデルで定義された型。 値はメタデータでコード化する必要があるため、 **10 進数** などの非プリミティブ型は使用できません。 このプロパティに新しい型の名前を入力すると、UML モデル エクスプローラーの **[未指定の型]** セクションに型が 1 つ追加されます。|  
|**可視性**|Public|指定できる値とシグネチャに表示される文字は次のとおりです。<br /><br /> **+ Public** - グローバルに参照できる<br /><br /> **- Private** - 所有元の型の外部では参照できない<br /><br /> **# Protected** - 所有元から派生した型では参照できる<br /><br /> **~ Package** - 同じパッケージ内の他の型で参照できる|  
|**作業項目**|関連付けなし|関連付けられている作業項目の数。 読み取り専用。<br /><br /> 詳細については、次を参照してください。[モデル要素をリンクし、作業項目](../modeling/link-model-elements-and-work-items.md)します。|  
|**リーフには**|False|true の場合、派生型でこの属性の再定義は許可されません。|  
|**派生します。**|False|true の場合、この属性は他の属性から計算されます。 たとえば、Diagonal は Width と Height から計算されます。 詳細は、 **Description** またはアタッチされたコメントに記述する必要があります。|  
|**説明**|(空)|一般的なメモとして、または属性の値に対する制約を定義するために使用します。|  
|**多重度**|1|**1** : この属性は、指定した型の値を 1 つ持ちます。<br /><br /> **0..1** : この属性には、 `null`値を指定できます。<br /><br /> **\*** : この属性の値は、値のコレクションです。<br /><br /> **1..\***  -この属性の値は、少なくとも 1 つの値を含むコレクション。<br /><br /> *n* **..** *m* : この属性の値は、 *n* ～ *m* 個の値を含むコレクションです。|  
|**順序付け**|False|true の場合、コレクションは順序付きリストの形式です **複数要素の接続性** が 1 より大きい場合。|  
|**一意では**|False|true の場合、コレクション内に重複値は存在しません。 **複数要素の接続性** が 1 より大きい場合。|  
  
## <a name="see-also"></a>関連項目  
 [UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)   
 [UML クラス ダイアグラムで型のプロパティ](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [UML クラス図の操作のプロパティ](../modeling/properties-of-operations-on-uml-class-diagrams.md)   
 [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)   
 [UML クラス図: ガイドライン](../modeling/uml-class-diagrams-guidelines.md)



