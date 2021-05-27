---
title: ワークフロー デザイナー - ForEach&lt;T&gt; アクティビティ デザイナー
description: ForEach <T> アクティビティが、指定した Values コレクション内の各項目に対して、その Body に含まれるアクティビティを実行するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ForEach`1.UI
ms.assetid: 67097b3a-fcf5-4a72-beb1-2c7784151a86
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d4c594e613d1160794e8310695d61bcc97902caa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876460"
---
# <a name="foreachlttgt-activity-designer"></a>ForEach&lt;T&gt; アクティビティ デザイナー

<xref:System.Activities.Statements.ForEach%601> アクティビティは、指定した <xref:System.Activities.Statements.ForEach%601.Body%2A> コレクション内の各項目に対して、<xref:System.Activities.Statements.ForEach%601.Values%2A> に含まれるアクティビティを実行します。

## <a name="foreacht-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの ForEach<T\> のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.ForEach%601> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.ForEach%601> アクティビティの表示名。 既定値は ForEach<Int32\> です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.ForEach%601.Values%2A>|はい|反復処理を行う項目のコレクション。 <xref:System.Activities.Statements.ForEach%601.Values%2A> を設定するには、**ForEach<T\>** アクティビティ デザイナーまたはプロパティ グリッドの **[値]** ボックスに Visual Basic の式を入力します。|
|*TypeArgument*|はい|ジェネリック パラメーター *T* によって指定された <xref:System.Activities.Statements.ForEach%601.Values%2A> コレクション内の項目の型。既定では、*TypeArgument* は **Int32** に設定されます。 型を変更するには、プロパティ グリッドで *TypeArgument* コンボ ボックスの値を変更します。|

既定では、ループ反復子には、**item** という名前が付けられます。 反復子変数の名前は、<xref:System.Activities.Statements.ForEach%601> アクティビティ デザイナーで変更できます。 ループ反復子は、<xref:System.Activities.Statements.ForEach%601> アクティビティの子の式で使用できます。

## <a name="see-also"></a>関連項目

- [ParallelForEach\<T>](../workflow-designer/parallelforeach-t-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
