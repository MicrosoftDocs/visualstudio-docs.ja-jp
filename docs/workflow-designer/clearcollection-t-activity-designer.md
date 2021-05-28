---
title: ワークフロー デザイナー - ClearCollection&lt;T&gt; アクティビティ デザイナー
description: ClearCollection<T> アクティビティ デザイナーを使用して、ClearCollection<T> アクティビティを作成して構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ClearCollection`1.UI
ms.assetid: db0e5da2-7b5a-4f1a-864c-f3aeeeeb51a7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 31d576712804a75fdca57374ce82a53ff0d1ce84
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99942088"
---
# <a name="clearcollectiont-activity-designer"></a>ClearCollection\<T> アクティビティ デザイナー

**ClearCollection\<T>** アクティビティ デザイナーは、<xref:System.Activities.Statements.ClearCollection%601> アクティビティを作成および構成するために使用します。

## <a name="the-clearcollectiont-activity"></a>ClearCollection\<T> アクティビティ

<xref:System.Activities.Statements.ClearCollection%601> アクティビティで、指定したすべての項目のコレクションをクリアします。

### <a name="using-the-clearcollectiont-activity-designer"></a>ClearCollection\<T> アクティビティ デザイナーの使用

**ClearCollection\<T>** アクティビティ デザイナーは、 **[ツールボックス]** の **[コレクション]** カテゴリにあり、ワークフロー デザイナーの **[ツールボックス]** タブをクリックしてアクセスします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** + **Alt**+ **X** キーを押します。

**ClearCollection\<T>** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される任意のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 アクティビティ デザイナーをドロップすると、ClearCollection<Int32\> の既定の <xref:System.Activities.Activity.DisplayName%2A> で <xref:System.Activities.Statements.ClearCollection%601> アクティビティが作成されます (既定では、*TypeArgument* は **Int32** です。 TypeArgument はプロパティ グリッドで変更できます)。<xref:System.Activities.Activity.DisplayName%2A> 値は、**ClearCollection<T\>** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-clearcollectiont-properties"></a>ClearCollection\<T> のプロパティ

次の表に、<xref:System.Activities.Statements.ClearCollection%601> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.ClearCollection%601> アクティビティの表示名を指定します (省略可能)。 既定値は ClearCollection<Int32\> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ClearCollection%601.Collection%2A>|はい|クリアする項目のコレクションを指定します。 このコレクションの型は **ICollection\<TypeArgument> です。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|はい|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型を指定します。 既定では、この *TypeArgument* 型は **Int32** に設定されます。 型を変更するには、プロパティ グリッドのコンボ ボックスで、*TypeArgument* の値を変更します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ExistsInCollection\<T>](../workflow-designer/existsincollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)