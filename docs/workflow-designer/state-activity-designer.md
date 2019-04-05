---
title: ワークフロー デザイナーの State アクティビティ デザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.State.UI
ms.assetid: 9455ab37-93a0-4c46-9eb8-b6611ca23167
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 4d07cfeeb713767bc4f711c99b6b482759af2232
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55940765"
---
# <a name="state-activity-designer"></a>State アクティビティ デザイナー

<xref:System.Activities.Statements.State> はステート マシンの状態を表します。

## <a name="using-the-state-activity-designer"></a>State アクティビティ デザイナーの使用

追加する、 <xref:System.Activities.Statements.State> 、ワークフローにドラッグ、**状態**からアクティビティ デザイナー、**ステート マシン**のセクション、**ツールボックス**にドロップし、 <xref:System.Activities.Statements.StateMachine>ワークフロー デザイナー画面でアクティビティ。 <xref:System.Activities.Statements.State> アクティビティは、<xref:System.Activities.Statements.StateMachine> にドロップして遷移を後で追加できます。または遷移は、<xref:System.Activities.Statements.State> アクティビティをドロップしたときに作成できます。 追加する、<xref:System.Activities.Statements.State>アクティビティ ドラッグの 1 つのステップの遷移を作成し、**状態**からのアクティビティ、**ステート マシン**のセクション、**ツールボックス**別上に置きますワークフロー デザイナーでの状態。 ドラッグされている <xref:System.Activities.Statements.State> が別の <xref:System.Activities.Statements.State> の上にある場合、もう一方の <xref:System.Activities.Statements.State> の周囲に 4 つの三角形が表示されます。 
  <xref:System.Activities.Statements.State> を 4 つの三角形のいずれかにドロップすると、ステート マシンに追加され、遷移元の <xref:System.Activities.Statements.State> からドロップされた遷移先の <xref:System.Activities.Statements.State> に遷移が作成されます。 詳細については、[遷移](../workflow-designer/transition-activity-designer.md)を参照してください。

### <a name="state-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの State アクティビティのプロパティ

次の表に、ワークフロー デザイナーを使用して設定できる <xref:System.Activities.Statements.State> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティの中には、プロパティ グリッドで編集できるものがあります。また、その一部はデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.State> アクティビティ デザイナーの表示名を指定します。 既定値は**状態**します。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。 <xref:System.Activities.Statements.State.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Statements.State.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.State.Entry%2A>|False|この状態の遷移時に発生するアクションを指定します。 ときに、<xref:System.Activities.Statements.State>アクティビティが展開されているからアクティビティをドラッグしてこの値を設定することができます、**ツールボックス**にドロップし、**エントリ**状態のセクション。|
|<xref:System.Activities.Statements.State.Exit%2A>|False|この状態からの遷移時に発生するアクションを指定します。 ときに、<xref:System.Activities.Statements.State>アクティビティが展開されているからアクティビティをドラッグしてこの値を設定することができます、**ツールボックス**にドロップし、**終了**状態のセクション。|
|<xref:System.Activities.Statements.State.Transitions%2A>|False|<xref:System.Activities.Statements.State> から発生する可能性のある遷移を一覧表示します。 リスト内の各項目には、関連付けられた <xref:System.Activities.Statements.Transition> と遷移先の <xref:System.Activities.Statements.State> へのリンクがあります。 リンクをクリックすると、デザイナーを <xref:System.Activities.Statements.Transition> または <xref:System.Activities.Statements.State> の展開されたビューに切り替えます。|

## <a name="see-also"></a>関連項目

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [FinalState](../workflow-designer/finalstate-activity-designer.md)
- [Transition](../workflow-designer/transition-activity-designer.md)