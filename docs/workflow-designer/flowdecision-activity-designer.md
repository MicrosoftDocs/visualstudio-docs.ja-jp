---
title: ワークフロー デザイナー - FlowDecision アクティビティ デザイナー
description: FlowDecision ノードは制御フローを 2 つの選択肢のいずれかに分岐させる条件ノードであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.FlowDecision.UI
ms.assetid: 4a49edc3-3662-4b7b-812e-0a5ba00d6c94
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 77570557563b4aca3109f5bcbdebd16c7af09144
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938435"
---
# <a name="flowdecision-activity-designer"></a>FlowDecision アクティビティ デザイナー

<xref:System.Activities.Statements.FlowDecision> ノードは条件ノードであり、指定した条件を満たすかどうかに基づいて、2 つの選択肢のどちらかに進む制御フローの分岐を提供します。 フローに 3 つ以上の分岐が必要な場合は、代わりに <xref:System.Activities.Statements.FlowSwitch%601> を使用します。

## <a name="the-flowdecision-node"></a>FlowDecision ノード

<xref:System.Activities.Statements.FlowDecision> は、フローを 2 つに分岐できる場合に使用します。 <xref:System.Activities.Statements.FlowDecision> ノードには、<xref:System.Activities.Statements.FlowDecision.Condition%2A> および <xref:System.Activities.Statements.FlowNode> があり、<xref:System.Activities.Statements.FlowDecision.True%2A> または <xref:System.Activities.Statements.FlowDecision.False%2A> という、想定される 2 つの結果のそれぞれに関連付けられています。 <xref:System.Activities.Statements.FlowDecision.Condition%2A> が評価され、この評価の値により、次に <xref:System.Activities.Statements.FlowNode> 内で処理される <xref:System.Activities.Statements.Flowchart> が決定されます。

### <a name="using-the-flowdecision-designer"></a>FlowDecision デザイナーの使用

**FlowDecision** デザイナーは、 **[ツールボックス]** の **[フローチャート]** カテゴリにあります。ワークフロー デザイナーの **[ツールボックス]** タブをクリックすることでアクセスできます。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl**+**Alt**+**X** キーを押します。

**FlowDecision** デザイナーは、 **[ツールボックス]** からドラッグして、**Flowchart** アクティビティ デザイナー内のワークフロー デザイナー画面にドロップできます。 これにより、<xref:System.Activities.Statements.Flowchart> アクティビティ内に、 **[Decision]** というラベルの付いた <xref:System.Activities.Statements.FlowDecision> が作成されます。 デザイナー上にマウス ポインターを置くと、2 つの分岐用の正方形のハンドル ( **[True]** および **[False]** ) が表示されます。

**FlowDecision** デザイナーやその他のデザイナーを **Flowchart** 上にドラッグした後、ノードを互いにリンクさせて実行の順序を指定できます。 ソース ノード (**FlowDecision** の **[True]** および **[False]** 分岐を含む) とターゲット ノードの間にリンクを作成するには、ソース ノードのデザイナー上にマウス ポインターを置きます。その両側に正方形のハンドルが表示されます。 そのハンドルのどちらかをクリックし、マウス ボタンを押したまま、接続先ノードにマウス ポインターを置いたときと同じように表示されるハンドルのどちらかにドラッグします。 マウス ボタンを放すと、これら 2 つのノードの間にリンクが作成されます。このリンクは、接続元デザイナーから接続先デザイナーへの矢印で表されます。

"VB の式を入力してください" というヒント テキストが表示されている場所をクリックすることで、<xref:System.Activities.Statements.FlowDecision.Condition%2A> を示す式を **[プロパティ]** ウィンドウの **[条件]** ボックスに入力できます。

### <a name="the-flowdecision-properties"></a>FlowDecision プロパティ

次の表に、<xref:System.Activities.Statements.FlowDecision> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowDecision.Condition%2A>|はい|フロー制御が使用するパスを決定する条件。|
|<xref:System.Activities.Statements.FlowDecision.True%2A>|いいえ|<xref:System.Activities.Statements.FlowDecision.Condition%2A> が満たされた場合にフロー制御で使用されるパス。|
|<xref:System.Activities.Statements.FlowDecision.False%2A>|いいえ|<xref:System.Activities.Statements.FlowDecision.Condition%2A> が満たされない場合にフロー制御で使用されるパス。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designers.md)
- [フローチャート](../workflow-designer/flowchart-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
