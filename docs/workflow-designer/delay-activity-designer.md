---
title: ワークフロー デザイナー - Delay アクティビティ デザイナー
description: Delay アクティビティと、Delay アクティビティ デザイナーを使用して Delay アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Delay.UI
ms.assetid: f51742a8-2c9a-47d1-8a23-18459d03ae19
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1b661dddf6c07bca34e5ea044fd1338da68f4e19
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894310"
---
# <a name="delay-activity-designer"></a>Delay アクティビティ デザイナー

**Delay** アクティビティ デザイナーは、<xref:System.Activities.Statements.Delay> アクティビティを作成および構成するために使用します。

## <a name="the-delay-activity"></a>Delay アクティビティ

<xref:System.Activities.Statements.Delay> アクティビティで、ワークフローの実行を、指定した時間だけ遅らせます。

### <a name="use-the-delay-activity-designer"></a>Delay アクティビティ デザイナーを使用する

**Delay** アクティビティ デザイナーは、 **[ツールボックス]** の **[プリミティブ]** カテゴリにあり、ワークフロー デザイナーの **[ツールボックス]** タブをクリックしてアクセスします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** +**Alt**+ **X** キーを押します。

**Delay** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される通常のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 アクティビティ デザイナーをドロップすると、Delay の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.Activities.Statements.Delay> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**Delay** アクティビティ デザイナーのヘッダーで、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-delay-properties"></a>Delay のプロパティ

次の表に、<xref:System.Activities.Statements.Delay> のプロパティと、それらがデザイナーでどのように使用されるかを示します。 これらのプロパティは、プロパティ グリッドで編集でき、一部のプロパティは、ワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Delay> アクティビティの表示名。 既定値は Delay です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Delay.Duration%2A>|はい|ワークフローの実行を遅らせる時間の長さ。 このプロパティは、プロパティ グリッドで設定します。 時間の長さを指定するには、00:00:00 という形式のリテラル <xref:System.TimeSpan>、または Visual Basic の式を入力します。|

## <a name="see-also"></a>関連項目

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [Delay アクティビティ デザイナー](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)