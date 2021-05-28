---
title: InitializeCorrelation アクティビティ デザイナー
description: ワークフロー デザイナーで、InitializeCorrelation アクティビティ デザイナーを使用して InitializeCorrelation アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9591ef604fcf9374e9aa498e74c5a7761459589f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959793"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナー

**InitializeCorrelation** アクティビティ デザイナーは、<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを作成および構成するために使用します。 <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティは、メッセージを送信または受信する前に、メッセージ間の相関関係を確立します。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation アクティビティ

<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを使用すると、メッセージが送受信されずに関連付けが初期化されます。 通常、関連付けはメッセージを送受信するときに初期化されます。 メッセージを送受信する前に関連付けを確立する必要がある場合は、<xref:System.ServiceModel.Activities.InitializeCorrelation> を使用して関連付けを初期化できます。

### <a name="using-the-initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナーの使用

**[ツールボックス]** の **[メッセージング]** カテゴリで、**InitializeCorrelation** アクティビティ デザイナーにアクセスします。

**InitializeCorrelation** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、ワークフロー デザイナー画面にドロップできます。 アクティビティ デザイナーをドロップすると、InitializeCorrelation の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**InitializeCorrelation** アクティビティ デザイナーのヘッダー、または **[プロパティ]** ウィンドウの **[DisplayName]** ボックスで編集できます。

<xref:System.ServiceModel.Activities.CorrelationHandle> は、**InitializeCorrelation** アクティビティ デザイナー画面の **[プロパティ]** ウィンドウの **[関連付け]** フィールドで指定できます。

関連付けハンドルとその初期化に使用されるキーと値のペアを指定できる **[関連付けの初期化]** ダイアログ ボックスを表示するには、 **[プロパティ]** ウィンドウの **[CorrelationData]** フィールドの横にある省略記号ボタンを選択します。 または、**InitializeCorrelation** アクティビティ デザイナー画面の [表示 ...] ヒントテキストを選択します。 このダイアログ ボックスの使用方法の詳細については、「[[型コレクション エディター] ダイアログ ボックス](../workflow-designer/type-collection-editor-dialog-box.md)」を参照してください。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation プロパティ

次の表に、<xref:System.ServiceModel.Activities.InitializeCorrelation> のプロパティと、それらがデザイナーでどのように使用されるかを示します。 これらのプロパティは、 **[プロパティ]** ウィンドウまたはワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの表示名。 既定値は InitializeCorrelation です。<br /><br /> 既定値以外のフレンドリー <xref:System.Activities.Activity.DisplayName%2A> の使用は厳密には必須ではありませんが、使用することをお勧めします。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|いいえ|関連付け内のワークフロー アクティビティを関連付けるために使用される <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|いいえ|メッセージをワークフロー インスタンスに関連付ける、関連付けデータのディクショナリ。<br /><br /> <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> を構成するには **[関連付け初期化]** ダイアログ ボックスを使用します。 このダイアログ ボックスの使用方法の詳細については、「[[型コレクション エディター] ダイアログ ボックス](../workflow-designer/type-collection-editor-dialog-box.md)」を参照してください。|

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [受信](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)