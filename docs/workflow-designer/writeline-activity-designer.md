---
title: ワークフロー デザイナー - WriteLine アクティビティ デザイナー
description: WriteLine アクティビティと、WriteLine アクティビティ デザイナーを使用し、WriteLine アクティビティを作成して構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.WriteLine.UI
ms.assetid: 1b5f29a8-b7fd-477e-949e-2f689cae3c96
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 7cb4806949b21a6c92548b91623e63306f2a7722
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875108"
---
# <a name="writeline-activity-designer"></a>WriteLine アクティビティ デザイナー

**WriteLine** アクティビティ デザイナーは、<xref:System.Activities.Statements.WriteLine> アクティビティを作成および構成するために使用します。

## <a name="the-writeline-activity"></a>WriteLine アクティビティ

<xref:System.Activities.Statements.WriteLine> アクティビティは、指定された <xref:System.IO.TextWriter> オブジェクトにテキストを書き込みます。 <xref:System.IO.TextWriter> を指定しない場合、<xref:System.Activities.Statements.WriteLine> はテキストをコンソールに書き込みます。

### <a name="using-the-writeline-activity-designer"></a>WriteLine アクティビティ デザイナーの使用

**[ツールボックス]** の **[プリミティブ]** カテゴリで、**WriteLine** アクティビティ デザイナーにアクセスします。 **WriteLine** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される通常のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 この操作により、WriteLine という既定の <xref:System.Activities.Statements.WriteLine> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**WriteLine** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-writeline-properties"></a>WriteLine プロパティ

次の表に、<xref:System.Activities.Statements.WriteLine> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集でき、一部のプロパティは、ワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.WriteLine> アクティビティの表示名。 既定値は WriteLine です。 <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.WriteLine.Text%2A>|いいえ|書き込むテキスト。 このプロパティを設定するには、**WriteLine** アクティビティ デザイナーの **[テキスト]** ボックスまたはプロパティ グリッドに、Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.WriteLine.TextWriter%2A>|いいえ|<xref:System.IO.TextWriter> による <xref:System.Activities.Statements.WriteLine> の書き込み先の <xref:System.Activities.Statements.WriteLine.Text%2A>。 既定はコンソールです。|

## <a name="see-also"></a>関連項目

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [[遅延]](../workflow-designer/delay-activity-designer.md)
- [InvokeMethod](../workflow-designer/invokemethod-activity-designer.md)
