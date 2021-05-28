---
title: ワークフロー デザイナー - CorrelationScope アクティビティ デザイナー
description: CorrelationScope アクティビティ デザイナーを使用して、CorrelationScope アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.CorrelationScope.UI
ms.assetid: 75f20664-9042-464d-8e2b-148d365a2286
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e9edd755465cf812c1572c62f1c6335fc5295281
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955523"
---
# <a name="correlationscope-activity-designer"></a>CorrelationScope アクティビティ デザイナー

**CorrelationScope** アクティビティ デザイナーは、<xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを使用して、子メッセージング アクティビティを暗黙で管理する <xref:System.ServiceModel.Activities.CorrelationScope> アクティビティを作成および構成するために使用します。

## <a name="the-correlationscope-activity"></a>CorrelationScope アクティビティ

<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> プロパティでは、子メッセージング アクティビティの管理に使用する <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。 <xref:System.ServiceModel.Activities.Send> に含まれる <xref:System.ServiceModel.Activities.Receive> アクティビティおよび <xref:System.ServiceModel.Activities.CorrelationScope.Body%2A> アクティビティは、親 <xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A> アクティビティの <xref:System.ServiceModel.Activities.CorrelationScope> プロパティを使用して関連付けを行うように構成されます。

### <a name="use-the-correlationscope-activity-designer"></a>CorrelationScope アクティビティ デザイナーを使用する

**CorrelationScope** アクティビティ デザイナーは、 **[ツールボックス]** の **[メッセージング]** カテゴリにあります。ワークフロー デザイナーの左側にある **[ツールボックス]** タブをクリックすることでアクセスします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** + **Alt**+ **X** キーを押します。

**CorrelationScope** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、ワークフロー デザイナー画面にドロップできます。 これにより、CorrelationScope の既定の **DisplayName** を持つ <xref:System.ServiceModel.Activities.CorrelationScope> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> 値は、**CorrelationScope** アクティビティ デザイナーのヘッダーまたは **[プロパティ]** ウィンドウの **[DisplayName]** ボックスで編集できます。

子メッセージング アクティビティで使用される <xref:System.ServiceModel.Activities.CorrelationHandle> を指定するには、 **[プロパティ]** ウィンドウの **[CorrelatesWith]** フィールドの横にある省略記号ボタンをクリックして、 **[式エディター]** ダイアログ ボックスを表示します。 このプロパティは、アクティビティ デザイナー画面で設定することもできます。

相関関係内にスコープ設定されるアクティビティは、対応するデザイナーを、**CorrelationScope** デザイナーの **[Body]** ボックス内にドラッグすることで指定します。

### <a name="the-correlationscope-properties"></a>CorrelationScope プロパティ

次の表に、<xref:System.ServiceModel.Activities.CorrelationScope> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、 **[プロパティ]** ウィンドウ、またはワークフロー デザイナー画面で編集できます。多くの場合は、どちらでも編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの省略可能な表示名。|
|<xref:System.ServiceModel.Activities.CorrelationScope.CorrelatesWith%2A>|いいえ|子メッセージング アクティビティの管理に使用する <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。 このプロパティを設定しない場合は、<xref:System.ServiceModel.Activities.CorrelationScope> に、暗黙の <xref:System.ServiceModel.Activities.CorrelationHandle> が自動的に作成されます。|
|<xref:System.ServiceModel.Activities.CorrelationScope.Body%2A>|いいえ|相関関係のスコープ内のアクティビティを指定します。|

## <a name="see-also"></a>関連項目

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受信](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)