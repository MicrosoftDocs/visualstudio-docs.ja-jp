---
title: ワークフロー デザイナー - StateMachine アクティビティ デザイナー
description: StateMachine アクティビティにどのように状態のコレクションが含まれているか、また一般的なステート マシン パラダイムを使用してワーク フローをモデル化するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- StateMachine Designer
- System.Activities.Statements.StateMachine.UI
ms.assetid: 474d5fb3-1049-4b3f-bc6b-7524dbbe1672
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 7fe26f8d0ea127189d115692bd01fa538bf8fb33
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873503"
---
# <a name="statemachine-activity-designer"></a>StateMachine アクティビティ デザイナー

<xref:System.Activities.Statements.StateMachine> アクティビティには状態のコレクションが含まれており、一般的なステート マシン パラダイムを使用してワーク フローをモデル化します。

## <a name="using-the-statemachine-activity-designer"></a>StateMachine アクティビティ デザイナーの使用

<xref:System.Activities.Statements.StateMachine> アクティビティを追加するには、 **[ツールボックス]** の **[ステート マシン]** セクションから **StateMachine** アクティビティ デザイナーをドラッグして、ワークフロー デザイナー画面にドロップします。 この <xref:System.Activities.Statements.StateMachine> アクティビティに子の状態を追加するには、 **[ツールボックス]** から <xref:System.Activities.Statements.State> または <xref:System.Activities.Core.Presentation.FinalState> をドラッグして、**StateMachine** にドロップします。

### <a name="statemachine-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの StateMachine アクティビティのプロパティ

次の表に、ワークフロー デザイナーを使用して設定できる <xref:System.Activities.Statements.StateMachine> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部はデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|ヘッダーの <xref:System.Activities.Statements.StateMachine> アクティビティ デザイナーの表示名を指定します。 既定値は **StateMachine** です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。 <xref:System.Activities.Activity.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
