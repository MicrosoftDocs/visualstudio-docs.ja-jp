---
title: If アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.If.UI
ms.assetid: 930a8fa2-db98-43e9-ad6d-a85cc7a6519a
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6b35fe7f1b55dde25ec896f230f66cef00d24eed
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659059"
---
# <a name="if-activity-designer"></a>If アクティビティ デザイナー
<xref:System.Activities.Statements.If> アクティビティでは、条件を評価し、その評価の結果に応じてアクティビティを実行します。 このアクティビティは、手順型モデルのプログラミング スタイルを使用する場合に最も役立ちます。 <xref:System.Activities.Statements.If> アクティビティは、<xref:System.Activities.Statements.Sequence> アクティビティや <xref:System.Activities.Statements.Parallel> アクティビティなどの内部に入れ子にすることができます。 <xref:System.Activities.Statements.Flowchart> アクティビティを使用している場合は、代わりに、<xref:System.Activities.Statements.FlowDecision> アクティビティの使用を検討してください。

## <a name="if-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの If のプロパティ
 次の表に、最も役に立つ <xref:System.Activities.Statements.If> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必要|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.If.Condition%2A>|True|実行する子アクティビティを決定する条件。 @No__t_0 を設定するには、 **If**アクティビティデザイナーまたはプロパティグリッドの **[条件]** ボックスに [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 式を入力します。|
|<xref:System.Activities.Statements.If.Else%2A>|False|@No__t_0 が**false**の場合に実行するアクティビティ。 @No__t_0 分岐によって実行されるアクティビティを追加するには、"ここにアクティビティをドロップします" というヒントテキストが表示された**if**アクティビティデザイナーの **[Else]** ボックスに、 **[ツールボックス]** からアクティビティをドロップします。|
|<xref:System.Activities.Statements.If.Then%2A>|False|@No__t_0 が**true**の場合に実行するアクティビティ。 @No__t_0 分岐によって実行されるアクティビティを追加するには、"ここにアクティビティをドロップします" というヒントテキストが表示された**If**アクティビティデザイナーの **[Then** ] ボックスに、 **[ツールボックス]** からアクティビティをドロップします。|

## <a name="see-also"></a>参照
 [シーケンス](../workflow-designer/sequence-activity-designer.md)の[並列](../workflow-designer/parallel-activity-designer.md)[制御フロー](../workflow-designer/control-flow-activity-designers.md)