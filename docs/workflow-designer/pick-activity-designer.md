---
title: ワークフロー デザイナー - Pick アクティビティ デザイナー
description: Pick アクティビティによってイベントベースの制御フローを用意し、トリガー イベントに応答して複数の分岐のいずれかを実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5b616cf3d9b7eba5b2a2e9de23546a8a5f9c36ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968698"
---
# <a name="pick-activity-designer"></a>Pick アクティビティ デザイナー

<xref:System.Activities.Statements.Pick> アクティビティでは、イベント ベースの制御フローを提供します。 このアクティビティは、トリガー起動イベントに応答して、複数の分岐のいずれか 1 つを実行します。

## <a name="the-pick-activity"></a>Pick アクティビティ

<xref:System.Activities.Statements.Pick> アクティビティには、<xref:System.Activities.Statements.PickBranch> オブジェクトのコレクションが含まれており、<xref:System.Activities.Statements.Pick> アクティビティはそのオブジェクトの 1 つを、トリガーの役割を果たす受信イベントに応答して実行できます。 この方法で、ワークフロー デザイナーで、イベントベースの制御フロー モデリングを用意します。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。 <xref:System.Activities.Statements.Pick> アクティビティの実行の開始時に、<xref:System.Activities.Statements.PickBranch> 要素のすべてのトリガー アクティビティがスケジュールされます。 最初のアクティビティが完了すると、対応するアクション アクティビティがスケジュールされ、他のすべてのトリガー アクティビティは取り消されます。

### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法

**[ツールボックス]** の **[制御フロー]** カテゴリにある **Pick** アクティビティ デザイナーにアクセスします。 **Pick** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、通常アクティビティ デザイナーが配置されるワークフロー デザイナー画面 (**Sequence** アクティビティ デザイナーなど) にドロップできます。 ワークフロー デザイナーにドロップすると、<xref:System.Activities.Statements.Pick> アクティビティが作成されます。これには、既定で、Branch1 と Branch2 という表示名を持つ 2 つの空の <xref:System.Activities.Statements.PickBranch> アクティビティが要素として含まれています。 それぞれの <xref:System.Activities.Statements.PickBranch.DisplayName%2A> プロパティの値は、**PickBranch** アクティビティ デザイナーのヘッダー内、または各分岐の **[プロパティ]** ウィンドウ内で編集できます。

<xref:System.Activities.Statements.PickBranch> アクティビティを <xref:System.Activities.Statements.Pick> オブジェクトのコレクションに追加する方法は 2 つあります。 **[ツールボックス]** から **PickBranch** デザイナーをドラッグ アンド ドロップするか、**Pick** デザイン画面内から右クリックメニューを使用します。 詳細については、「[PickBranch](../workflow-designer/pickbranch-activity-designer.md)」トピックを参照してください。 **Pick** アクティビティ デザイナーに配置できる項目は、**PickBranch** アクティビティ デザイナーのみであることに注意してください。

### <a name="pick-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Pick アクティビティのプロパティ

次の表に、<xref:System.Activities.Statements.Pick> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|ヘッダーの <xref:System.Activities.Statements.Pick> アクティビティ デザイナーの表示名を指定します。 既定値は Pick です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [Pick アクティビティ](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [Pick アクティビティの使用](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)