---
title: InitializeCorrelation アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 145b67574169696771f4102b29e9dc8f6a9d1575
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659022"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナー
**InitializeCorrelation**アクティビティデザイナーは、メッセージを送信または受信する前に、メッセージ間の相関関係を確立するために使用される <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを作成および構成するために使用します。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation アクティビティ
 <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを使用すると、メッセージが送受信されずに関連付けが初期化されます。 通常、関連付けはメッセージを送受信するときに初期化されます。 メッセージを送受信する前に関連付けを確立する必要がある場合は、<xref:System.ServiceModel.Activities.InitializeCorrelation> を使用して関連付けを初期化できます。

### <a name="using-the-initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナーの使用
 **InitializeCorrelation**アクティビティデザイナーは、[**ツールボックス]** の **[メッセージング]** カテゴリにあります。これにアクセスするには、[!INCLUDE[wfd2](../includes/wfd2-md.md)] の **[ツールボックス]** タブをクリックします (または、ビューから **[ツールバー]** を選択します)。メニューまたは CTRL + ALT + X)

 **InitializeCorrelation**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして [!INCLUDE[wfd2](../includes/wfd2-md.md)] 画面にドロップできます。 これにより、既定の <xref:System.Activities.Activity.DisplayName%2A> InitializeCorrelation を持つ <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、 **InitializeCorrelation**アクティビティデザイナーのヘッダー、または **[プロパティ]** ウィンドウの **[DisplayName]** ボックスで編集できます。

 @No__t_0 は、 **InitializeCorrelation**アクティビティデザイナー画面の **[プロパティ]** ウィンドウの **[関連付け]** フィールドで指定できます。

 **[プロパティ]** ウィンドウまたは 表示... の  **[correlationdata]** フィールドの他の省略記号ボタンをクリックします。 **InitializeCorrelation**アクティビティデザイナー画面のヒントテキストには、 **[関連付けの初期化]** ダイアログボックスが表示されます。このダイアログボックスでは、関連付けハンドルと、それを初期化するために使用されるキーと値のペアを指定できます。 このダイアログボックスを使用する [!INCLUDE[crabout](../includes/crabout-md.md)] については、「[[型コレクションエディター] ダイアログボックス](../workflow-designer/type-collection-editor-dialog-box.md)」を参照してください。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation プロパティ
 次の表に、<xref:System.ServiceModel.Activities.InitializeCorrelation> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、 **[プロパティ]** ウィンドウまたは [!INCLUDE[wfd2](../includes/wfd2-md.md)] 画面で編集できます。

|プロパティ名|必要|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの表示名。 既定値は InitializeCorrelation です。<br /><br /> 既定値以外の <xref:System.Activities.Activity.DisplayName%2A> の使用は必須ではありませんが、使用することをお勧めします。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|関連付け内のワークフロー アクティビティを関連付けるために使用される <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|メッセージをワークフロー インスタンスに関連付ける、関連付けデータのディクショナリ。<br /><br /> **[関連付けの初期化]** ダイアログボックスを使用すると、<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> を構成できます。 [!INCLUDE[crabout](../includes/crabout-md.md)] このダイアログボックスを使用するには、[[型コレクションエディター] ダイアログボックス](../workflow-designer/type-collection-editor-dialog-box.md)のトピックを参照してください。|

## <a name="see-also"></a>参照
 [Correlationscope](../workflow-designer/correlationscope-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md) [Send](../workflow-designer/send-activity-designer.md) [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)