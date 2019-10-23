---
title: ワークフローデザイナー-Pick アクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 983a3ee3539617bf7ee5864c2138b2f0369e228f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650074"
---
# <a name="pick-activity-designer"></a>Pick アクティビティ デザイナー

<xref:System.Activities.Statements.Pick> アクティビティでは、イベント ベースの制御フローを提供します。 このアクティビティは、トリガー起動イベントに応答して、複数の分岐のいずれか 1 つを実行します。

## <a name="the-pick-activity"></a>Pick アクティビティ

<xref:System.Activities.Statements.Pick> アクティビティには、<xref:System.Activities.Statements.PickBranch> オブジェクトのコレクションが含まれており、<xref:System.Activities.Statements.Pick> アクティビティはそのオブジェクトの 1 つを、トリガーの役割を果たす受信イベントに応答して実行できます。 この方法では、ワークフローデザイナーイベントベースの制御フローモデリングを提供します。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。 @No__t_0 アクティビティの実行の開始時に、<xref:System.Activities.Statements.PickBranch> 要素のすべてのトリガーアクティビティがスケジュールされます。 最初のアクティビティが完了すると、対応するアクション アクティビティがスケジュールされ、他のすべてのトリガー アクティビティは取り消されます。

### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法

**[ツールボックス]** の **[制御フロー]** カテゴリにある**Pick**アクティビティデザイナーにアクセスします。 **Pick**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティデザイナーを通常配置している任意の場所 ( **Sequence**アクティビティデザイナー内など) にワークフローデザイナー画面にドロップできます。 ワークフローデザイナーにドロップすると、<xref:System.Activities.Statements.Pick> アクティビティが作成されます。既定では、Branch1 と Branch2 の表示名を持つ要素として、2つの空の <xref:System.Activities.Statements.PickBranch> アクティビティが既定で含まれています。 これらの <xref:System.Activities.Statements.PickBranch.DisplayName%2A> のプロパティ値は、"**分岐**アクティビティデザイナー" ヘッダー、または各分岐の **[プロパティ]** ウィンドウで編集できます。

@No__t_1 オブジェクトのコレクションに <xref:System.Activities.Statements.PickBranch> アクティビティを追加するには、 **[ツールボックス]** から Pick **[branch]** デザイナーをドラッグアンドドロップする方法と、 **Pick**デザイン画面内から右クリックメニューを使用する方法の2つがあります。 詳細については、「[ピック分岐](../workflow-designer/pickbranch-activity-designer.md)」を参照してください。 Pick アクティビティデザイナー内に配置できる項目は、 **Pick** **branch**アクティビティデザイナーのみであることに注意してください。

### <a name="pick-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Pick アクティビティのプロパティ

次の表に、<xref:System.Activities.Statements.Pick> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必要|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.Pick> アクティビティ デザイナーの表示名を指定します。 既定値は Pick です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [Pick アクティビティ](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [Pick アクティビティの使用](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)