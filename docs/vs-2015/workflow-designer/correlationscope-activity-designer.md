---
title: CorrelationScope アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.CorrelationScope.UI
ms.assetid: 75f20664-9042-464d-8e2b-148d365a2286
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b6ffcfd63d60ab6f085b5cb2a793e8bf17a50d8e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656912"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope アクティビティ デザイナー
**Correlationscope**アクティビティデザイナーは、<xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを使用して、子メッセージングアクティビティを暗黙的に管理する <xref:System.ServiceModel.Activities.CorrelationScope> アクティビティを作成および構成するために使用します。

## <a name="the-correlationscope-activity"></a>CorrelationScope アクティビティ
 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> プロパティでは、子メッセージング アクティビティの管理に使用する <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。 <xref:System.ServiceModel.Activities.Send> に含まれる <xref:System.ServiceModel.Activities.Receive> アクティビティおよび <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> アクティビティは、親 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> アクティビティの <xref:System.ServiceModel.Activities.CorrelationScope> プロパティを使用して関連付けを行うように構成されます。

### <a name="using-the-correlationscope-activity-designer"></a>CorrelationScope アクティビティ デザイナーの使用
 **Correlationscope**アクティビティデザイナーは **、[** **ツールボックス**] の **[メッセージング]** カテゴリにあります。これにアクセスするには、[!INCLUDE[wfd2](../includes/wfd2-md.md)] の左側にある **[ツールボックス]** タブをクリックします (または、 **[表示]** メニュー、または CTRL + ALT + X キー)

 **Correlationscope**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、[!INCLUDE[wfd2](../includes/wfd2-md.md)] 画面にドロップできます。 これにより、CorrelationScope という既定の**DisplayName**を持つ <xref:System.ServiceModel.Activities.CorrelationScope> アクティビティが作成されます。 @No__t_0 は、 **Correlationscope**アクティビティデザイナーのヘッダー、または **[プロパティ]** ウィンドウの **[DisplayName]** ボックスで編集できます。

 子メッセージングアクティビティによって使用される <xref:System.ServiceModel.Activities.CorrelationHandle> を指定するには、 **[プロパティ]** ウィンドウの **[CorrelatesWith]** フィールドの横にある省略記号ボタンをクリックして、 **[式エディター]** ダイアログボックスを表示します。 このプロパティは、アクティビティ デザイナー画面で設定することもできます。

 関連付けに含まれるアクティビティは、 **Correlationscope**デザイナー内の **[本文]** ボックス内のデザイナーを削除することによって指定します。

### <a name="the-correlationscope-properties"></a>CorrelationScope プロパティ
 次の表に、<xref:System.ServiceModel.Activities.CorrelationScope> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、 **[プロパティ]** ウィンドウまたは [!INCLUDE[wfd2](../includes/wfd2-md.md)] デザイナー画面で編集できます。また、多くの場合、両方で編集できます。

|プロパティ名|必要|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの省略可能な表示名。|
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|False|子メッセージング アクティビティの管理に使用する <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。 このプロパティを設定しない場合は、<xref:System.ServiceModel.Activities.CorrelationScope> に、暗黙の <xref:System.ServiceModel.Activities.CorrelationHandle> が自動的に作成されます。|
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|False|相関関係のスコープ内のアクティビティを指定します。|

## <a name="see-also"></a>参照
 [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) [Receive](../workflow-designer/receive-activity-designer.md) [receiveandsendreply](../workflow-designer/receiveandsendreply-template-designer.md) [Send](../workflow-designer/send-activity-designer.md) [sendandreceivereply](../workflow-designer/sendandreceivereply-template-designer.md) [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)