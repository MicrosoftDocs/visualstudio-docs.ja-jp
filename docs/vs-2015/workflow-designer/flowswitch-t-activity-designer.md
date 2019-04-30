---
title: FlowSwitch&lt;T&gt;アクティビティ デザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Core.Presentation.FlowSwitchLink.UI
- System.Activities.Statements.FlowSwitch`1.UI
- System.Activities.Core.Presentation.FlowSwitchLink`1.UI
- System.Activities.Core.Presentation.FlowSwitchLinkIdentifier.UI
ms.assetid: 5b9c5afe-7499-4ee8-8c33-28aff14bde07
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ccd3e328a904540dd03c85f53634dc1eaab96c6e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943308"
---
# <a name="flowswitchlttgt-activity-designer"></a>FlowSwitch&lt;T&gt;アクティビティ デザイナー
<xref:System.Activities.Statements.FlowSwitch%601> アクティビティは、3 つ以上の代替分岐が必要な場合に、一致条件に基づいて制御フローの分岐を提供する条件ノードです。 フローの分岐に必要なパスが 2 つのみである場合は、代わりに <xref:System.Activities.Statements.FlowDecision> アクティビティを使用します。  
  
## <a name="the-flowswitcht-activity"></a>FlowSwitch\<T > アクティビティ  
 <xref:System.Activities.Statements.FlowSwitch%601>アクティビティが含まれています、<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>型の値を返す*T* (ジェネリック パラメーターで指定) 評価されたときにします。 アクティビティには、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> のセットも含まれます。これは、この評価の想定される結果から、<xref:System.Activities.Statements.FlowNode> オブジェクトへの一意のマッピングを指定します。 <xref:System.Activities.Statements.FlowNode>型のオブジェクトが、1 つは、実行*T*評価の値と一致する<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>します。 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> case は、一致が取得されない case に対して (必要に応じて) 提供できます。  
  
### <a name="using-the-flowswitcht-activity-designer"></a>FlowSwitch を使用して\<T > アクティビティ デザイナー  
 **FlowSwitch\<T >** アクティビティ デザイナーが記載されて、**フローチャート**のカテゴリ、**ツールボックス**をクリックしてアクセスする**ツールボックス** タブの左側にある、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、選択**ツールバー**から、**ビュー**メニューのまたは CTRL + ALT + X)。  
  
 **FlowSwitch\<T >** からアクティビティ デザイナーをドラッグすることができます、**ツールボックス**ドロップ、[!INCLUDE[wfd2](../includes/wfd2-md.md)]内でサーフェスを**フローチャート**アクティビティ デザイナー。 使用して、**の種類を選択**種類を指定するを表示するウィンドウ (を使用したコードに関連付けられている、<xref:System.Activities.Statements.FlowSwitch%601>でそのジェネリック パラメーター) の評価から取得した、 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>。 この手順で作成、<xref:System.Activities.Statements.FlowSwitch%601>というラベルの付いたアクティビティ**スイッチ**内、<xref:System.Activities.Statements.Flowchart>アクティビティ。 <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>で入力することができます、**式**のボックス、**プロパティ**というヒント テキストが「VB の式を入力」を表示 ウィンドウをクリックします。  
  
 マウス、 **FlowSwitch\<T >** リンク アップに使用される四角形のハンドルが発生するアクティビティ デザイナー<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>が端に表示します。 ドラッグした後、 **FlowSwitch < T\>** アクティビティ デザイナーおよびその他のアクティビティ デザイナーを**フローチャート**、<xref:System.Activities.Activity>リンク オブジェクトを表す準備が整いました実行の順序を指定します。 いずれかを作成する、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>に関連付けられている、<xref:System.Activities.Statements.FlowSwitch%601>の周囲に四角形の case ハンドルのいずれかを**FlowSwitch\<T >** ハンドルのいずれかに (マウスのボタンを押しながら) をドラッグしますマウスがデザイナー上に置いたときに、接続先アクティビティに関する同様の方法で表示されるとします。 マウス ボタンをクリックし、矢印は、リリース、 **FlowSwitch\<T >** 接続先デザイナーへこの case を表すが表示されます。 このケースを矢印を表示しで編集することができますの既定値、**ケース**のボックス、**プロパティ**ウィンドウ。  
  
### <a name="the-flowswitcht-properties"></a>FlowSwitch\<T > のプロパティ  
 次の表に、<xref:System.Activities.Statements.FlowSwitch%601> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。  
  
|プロパティ名|必須|使用法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A>|True|実行パスのどの <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> に切り替えるかを決定するために評価される式を指定します。|  
|<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A>|False|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価によって得られる可能性のある結果から、<xref:System.Activities.Statements.FlowNode> オブジェクトのセットへの一意のマッピングを指定します。|  
|<xref:System.Activities.Statements.FlowSwitch%601.Default%2A>|True|<xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> の評価が、<xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> オブジェクトに含まれる値のいずれにも一致しない場合のマッピングを指定します。|  
  
## <a name="see-also"></a>関連項目  
 [フローチャート](../workflow-designer/flowchart-activity-designers.md)   
 [フローチャート](../workflow-designer/flowchart-activity-designer.md)   
 [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)