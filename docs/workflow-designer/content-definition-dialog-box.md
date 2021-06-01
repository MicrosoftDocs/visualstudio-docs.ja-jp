---
title: ワークフロー デザイナー - [コンテンツ定義] ダイアログ ボックス
description: '[コンテンツ定義] ダイアログ ボックスを使用して、Send、Receive、SendReply、および ReceiveReply の各アクティビティのコンテンツ プロパティを構成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MessageContent.UI
ms.assetid: 7e4237c3-90a1-4149-bd8a-3643d1dde0df
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a25d049b17381c49bfa1b4a5544972b6dc5fe499
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955646"
---
# <a name="content-definition-dialog-box"></a>[コンテンツ定義] ダイアログ ボックス

**[コンテンツ定義]** ダイアログ ボックスは、ワークフロー デザイナーで <xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.SendReply>、および <xref:System.ServiceModel.Activities.ReceiveReply> の各アクティビティの **コンテンツ** のプロパティを構成するために使用されます。 このボックスを使用するアクティビティ デザイナーの詳細については、[Send](../workflow-designer/send-activity-designer.md)、[Receive](../workflow-designer/receive-activity-designer.md)、[ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)、および [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) の各トピックを参照してください。

次の表に、 **[関連付けの初期化]** ダイアログ ボックスのユーザー インターフェイス (UI) 要素を示します。

|UI 要素|説明|
|-|-----------------|
|**メッセージ**|**[メッセージ データ]** 式テキスト ボックスでメッセージの内容を指定し、 **[メッセージの種類]** ドロップダウン リスト ボックスを使用して種類を指定します。 **[コンテンツ定義]** では、既定で、ワークフロー サービス定義内の <xref:System.ServiceModel.Channels.Message> またはメッセージ コントラクト型を受け取る <xref:System.ServiceModel.Activities.ReceiveMessageContent> が使用されます。|
|**パラメーター**|データ コントラクトを受け取る <xref:System.ServiceModel.Activities.ReceiveParametersContent> を使用するには、 **[パラメーター]** オプション ボタンをクリックします。 <xref:System.Activities.OutArgument> キーおよび値のペアのジェネリック コレクションを設定するには、データ グリッドを使用します。これらの値は、現在のワークフローの変数パラメーターに割り当てられます。|

**[コンテンツ定義]** ダイアログ ボックスは、**Send**、**Receive**、**ReceiveAndSendReply**、および **SendAndReceiveReply** の各デザイナーで使用されます。 デザイナーへのアクセス方法は、どの場合も同様です。ここでは、Receive デザイナーを使用する例で手順を説明します。

**Receive** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面にドロップできます。 この操作により、Receive という既定の <xref:System.ServiceModel.Activities.Receive> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 **Receive** アクティビティ デザイナーを選択し、プロパティ グリッドで **Content** プロパティの (コンテンツ) というテキストの横にある省略記号ボタンをクリックして、 **[コンテンツ定義]** ダイアログ ボックスを表示します。

コンテンツは、<xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティの **[メッセージ]** セクション内、または <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティの **[パラメーター]** セクション内で指定できます。

## <a name="see-also"></a>関連項目

- [ワークフロー デザイナーの UI ヘルプ](browse-and-select-a-dotnet-type-dialog-box.md)