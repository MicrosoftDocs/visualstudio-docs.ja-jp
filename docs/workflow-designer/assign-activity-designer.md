---
title: ワークフロー デザイナー - Assign アクティビティ デザイナー
description: Assign アクティビティ デザイナーを使用して Assign アクティビティを作成および構成する方法と、Assign アクティビティによって変数または引数に値が割り当てられる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Assign.UI
ms.assetid: ba3feb3c-f144-47ea-926d-cf752b804153
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fe6f649543cee66a1050e5724a9317b7b8806534
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888642"
---
# <a name="assign-activity-designer"></a>Assign アクティビティ デザイナー

**Assign** アクティビティ デザイナーは、<xref:System.Activities.Statements.Assign> アクティビティを作成および構成するために使用します。

## <a name="the-assign-activity"></a>Assign アクティビティ

<xref:System.Activities.Statements.Assign> アクティビティで、変数または引数に値を割り当てます。

### <a name="using-the-assign-activity-designer"></a>Assign アクティビティ デザイナーの使用

**Assign** アクティビティ デザイナーは、 **[ツールボックス]** の **[プリミティブ]** カテゴリにあります。アクセスするには、 **[ツールボックス]** タブをクリックします (または、 **[表示]** メニューの **[ツールボックス]** をクリックするか、Ctrl + Alt + X キーを押します)。

**Assign** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される任意のワークフロー デザイナー サーフェス (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 **Assign** アクティビティ デザイナーをドロップすると、Assign という既定の **DisplayName** を持つ <xref:System.Activities.Statements.Assign> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**Assign** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-assign-properties"></a>Assign のプロパティ

次の表に、<xref:System.Activities.Statements.Assign> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。一部は、ワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Assign> アクティビティの表示名。 既定値は Assign です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Assign.To%2A>|はい|<xref:System.Activities.Statements.Assign.Value%2A> を割り当てる変数または引数。 値は。有効な Visual Basic 識別子である必要があります。 このプロパティを設定するには、**Assign** アクティビティ デザイナーまたはプロパティ グリッドの **[割り当て先]** ボックスに Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.Assign.Value%2A>|はい|変数に割り当てられる値。 <xref:System.Activities.Statements.Assign.Value%2A> を設定するには、**Assign** アクティビティ デザイナーまたはプロパティ グリッドの **[値]** ボックスに Visual Basic の式を入力します。|

## <a name="see-also"></a>関連項目

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [[遅延]](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)