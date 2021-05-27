---
title: ワークフロー デザイナー - State アクティビティ デザイナー
description: StateMachine アクティビティと、State アクティビティ デザイナーを使用して状態をワークフローに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.State.UI
ms.assetid: 9455ab37-93a0-4c46-9eb8-b6611ca23167
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: abf4e81ecd258668c93b674410f029e6be0f5bf1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873516"
---
# <a name="state-activity-designer"></a>State アクティビティ デザイナー

<xref:System.Activities.Statements.State> はステート マシンの状態を表します。

## <a name="using-the-state-activity-designer"></a>State アクティビティ デザイナーの使用

<xref:System.Activities.Statements.State> をワークフローに追加するには、 **[ツールボックス]** の **[ステート マシン]** セクションから **[State]** のアクティビティ デザイナーをドラッグして、ワークフロー デザイナー サーフェイス上の <xref:System.Activities.Statements.StateMachine> アクティビティにドロップします。 <xref:System.Activities.Statements.State> アクティビティは、<xref:System.Activities.Statements.StateMachine> にドロップして遷移を後で追加できます。または遷移は、<xref:System.Activities.Statements.State> アクティビティをドロップしたときに作成できます。 <xref:System.Activities.Statements.State> アクティビティを追加し、1 ステップの遷移を作成するには、 **[ツールボックス]** の **[ステート マシン]** セクションから **State** アクティビティをドラッグし、ワークフロー デザイナーの別の状態に置きます。 ドラッグされている <xref:System.Activities.Statements.State> が別の <xref:System.Activities.Statements.State> の上にある場合、もう一方の <xref:System.Activities.Statements.State> の周囲に 4 つの三角形が表示されます。 <xref:System.Activities.Statements.State> を 4 つの三角形のいずれかにドロップすると、ステート マシンに追加され、遷移元の <xref:System.Activities.Statements.State> からドロップされた遷移先の <xref:System.Activities.Statements.State> に遷移が作成されます。 詳しくは、[遷移](../workflow-designer/transition-activity-designer.md)に関するページをご覧ください。

### <a name="state-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの State アクティビティのプロパティ

次の表に、ワークフロー デザイナーを使用して設定できる <xref:System.Activities.Statements.State> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティの中には、プロパティ グリッドで編集できるものがあります。また、その一部はデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|いいえ|ヘッダーの <xref:System.Activities.Statements.State> アクティビティ デザイナーの表示名を指定します。 既定値は **State** です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。 <xref:System.Activities.Statements.State.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Statements.State.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.State.Entry%2A>|いいえ|この状態の遷移時に発生するアクションを指定します。 <xref:System.Activities.Statements.State> アクティビティが展開されているとき、この値は **[ツールボックス]** からアクティビティをドラッグし、状態の **[入力]** セクションにドロップして設定できます。|
|<xref:System.Activities.Statements.State.Exit%2A>|いいえ|この状態からの遷移時に発生するアクションを指定します。 <xref:System.Activities.Statements.State> アクティビティが展開されているとき、この値は **[ツールボックス]** からアクティビティをドラッグし、状態の **[終了]** セクションにドロップして設定できます。|
|<xref:System.Activities.Statements.State.Transitions%2A>|いいえ|<xref:System.Activities.Statements.State> から発生する可能性のある遷移を一覧表示します。 リスト内の各項目には、関連付けられた <xref:System.Activities.Statements.Transition> と遷移先の <xref:System.Activities.Statements.State> へのリンクがあります。 リンクをクリックすると、デザイナーを <xref:System.Activities.Statements.Transition> または <xref:System.Activities.Statements.State> の展開されたビューに切り替えます。|

## <a name="see-also"></a>関連項目

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [FinalState](../workflow-designer/finalstate-activity-designer.md)
- [移行](../workflow-designer/transition-activity-designer.md)
