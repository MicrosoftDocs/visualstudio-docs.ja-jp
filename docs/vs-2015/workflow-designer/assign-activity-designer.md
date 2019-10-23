---
title: Assign アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 40ebe465d5eeb12a956d285a8313b0acdbcfb8d5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659184"
---
# <a name="assign-activity-designer"></a>Assign アクティビティ デザイナー
**Assign**アクティビティデザイナーは、<xref:System.Activities.Statements.Assign> アクティビティを作成および構成するために使用されます。

## <a name="the-assign-activity"></a>Assign アクティビティ
 <xref:System.Activities.Statements.Assign> アクティビティで、変数または引数に値を割り当てます。

### <a name="using-the-assign-activity-designer"></a>Assign アクティビティ デザイナーの使用
 **Assign**アクティビティデザイナーは、[**ツールボックス]** の **[プリミティブ]** カテゴリにあります。このカテゴリにアクセスするには、 **[ツール]** ボックス タブをクリックします (または、 **[表示]** メニューの **[ツールボックス]** を選択するか、CTRL + ALT + X キーを押します)。

 **Assign**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置している [!INCLUDE[wfd2](../includes/wfd2-md.md)] 画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 これにより、Assign という既定の**DisplayName**を持つ <xref:System.Activities.Statements.Assign> アクティビティが作成されます。 @No__t_0 は、 **Assign**アクティビティデザイナーのヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-assign-properties"></a>Assign のプロパティ
 次の表に、<xref:System.Activities.Statements.Assign> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集できます。

|プロパティ名|必要|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Assign> アクティビティの表示名。 既定値は Assign です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Assign.To%2A>|True|<xref:System.Activities.Statements.Assign.Value%2A> を割り当てる変数または引数。 有効な Visual Basic 識別子を指定する必要があります。 プロパティを設定するには、 **Assign**アクティビティデザイナーまたはプロパティグリッドの **[To]** ボックスに Visual Basic 式を入力します。|
|<xref:System.Activities.Statements.Assign.Value%2A>|True|変数に割り当てられる値。 @No__t_0 を設定するには、 **Assign**アクティビティデザイナーまたはプロパティグリッドの **[値]** ボックスに Visual Basic 式を入力します。|

## <a name="see-also"></a>参照
 [プリミティブ](../workflow-designer/primitives-activity-designers.md)[遅延](../workflow-designer/delay-activity-designer.md) [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md) [WriteLine](../workflow-designer/writeline-activity-designer.md)