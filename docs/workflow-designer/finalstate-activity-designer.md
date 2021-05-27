---
title: ワークフロー デザイナー - FinalState アクティビティ デザイナー
description: FinalState デザイナーを使用し、ステート マシン インスタンスを終了させる状態を作る方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: aa186893-8775-40dd-981f-8593ead831d0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a6ec51d17453a13f8c3ab1adffc5447afb5db7e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894180"
---
# <a name="finalstate-activity-designer"></a>FinalState アクティビティ デザイナー

<xref:System.Activities.Core.Presentation.FinalState> デザイナーは、ステート マシンのインスタンスを終了する <xref:System.Activities.Statements.State> を作成するために使用されます。

## <a name="using-the-finalstate-activity-designer"></a>FinalState アクティビティ デザイナーの使用

**FinalState** デザイナーは、ステート マシン内の最終状態として事前に構成済みの <xref:System.Activities.Statements.State> を作成するために使用されます。 <xref:System.Activities.Core.Presentation.FinalState> アクティビティ デザイナーを使用して作成された <xref:System.Activities.Statements.State> の <xref:System.Activities.Statements.State.IsFinal%2A> プロパティは **true** に設定されていますが、<xref:System.Activities.Statements.State.Exit%2A> アクティビティとそれが発生元の遷移はありません。 <xref:System.Activities.Core.Presentation.FinalState> アクティビティ デザイナーを使用し、ステート マシン内の最終状態として事前に構成済みの <xref:System.Activities.Statements.State> アクティビティを追加するには、**FinalState** アクティビティ デザイナーを **[ツールボックス]** の **[ステート マシン]** セクションからドラッグして、ワークフロー デザイナーにドロップします。 <xref:System.Activities.Core.Presentation.FinalState> アクティビティ デザイナーは、<xref:System.Activities.Statements.StateMachine> にドロップして遷移を後で追加できます。または遷移は、<xref:System.Activities.Core.Presentation.FinalState> アクティビティ デザイナーをドロップしたときに作成できます。 遷移の作成の詳細については、[遷移](../workflow-designer/transition-activity-designer.md)に関するページを参照してください。

### <a name="state-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの State アクティビティのプロパティ

次の表に、<xref:System.Activities.Core.Presentation.FinalState> デザイナーを使用して設定できるプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティの中には、プロパティ グリッドで編集できるものがあります。また、その一部はデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.State.DisplayName%2A>|いいえ|ヘッダーの <xref:System.Activities.Statements.State> アクティビティ デザイナーの表示名を指定します。 既定値は **State** です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。 <xref:System.Activities.Statements.State.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Statements.State.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.State.Entry%2A>|いいえ|この状態の遷移時に発生するアクションを指定します。 この値は **[ツールボックス]** からアクティビティをドラッグし、状態の <xref:System.Activities.Statements.State.Entry%2A> セクションにドロップして設定できます。|

## <a name="see-also"></a>関連項目

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [State](../workflow-designer/state-activity-designer.md)
- [移行](../workflow-designer/transition-activity-designer.md)