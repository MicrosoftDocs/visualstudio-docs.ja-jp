---
title: RemoveFromCollection&lt;T&gt; アクティビティ デザイナー
description: ワークフロー デザイナーで RemoveFromCollection <T> アクティビティ デザイナーを使用して、RemoveFromCollection <T> アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.RemoveFromCollection`1.UI
ms.assetid: 6617ba26-c8bc-4aed-b746-112bf490d288
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9fdaf7172c00d80e5e7615bfcadcc1fb6233c257
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847363"
---
# <a name="removefromcollectiont-activity-designer"></a>RemoveFromCollection\<T> アクティビティ デザイナー

**RemoveFromCollection\<T>** アクティビティ デザイナーは、<xref:System.Activities.Statements.RemoveFromCollection%601> アクティビティを作成および構成するために使用します。

## <a name="the-removefromcollectiontactivity"></a>RemoveFromCollection \<T> アクティビティ

<xref:System.Activities.Statements.RemoveFromCollection%601> アクティビティは、指定した項目を特定のコレクションから削除します。

### <a name="using-the-removefromcollectiont-activity-designer"></a>RemoveFromCollection\<T> アクティビティ デザイナーの使用

**[ツールボックス]** の **[コレクション]** カテゴリで **RemoveFromCollection\<T>** アクティビティ デザイナーにアクセスします。
**RemoveFromCollection\<T>** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置しているワークフロー デザイナー画面の任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 これにより、RemoveFromCollection<Int32\> という既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.Activities.Statements.RemoveFromCollection%601> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> 値は、**RemoveFromCollection<T\>** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-removefromcollectiont-properties"></a>RemoveFromCollection<T\> プロパティ

次の表に、<xref:System.Activities.Statements.RemoveFromCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.RemoveFromCollection%601> アクティビティの省略可能な表示名。 既定値は、RemoveFromCollection<Int32\> です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Item%2A>|はい|**Collection\<T>** から削除する項目。 この項目の型は *T* であり、*TypeArgument* 型です。 項目を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.RemoveFromCollection%601.Collection%2A>|はい|項目の削除元となるコレクション。 このコレクションの型は **ICollection<TypeArgument\>** です。 コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|はい|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型。 既定では、この *TypeArgument* 型は **Int32** に設定されます。 型を変更するには、プロパティ グリッドのコンボ ボックスで、*TypeArgument* の値を変更します。|
|<xref:System.Activities.Activity%601.Result%2A>|いいえ|指定した項目がコレクションから削除されたかどうかを示す値。 結果にバインドする変数を指定するには、プロパティ グリッドで変数を入力します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)