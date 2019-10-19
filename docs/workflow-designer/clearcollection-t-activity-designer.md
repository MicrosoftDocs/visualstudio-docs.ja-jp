---
title: ワークフローデザイナー-ClearCollection <T> アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ClearCollection`1.UI
ms.assetid: db0e5da2-7b5a-4f1a-864c-f3aeeeeb51a7
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a4808c046c4da23bc5c95d3978965afd938962f5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650698"
---
# <a name="clearcollectiont-activity-designer"></a>ClearCollection \<T > アクティビティデザイナー

@No__t_2 アクティビティを作成および構成するには、 **Clearcollection \<T >** アクティビティデザイナーを使用します。

## <a name="the-clearcollectiont-activity"></a>ClearCollection \<T > アクティビティ

<xref:System.Activities.Statements.ClearCollection%601> アクティビティで、指定したすべての項目のコレクションをクリアします。

### <a name="using-the-clearcollectiont-activity-designer"></a>ClearCollection \<T > アクティビティデザイナーの使用

**Clearcollection \<T >** アクティビティデザイナーは、 **[ツールボックス]** の **[コレクション]** カテゴリにあります。このカテゴリにアクセスするには、ワークフローデザイナーの **[ツールボックス]** タブをクリックします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、 **ctrl** +**Alt** +**X**キーを押します。

**Clearcollection \<T >** アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが配置されている任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) ワークフローデザイナーにドロップできます。 アクティビティデザイナーを削除すると、既定の <xref:System.Activities.Activity.DisplayName%2A> ClearCollection < Int32 \> の <xref:System.Activities.Statements.ClearCollection%601> アクティビティが作成されます。 (既定では、 *Typeargument*は**Int32**です。 TypeArgument は、プロパティグリッドで変更できます)。@No__t_0 値は、 **Clearcollection < t \>** アクティビティデザイナーのヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-clearcollectiont-properties"></a>ClearCollection \<T > プロパティ

次の表に、<xref:System.Activities.Statements.ClearCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必要|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.ClearCollection%601> アクティビティの表示名を指定します (省略可能)。 既定値は ClearCollection < Int32 \> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ClearCollection%601.Collection%2A>|True|クリアする項目のコレクションを指定します。 このコレクションの型は**ICollection \<TypeArgument > です。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|True|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型を指定します。 既定では、この*Typeargument*型は**Int32**に設定されています。 型を変更するには、プロパティグリッドで、コンボボックスの*Typeargument*の値を変更します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)