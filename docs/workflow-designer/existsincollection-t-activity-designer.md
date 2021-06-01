---
title: ExistsInCollection&lt;T&gt; アクティビティ デザイナー
description: ワークフロー デザイナーで ExistsInCollection<T> アクティビティ デザイナーを使用して、ExistsInCollection<T> アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 971d6bd028315ae4a8b6f3a88164c97c6f95712b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961327"
---
# <a name="existsincollectiont-activity-designer"></a>ExistsInCollection\<T> アクティビティ デザイナー

**ExistsInCollection\<T>** アクティビティ デザイナーは、<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティを作成および構成するために使用されます。

## <a name="the-existsincollectiont-activity"></a>The ExistsInCollection\<T> アクティビティ

<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティでは、指定した項目が特定のコレクションに存在するかどうかを確認します。

### <a name="using-the-existsincollectiont-activity-designer"></a>ExistsInCollection\<T> アクティビティ デザイナーの使用

**ExistsInCollection\<T>** アクティビティ デザイナーは、 **[ツールボックス]** の **[コレクション]** カテゴリにあり、ワークフロー デザイナーの **[ツールボックス]** タブをクリックしてアクセスします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** + **Alt**+ **X** キーを押します。

**ExistsInCollection\<T>** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置するワークフロー デザイナー画面の任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 これにより、ExistsInCollection<Int32\> の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.Activities.Statements.ExistsInCollection%601> アクティビティが作成されます (既定では、*TypeArgument* は **Int32** です。 それはプロパティ グリッドで変更できます)。<xref:System.Activities.Activity.DisplayName%2A> 値は、**ExistsInCollection<T\>** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-existsincollectiont-properties"></a>ExistsInCollection\<T> のプロパティ

次の表に、<xref:System.Activities.Statements.ExistsInCollection%601> のプロパティと、デザイナーでのそれらの使用方法について説明します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティの表示名。 既定値は ExistsInCollection<Int32\> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|はい|Collection\<T> 内で検索される項目。 この項目の型は *T* であり、*TypeArgument* 型です。 項目を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|はい|項目が存在するかどうかを確認するコレクション。 このコレクションの型は **ICollection<TypeArgument\> です。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|はい|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型。 既定では、この *TypeArgument* 型は **Int32** に設定されます。 型を変更するには、プロパティ グリッドのコンボ ボックスで、*TypeArgument* の値を変更します。|
|<xref:System.Activities.Activity%601.Result%2A>|いいえ|指定した項目がコレクション内に存在するかどうかを示す値。 結果にバインドする変数を指定するには、プロパティ グリッドで Visual Basic 変数を入力します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)