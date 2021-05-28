---
title: '[関連付け初期化子の追加] ダイアログ ボックス'
description: ワークフロー デザイナーの [関連付け初期化子の追加] ダイアログ ボックスを使用して、Send、Receive、および SendReply アクティビティの CorrelationInitializers プロパティを構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AddCorrelationInitializers.UI
ms.assetid: c0517467-d54a-4ee6-aef0-c19b96b6f395
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ca78cea409f559583507fd4b5b7c9fc43f9a5ffc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99963732"
---
# <a name="add-correlationinitializers-dialog-box"></a>[関連付け初期化子の追加] ダイアログ ボックス

**[関連付け初期化子の追加]** ダイアログ ボックスは、ワークフロー デザイナー内で <xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.SendReply>、および <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティの **CorrelationInitializers** プロパティを構成するために使用されます。 このボックスを使用するアクティビティ デザイナーの詳細については、[Send](../workflow-designer/send-activity-designer.md)、[Receive](../workflow-designer/receive-activity-designer.md)、[ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)、および [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md) の各トピックを参照してください。

このダイアログ ボックスで指定したコレクションの関連付け初期化子では、メッセージング アクティビティ間の次の相関関係を初期化できます。

- クエリベース
- context
- コールバック コンテキスト
- 要求/応答

次の表に、 **[関連付け初期化子の追加]** ダイアログ ボックスのユーザー インターフェイス (UI) 要素を示します。

|UI 要素|説明|
|-|-----------------|
|**初期化子の追加**|初期化子をコレクションに追加するには、 **[初期化子の追加]** ボックスをクリックします。|
|**[関連付けの種類]**|関連付け初期化子の種類を指定します。 次の 4 種類から選択できます。<br /><br /> 1. <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> を指定するためのコールバック関連付け初期化子。<br />2. <xref:System.ServiceModel.Activities.CorrelationInitializer> を指定するためのコンテキスト関連付け初期化子。<br />3. <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> を指定するための要求/応答関連付け初期化子。<br />4. <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> を指定するためのクエリ関連付け初期化子。<br /><br /> **CorrelationType** を編集するには<br /><br /> 1. **[初期化子の追加]** DataGrid の特定の行にタブ移動します。<br />2. **CorrelationTypeComboBox** にフォーカスを設定するには、**Ctrl** + **Tab** を押します。<br />3. Alt キーを押しながら下方向キーを押して **ComboBox** をポップアップ表示して編集します。|
|**XPath クエリ**|送受信メッセージから相関関係データを抽出するためのクエリを含む、キーと値のペア。 このリストは、<xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 型を使用している場合にのみ有効です。|

## <a name="to-launch-the-add-correlation-initializers-dialog-box"></a>[関連付け初期化子の追加] ダイアログ ボックスを開くには

 **[関連付け初期化子の追加]** ダイアログ ボックスは、**Send**、**Receive**、**ReceiveAndSendReply**、および **SendAndReceiveReply** の各デザイナーで使用されます。 それらにアクセスする方法は、どの場合も同様です。ここでは、**Receive** デザイナーを使用する例で手順を説明します。

 **Receive** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面にドロップできます。 **Receive** アクティビティ デザイナーをドロップすると、Receive の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.ServiceModel.Activities.Receive> アクティビティが作成されます。 **Receive** アクティビティ デザイナーを選択し、プロパティ グリッドで **CorrelationInitializers** プロパティの (コレクション) というテキストの横にある省略記号ボタンをクリックして、 **[関連付け初期化子の追加]** ダイアログ ボックスを表示します。

## <a name="see-also"></a>関連項目

- [[関連付け初期化] ダイアログ ボックス](../workflow-designer/initialize-correlation-dialog-box.md)
