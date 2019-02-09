---
title: ワークフロー デザイナー - InitializeCorrelation アクティビティ デザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.InitializeCorrelation.UI
ms.assetid: 4c54f34c-ee84-42a6-abb0-ec260c1ccb76
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 496aefb2679edd87c892c54f44b14876b4ebce5b
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55953218"
---
# <a name="initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナー

**InitializeCorrelation**作成および構成するアクティビティ デザイナーが使用される、<xref:System.ServiceModel.Activities.InitializeCorrelation>アクティビティ。 <xref:System.ServiceModel.Activities.InitializeCorrelation>アクティビティが送信または受信する前に、メッセージ間の相関関係を確立します。

## <a name="the-initializecorrelation-activity"></a>InitializeCorrelation アクティビティ

<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを使用すると、メッセージが送受信されずに関連付けが初期化されます。 通常、関連付けはメッセージを送受信するときに初期化されます。 メッセージを送受信する前に関連付けを確立する必要がある場合は、<xref:System.ServiceModel.Activities.InitializeCorrelation> を使用して関連付けを初期化できます。

### <a name="using-the-initializecorrelation-activity-designer"></a>InitializeCorrelation アクティビティ デザイナーの使用

アクセス、 **InitializeCorrelation**内のアクティビティ デザイナー、**メッセージング**のカテゴリ、**ツールボックス**します。

**InitializeCorrelation**からアクティビティ デザイナーをドラッグすることができます、**ツールボックス**し、ワークフロー デザイナー画面にドロップします。 アクティビティ デザイナーをドロップを作成、 <xref:System.ServiceModel.Activities.InitializeCorrelation> 、既定値は、アクティビティ<xref:System.Activities.Activity.DisplayName%2A>InitializeCorrelation の。 <xref:System.Activities.Activity.DisplayName%2A>のヘッダーで編集できる、 **InitializeCorrelation**アクティビティ デザイナーまたは、 **DisplayName**のボックス、**プロパティ**ウィンドウ。

<xref:System.ServiceModel.Activities.CorrelationHandle>できますでを指定します、**相関**フィールドに**プロパティ**上のウィンドウ、 **InitializeCorrelation**アクティビティ デザイナー画面。

表示する、**関連付けの初期化**関連付けハンドルとそれを初期化するために使用するキー/値ペア横にある省略記号ボタンを選択を指定 ダイアログ ボックス、 **CorrelationData**フィールドに**プロパティ**ウィンドウ。 または、「表示…」ヒント テキストを選択、 **InitializeCorrelation**アクティビティ デザイナー画面。 このダイアログ ボックスの使用に関する詳細については、次を参照してください。、[型コレクション エディター ダイアログ ボックス](../workflow-designer/type-collection-editor-dialog-box.md)記事。

### <a name="the-initializecorrelation-properties"></a>InitializeCorrelation プロパティ

次の表は、<xref:System.ServiceModel.Activities.InitializeCorrelation>プロパティと、デザイナーでの使用方法について説明します。 これらのプロパティを編集できます**プロパティ**ウィンドウまたはワークフロー デザイナー画面。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの表示名。 既定値は InitializeCorrelation です。<br /><br /> ですが、わかりやすい既定以外の値の使用<xref:System.Activities.Activity.DisplayName%2A>は厳密に必要ありませんをお勧めします。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.Correlation%2A>|False|関連付け内のワークフロー アクティビティを関連付けるために使用される <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>|False|メッセージをワークフロー インスタンスに関連付ける、関連付けデータのディクショナリ。<br /><br /> 使用して、**関連付けの初期化**を構成するダイアログ ボックス、<xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A>します。 使用の詳細についてはこのダイアログ ボックスを参照してください、[型コレクション エディター ダイアログ ボックス](../workflow-designer/type-collection-editor-dialog-box.md)記事。|

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [Receive](../workflow-designer/receive-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)