---
title: ReceiveAndSendReply テンプレート デザイナー
description: ワークフロー デザイナーで ReceiveAndSendReply テンプレートを使用して、事前構成済みの Receive アクティビティと SendReply アクティビティのペアを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.ReceiveAndSendReply.UI
- System.ServiceModel.Activities.SendReply.UI
ms.assetid: d1d9a058-df7e-48f5-a2e7-3caeeba7eaa6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6bc86aed1e135f369d771a9ac47513c4eb28ce25
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926533"
---
# <a name="receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナー

**ReceiveAndSendReply** テンプレートは、事前構成済みの <xref:System.ServiceModel.Activities.Receive> アクティビティと <xref:System.ServiceModel.Activities.SendReply> アクティビティのペアを作成するために使用されます。 これらのアクティビティは、<xref:System.Activities.Statements.Sequence> アクティビティの一部であり、サーバー上の要求/応答メッセージ交換パターンの一部として関連付けられています。

## <a name="the-receiveandsendreply-template"></a>ReceiveAndSendReply テンプレート

**ReceiveAndSendReply** テンプレートを追加すると、<xref:System.Activities.Statements.Sequence> アクティビティによる <xref:System.ServiceModel.Activities.Receive> アクティビティと <xref:System.ServiceModel.Activities.SendReply> アクティビティの作成に加え、次の 3 つの処理が実行されます。

- <xref:System.ServiceModel.Activities.Receive> アクティビティの <xref:System.ServiceModel.Activities.Receive.OperationName%2A> プロパティと <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> プロパティを構成する。

- <xref:System.ServiceModel.Activities.SendReply.Request%2A> アクティビティの <xref:System.ServiceModel.Activities.Receive> プロパティを <xref:System.ServiceModel.Activities.Send> アクティビティにバインドする。

- 親アクティビティに、変数として <xref:System.ServiceModel.Activities.CorrelationHandle> を作成する。

### <a name="use-the-receiveandsendreply-template-designer"></a>ReceiveAndSendReply テンプレート デザイナーを使用する

**[ツールボックス]** の **[メッセージング]** カテゴリで、**ReceiveAndSendReply** アクティビティ デザイナーにアクセスします。 **ReceiveAndSendReply** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面にドロップできます。 アクティビティ デザイナーをドロップすると、**Send** アクティビティ デザイナーを使用して構成できる <xref:System.ServiceModel.Activities.Receive> アクティビティと、SendReplyToReceive デザイナーを使用して構成できる、関連性のある <xref:System.ServiceModel.Activities.SendReply> を構成できます。

**Receive** デザイナーを使用して <xref:System.ServiceModel.Activities.Receive> アクティビティを構成する方法の詳細については、「[Receive アクティビティ デザイナー](../workflow-designer/receive-activity-designer.md)」を参照してください。

### <a name="properties-of-sendreply"></a>SendReply のプロパティ

次の表に、<xref:System.ServiceModel.Activities.SendReply> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティはプロパティ グリッドで編集でき、一部はワークフロー デザイナー画面で編集できます。

| プロパティ名 | 必須 | 使用方法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | いいえ | <xref:System.ServiceModel.Activities.SendReply> アクティビティの省略可能な表示名。 既定値は SendReplyToReceive です。<br /><br /> 既定値以外のフレンドリー <xref:System.Activities.Activity.DisplayName%2A> の使用は厳密には必須ではありませんが、そのような値を使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.SendReply.Request%2A> | はい | この <xref:System.ServiceModel.Activities.Receive> アクティビティと関連付けられる <xref:System.ServiceModel.Activities.SendReply> アクティビティへの参照。 このプロパティを **null** にすることはできません。 <xref:System.ServiceModel.Activities.Receive> アクティビティと <xref:System.ServiceModel.Activities.SendReply> アクティビティは、要求/応答メッセージング パターンをモデル化するためにサーバーで一緒に使用されます。 このプロパティでは、関連付ける <xref:System.ServiceModel.Activities.Send> アクティビティを指定します。 このプロパティは <xref:System.ServiceModel.Activities.SendReply> アクティビティの作成元である <xref:System.ServiceModel.Activities.Send> アクティビティに自動的にバインドされるため、デザイナーで編集することはできません。 |
| <xref:System.ServiceModel.Activities.SendReply.Content%2A> | いいえ | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドで **[コンテンツ]** フィールドの横にある省略記号ボタンをクリックするか、**Receive** アクティビティ デザイナー画面で **[コンテンツ]** というラベルの横にある **[定義]** ボタンをクリックします。 どちらの場合も、 **[コンテンツ定義]** ダイアログ ボックスが表示されます。 このボックスの使用方法の詳細については、「[[コンテンツ定義] ダイアログ ボックス](../workflow-designer/content-definition-dialog-box.md)」トピックを参照してください。 |
| <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> | いいえ | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティ グリッドで <xref:System.ServiceModel.Activities.SendReply.CorrelationInitializers%2A> プロパティの横にある省略記号ボタンをクリックすると、 **[関連付け初期化子の追加]** ダイアログ ボックスが開きます。 このボックスの使用方法の詳細については、「[[関連付け初期化子の追加] ダイアログ ボックス](../workflow-designer/add-correlationinitializers-dialog-box.md)」トピックを参照してください。 |
| <xref:System.ServiceModel.Activities.SendReply.Action%2A> | いいえ | メッセージのアクション ヘッダーを指定します。 これを明示的に設定しない場合は、次の既定値が設定されます。<br /><br /> `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}` |
| <xref:System.ServiceModel.Activities.SendReply.PersistBeforeSend%2A> | いいえ | 応答メッセージを送信する前にワークフロー サービス インスタンスを永続化するかどうかを指定します。 既定値は **false** です。 |

## <a name="see-also"></a>関連項目

- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [受信](../workflow-designer/receive-activity-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)