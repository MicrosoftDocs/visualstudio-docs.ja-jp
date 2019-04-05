---
title: ClearCollection&lt;T&gt;アクティビティ デザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ClearCollection`1.UI
ms.assetid: db0e5da2-7b5a-4f1a-864c-f3aeeeeb51a7
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 240e634115e7602c66d69f0dba9cfa52504dc89a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58964181"
---
# <a name="clearcollectionlttgt-activity-designer"></a>ClearCollection&lt;T&gt;アクティビティ デザイナー
**ClearCollection\<T >** 作成および構成するアクティビティ デザイナーが使用される、<xref:System.Activities.Statements.ClearCollection%601>アクティビティ。  
  
## <a name="the-clearcollectiont-activity"></a>ClearCollection\<T > アクティビティ  
 <xref:System.Activities.Statements.ClearCollection%601> アクティビティで、指定したすべての項目のコレクションをクリアします。  
  
### <a name="using-the-clearcollectiont-activity-designer"></a>ClearCollection を使用して\<T > アクティビティ デザイナー  
 **ClearCollection\<T >** アクティビティ デザイナーが記載されて、**コレクション**のカテゴリ、**ツールボックス**をクリックしてアクセスします。**ツールボックス**のタブ、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、選択**ツールバー**から、**ビュー**メニューまたは CTRL + ALT + X)。  
  
 **ClearCollection\<T >** からアクティビティ デザイナーをドラッグすることができます、**ツールボックス**ドロップ、[!INCLUDE[wfd2](../includes/wfd2-md.md)]サーフェス任意の場所、アクティビティを通常配置など内、<xref:System.Activities.Statements.Sequence>. これを作成、 <xref:System.Activities.Statements.ClearCollection%601> 、既定値は、アクティビティ<xref:System.Activities.Activity.DisplayName%2A>ClearCollection の\<Int32 > です。 (既定で、 *TypeArgument*は**Int32**します。 プロパティ グリッドで変更できます)。<xref:System.Activities.Activity.DisplayName%2A>のヘッダーに値を編集できる、 **ClearCollection\<T >** アクティビティ デザイナーまたは、 **DisplayName**プロパティ グリッドのボックスです。 他のプロパティは、プロパティ グリッドで編集する必要があります。  
  
### <a name="the-clearcollectiont-properties"></a>ClearCollection\<T > のプロパティ  
 次の表に、<xref:System.Activities.Statements.ClearCollection%601> のプロパティと、デザイナーでのその使用方法を示します。  
  
|プロパティ名|必須|使用方法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.ClearCollection%601> アクティビティの表示名を指定します (省略可能)。 既定値は ClearCollection\<Int32 > です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|  
|<xref:System.Activities.Statements.ClearCollection%601.Collection%2A>|True|クリアする項目のコレクションを指定します。 このコレクションは、型の**ICollection\<TypeArgument >。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|  
|*TypeArgument*|True|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型を指定します。 既定では、この*TypeArgument*に設定されている型**Int32**します。 型を変更するには、値を変更、 *TypeArgument*プロパティ グリッドでコンボ ボックス。|  
  
## <a name="see-also"></a>関連項目  
 [コレクション](../workflow-designer/collection-activity-designers.md)   
 [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)   
 [ExistsInCollection\<T >](../workflow-designer/existsincollection-t-activity-designer.md)   
 [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)