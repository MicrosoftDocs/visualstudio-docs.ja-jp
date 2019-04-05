---
title: Pick アクティビティ デザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Pick.UI
ms.assetid: 642c0a47-1b47-45de-a19a-ca0606cedd7a
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7de5d9189906d72c96372acb1a361d315f973df6
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58977359"
---
# <a name="pick-activity-designer"></a>Pick アクティビティ デザイナー
<xref:System.Activities.Statements.Pick> アクティビティでは、イベント ベースの制御フローを提供します。 このアクティビティは、トリガー起動イベントに応答して、複数の分岐のいずれか 1 つを実行します。  
  
## <a name="the-pick-activity"></a>Pick アクティビティ  
 <xref:System.Activities.Statements.Pick> アクティビティには、<xref:System.Activities.Statements.PickBranch> オブジェクトのコレクションが含まれており、<xref:System.Activities.Statements.Pick> アクティビティはそのオブジェクトの 1 つを、トリガーの役割を果たす受信イベントに応答して実行できます。 このようにして、[!INCLUDE[wfd1](../includes/wfd1-md.md)]では、イベント ベースの制御フロー モデリングが提供されます。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。 <xref:System.Activities.Statements.Pick> アクティビティの実行の開始時に、<xref:System.Activities.Statements.PickBranch> 要素のすべてのトリガー アクティビティがスケジュールされます。 最初のアクティビティが完了すると、対応するアクション アクティビティがスケジュールされ、他のすべてのトリガー アクティビティは取り消されます。  
  
### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法  
 **選択**アクティビティ デザイナーが記載されて、**制御フロー**のカテゴリ、**ツールボックス**をクリックしてアクセスする、**ツールボックス**タブ[!INCLUDE[wfd2](../includes/wfd2-md.md)](または、選択**ツールバー**から、**ビュー**メニューまたは CTRL + ALT + X)。  
  
 **選択**からアクティビティ デザイナーをドラッグすることができます、**ツールボックス**ドロップ、[!INCLUDE[wfd2](../includes/wfd2-md.md)]サーフェス任意の場所のアクティビティ デザイナー通常配置している、内部の例については、 **シーケンス**アクティビティ デザイナー。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] にドロップすると、<xref:System.Activities.Statements.Pick> アクティビティが作成されます。このアクティビティには、既定で、Branch1 および Branch2 という表示名を持つ 2 つの空の <xref:System.Activities.Statements.PickBranch> アクティビティが要素として格納されます。 これらそれぞれ<xref:System.Activities.Statements.PickBranch.DisplayName%2A>でプロパティ値を編集できる、 **PickBranch**アクティビティ デザイナーのヘッダー内、または、**プロパティ**各分岐はウィンドウ。  
  
 追加する 2 つの方法はあります<xref:System.Activities.Statements.PickBranch>のコレクションにアクティビティを<xref:System.Activities.Statements.Pick>オブジェクト: ドラッグ アンド ドロップ、 **PickBranch**からデザイナー、**ツールボックス**からコンテキスト メニューを使用内で、**選択**デザイン サーフェイス。 詳細については、次を参照してください。、 [PickBranch](../workflow-designer/pickbranch-activity-designer.md)トピック。 内に配置できることのみいる項目に注意してください、**選択**アクティビティ デザイナーは、 **PickBranch**アクティビティ デザイナー。  
  
### <a name="pick-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Pick アクティビティのプロパティ  
 次の表に、<xref:System.Activities.Statements.Pick> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。  
  
|プロパティ名|必須|使用方法|  
|-------------------|--------------|-----------|  
|<xref:System.Activities.Activity.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.Pick> アクティビティ デザイナーの表示名を指定します。 既定値は Pick です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|  
  
## <a name="see-also"></a>関連項目  
 [制御フロー](../workflow-designer/control-flow-activity-designers.md)   
 [Pick アクティビティ](http://msdn.microsoft.com/library/b3e49b7f-0285-4720-8c09-11ae18f0d53e)   
 [Pick アクティビティの使用](http://msdn.microsoft.com/library/b89be812-a247-4025-b0e3-ffb20db027a6)