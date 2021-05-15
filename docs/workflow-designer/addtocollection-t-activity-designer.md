---
title: AddToCollection&lt;T&gt; アクティビティ デザイナー
description: ワークフロー デザイナーで AddToCollection<T> アクティビティ デザイナーを使用して、AddToCollection <T> アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.AddToCollection`1.UI
ms.assetid: f7fc0702-164e-4370-8946-bb2f9f9384b7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 18811199cce88c5d57332ced99763b4f6233da8d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920193"
---
# <a name="addtocollectiont-activity-designer"></a>AddToCollection\<T> アクティビティ デザイナー

**AddToCollection\<T>** アクティビティ デザイナーは、<xref:System.Activities.Statements.AddToCollection%601> アクティビティを作成および構成するために使用します。

## <a name="the-addtocollectiont-activity"></a>AddToCollection\<T> アクティビティ

<xref:System.Activities.Statements.AddToCollection%601> アクティビティでは、項目をコレクションに追加します。

### <a name="using-the-addtocollectiont-activity-designer"></a>AddToCollection\<T> アクティビティ デザイナーの使用

**AddToCollection\<T>** アクティビティ デザイナーは、 **[ツールボックス]** の **[コレクション]** カテゴリにあり、ワークフロー デザイナーの **[ツールボックス]** タブをクリックしてアクセスします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl**+**Alt**+**X** キーを押します。

**AddToCollection\<T>** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される任意のワークフロー デザイナー サーフェス (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 **AddToCollection\<T>** アクティビティ デザイナーをドロップすると、既定の <xref:System.Activities.Activity.DisplayName%2A> の AddToCollection<Int32\> を持つ <xref:System.Activities.Statements.AddToCollection%601> アクティビティが作成されます (既定では、*TypeArgument* は **Int32** です。 TypeArgument はプロパティ グリッドで変更できます)。<xref:System.Activities.Activity.DisplayName%2A> 値は、**AddToCollection<T\>** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-addtocollectiont-properties"></a>AddToCollection\<T> のプロパティ

次の表に、<xref:System.Activities.Statements.AddToCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.AddToCollection%601> アクティビティの表示名。 規定値は AddToCollection<Int32\> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.AddToCollection%601.Item%2A>|はい|Collection\<T> に追加する項目。 この項目の型は *T* であり、*TypeArgument* 型です。 項目を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.AddToCollection%601.Collection%2A>|はい|項目の追加先のコレクション。 このコレクションの型は **ICollection<TypeArgument\>** です。 コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|はい|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型。 既定では、この *TypeArgument* 型は **Int32** に設定されます。 型を変更するには、プロパティ グリッドのコンボ ボックスで、*TypeArgument* の値を変更します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T> アクティビティ デザイナー](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)
