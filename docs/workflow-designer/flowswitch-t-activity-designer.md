---
title: ワークフロー デザイナー - FlowSwitch&lt;T&gt; アクティビティ デザイナー
description: FlowSwitch<T> アクティビティがどのように一致条件に基づいて制御フローの分岐を提供する条件ノードであるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6f61dd3f14ba527e9f5be0e009825902e683fb1d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876564"
---
# <a name="flowswitcht-activity-designer"></a>FlowSwitch\<T> アクティビティ デザイナー

<xref:System.Activities.Statements.FlowSwitch%601> アクティビティは、3 つ以上の代替分岐が必要な場合に、一致条件に基づいて制御フローの分岐を提供する条件ノードです。 フローの分岐に必要なパスが 2 つのみである場合は、代わりに <xref:System.Activities.Statements.FlowDecision> アクティビティを使用します。

## <a name="the-flowswitcht-activity"></a>FlowSwitch\<T> アクティビティ

<xref:System.Activities.Statements.FlowSwitch%601> アクティビティには、評価時に *T* 型の値 (ジェネリック パラメーターにより指定される) を返す <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> が含まれます。 アクティビティには、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> のセットも含まれます。これは、この評価の想定される結果から、<xref:System.Activities.Statements.FlowNode> オブジェクトへの一意のマッピングを指定します。 実行された <xref:System.Activities.Statements.FlowNode> は、その *T* 型のオブジェクトが、評価された <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の値と一致します。 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> case は、一致が取得されない case に対して (必要に応じて) 提供できます。

### <a name="using-the-flowswitcht-activity-designer"></a>FlowSwitch\<T> アクティビティ デザイナーの使用

**FlowSwitch\<T>** デザイナーは、 **[ツールボックス]** の **[フローチャート]** カテゴリにあります。ワークフロー デザイナーの左側にある **[ツールボックス]** タブをクリックすることでアクセスできます。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** +**Alt**+ **X** キーを押します。

**FlowSwitch\<T>** デザイナーは、 **[ツールボックス]** からドラッグして、**Flowchart** アクティビティ デザイナー内のワークフロー デザイナー画面にドロップできます。 表示される **[型の選択]** ウィンドウを使用して、<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価から取得される型 (コード内でそのジェネリック パラメーターにより <xref:System.Activities.Statements.FlowSwitch%601> に関連付けられる) を指定します。 この手順により、<xref:System.Activities.Statements.Flowchart> アクティビティ内に、**Switch** というラベルの付いた <xref:System.Activities.Statements.FlowSwitch%601> アクティビティが作成されます。 "VB の式を入力してください" というヒント テキストが表示される場所をクリックすると、 **[プロパティ]** ウィンドウの **[式]** ボックスに <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> を入力できます。

**FlowSwitch\<T>** アクティビティ デザイナーにマウス ポインターを重ねると、正方形のハンドルが端に表示されます。これを使って、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> をリンクできます。 **FlowSwitch<T\>** などのアクティビティ デザイナーを **Flowchart** にドラッグすると、それらが表す <xref:System.Activities.Activity> オブジェクトを相互にリンクして、実行の順序を指定できるようになります。 <xref:System.Activities.Statements.FlowSwitch%601> に関連付けられた <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> の 1 つを作成するには、**FlowSwitch<T\>** の周囲にある正方形の case ハンドルの 1 つをクリックし、マウス ボタンを押したまま、接続先のアクティビティの周囲にある同様のハンドルの 1 つにドラッグします。このハンドルは、デザイナーにマウス ポインターを置くと表示されます。 マウス ボタンを放すと、**FlowSwitch<T\>** から接続先のデザイナーに向かう、この case を表す矢印が表示されます。 この case の既定値が矢印に表示されます。その値は、 **[プロパティ]** ウィンドウの **[Case]** ボックスで編集できます。

### <a name="the-flowswitcht-properties"></a>FlowSwitch\<T> のプロパティ

次の表に、<xref:System.Activities.Statements.FlowSwitch%601> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|はい|実行パスのどの <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> に切り替えるかを決定するために評価される式を指定します。|
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|いいえ|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価によって得られる可能性のある結果から、<xref:System.Activities.Statements.FlowNode> オブジェクトのセットへの一意のマッピングを指定します。|
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|はい|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価が、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> オブジェクトに含まれる値のいずれにも一致しない場合のマッピングを指定します。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designers.md)
- [フローチャート](../workflow-designer/flowchart-activity-designer.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
