---
title: ワークフローデザイナー-存在 &lt;T &gt; アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ExistsInCollection`1.UI
ms.assetid: 0acf9a13-caf5-4bb4-ba22-ec37d2b7267a
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a9dc1f6a3694b6164fe4f2187fa4c6e2b42751e7
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650486"
---
# <a name="existsincollectiont-activity-designer"></a>> アクティビティデザイナー \<T 存在するコレクション

@No__t_2 アクティビティを作成および構成するには、 **\<T >** アクティビティデザイナーを使用します。

## <a name="the-existsincollectiont-activity"></a>> アクティビティ \<T 存在するコレクション

<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティでは、指定した項目が特定のコレクションに存在するかどうかを確認します。

### <a name="using-the-existsincollectiont-activity-designer"></a>> アクティビティデザイナー \<T の存在を持つコレクションの使用

ワークフローデザイナーの **[ツールボックス]** タブをクリックするとアクセスされる **[ツールボックス]** の **[コレクション]** カテゴリには、 **\<T >** アクティビティデザイナーがあります。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、 **ctrl** +**Alt** +**X**キーを押します。

> アクティビティデザイナー **\<T**の存在を、 **[ツールボックス]** からドラッグして、アクティビティを通常配置している任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) ワークフローデザイナーにドロップできます。 これにより、<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティが作成されます。このアクティビティは、既定の <xref:System.Activities.Activity.DisplayName%2A> 存在する場合は < Int32 \> になります。 (既定では、 *Typeargument*は**Int32**です。 プロパティグリッドで変更できます)。 @No__t_0 値は、\> アクティビティデザイナーの **<** のヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。 他のプロパティは、プロパティ グリッドで編集する必要があります。

### <a name="the-existsincollectiont-properties"></a>> プロパティ \<T 存在するコレクション

次の表は、<xref:System.Activities.Statements.ExistsInCollection%601> のプロパティと、デザイナーでのそれらの使用方法を示しています。

|プロパティ名|必要|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.ExistsInCollection%601> アクティビティの表示名。 既定値は、< Int32 \> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Item%2A>|True|コレクション内で検索する項目 \<T >。 この項目の型は*T*で、 *typeargument*型です。 項目を指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.ExistsInCollection%601.Collection%2A>|True|項目が存在するかどうかを確認するコレクション。 このコレクションの型は**ICollection < TypeArgument \> です。** コレクションを指定するには、プロパティ グリッドで Visual Basic の式を入力します。|
|*TypeArgument*|True|<xref:System.Collections.Generic.ICollection%601> に格納される項目の T 型。 既定では、この*Typeargument*型は**Int32**に設定されています。 型を変更するには、プロパティグリッドで、コンボボックスの*Typeargument*の値を変更します。|
|<xref:System.Activities.Activity%601.Result%2A>|False|指定した項目がコレクション内に存在するかどうかを示す値。 結果にバインドする変数を指定するには、プロパティ グリッドで Visual Basic 変数を入力します。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [AddToCollection\<T>](../workflow-designer/addtocollection-t-activity-designer.md)
- [ClearCollection\<T>](../workflow-designer/clearcollection-t-activity-designer.md)
- [RemoveFromCollection\<T>](../workflow-designer/removefromcollection-t-activity-designer.md)