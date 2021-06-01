---
title: ワークフロー デザイナー - Receive アクティビティ デザイナー
description: Receive アクティビティと、Receive アクティビティ デザイナーを使用して Receive アクティビティを作成し、構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Receive.UI
ms.assetid: f58d3c70-944d-4bb4-90a7-e68c103caddc
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ceff7d40ffd0d7c961f07dd65a8070a8f11a1b4b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899376"
---
# <a name="receive-activity-designer"></a>Receive アクティビティ デザイナー

**Receive** アクティビティ デザイナーは、<xref:System.ServiceModel.Activities.Receive> アクティビティを作成および構成するために使用します。 <xref:System.ServiceModel.Activities.Receive> アクティビティは、メッセージ (<xref:System.ServiceModel.Channels.Message>、<xref:System.IO.Stream>、<xref:System.Xml.Linq.XElement> などの組み込みの型、アプリケーション定義のデータ コントラクト、メッセージ コントラクト、またはシリアル化可能な XML クラス) を受信するアクティビティです。

## <a name="the-receive-activity"></a>Receive アクティビティ

<xref:System.ServiceModel.Activities.Receive> アクティビティでは、使用されている受信コンテンツの型に応じて、単一または複数のアイテムを受信できます。 <xref:System.ServiceModel.Activities.SendReply> アクティビティは、サービスでの要求/応答メッセージ交換パターンの一部としてメッセージを受信する <xref:System.ServiceModel.Activities.Receive> アクティビティにバインドできます。

### <a name="using-the-receive-activity-designer"></a>Receive アクティビティ デザイナーの使用

**[ツールボックス]** の **[メッセージング]** カテゴリで、**Receive** アクティビティ デザイナーにアクセスします。 **Receive** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面にドロップできます。 この操作により、Receive という既定の <xref:System.ServiceModel.Activities.Receive> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**Receive** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

<xref:System.ServiceModel.Activities.SendReply> アクティビティを作成し、選択した <xref:System.ServiceModel.Activities.Receive> アクティビティにバインドするには、**Receive** アクティビティ デザイナーを右クリックし、コンテキスト メニューの **[SendReply の作成]** をクリックします。これで、**Receive** デザイナーの下に **SendReplyToReceive** デザイナーが表示されます。 <xref:System.ServiceModel.Activities.SendReply> アクティビティは、サービスでの要求/応答メッセージ交換パターンの一部として応答メッセージを送信するアクティビティであり、 **SendReplyToReceive** デザイナーで構成できます。

また、 **[ツールボックス]** の **[メッセージング]** カテゴリの **ReceiveAndSendReply** テンプレート デザイナーを使用して、構成済みの <xref:System.ServiceModel.Activities.Receive> アクティビティと <xref:System.ServiceModel.Activities.SendReply> アクティビティのペアを作成できます。 **ReceiveAndSendReply** と **SendReplyToReceive** テンプレートの使用の詳細については、[ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md) に関するトピックを参照してください。

### <a name="the-receive-activity-properties"></a>Receive アクティビティのプロパティ

次の表に、<xref:System.ServiceModel.Activities.Receive> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはワークフロー デザイナー画面で編集できます。 必須のプロパティは <xref:System.ServiceModel.Activities.Receive.OperationName%2A> プロパティのみです。

| プロパティ名 | 必須 | 使用方法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | いいえ | <xref:System.ServiceModel.Activities.Receive> アクティビティの表示名を指定します。 既定値は Receive です。<br /><br /> 既定値以外の <xref:System.Activities.Activity.DisplayName%2A> の使用は必須ではありませんが、使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.Receive.OperationName%2A> | はい | この <xref:System.ServiceModel.Activities.Receive> アクティビティによって実装されるサービス操作の名前を指定します。 このプロパティは、**Action** プロパティが明示的に設定されていない場合に、**Action** プロパティの既定値を構成するために使用します。 |
| <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> | いいえ | サービス コントラクトの名前を指定します。 このプロパティは、サービス操作を個々のサービス コントラクトにグループ化するために使用します。 同じ <xref:System.ServiceModel.Activities.Receive> を持つすべての <xref:System.ServiceModel.Activities.Receive.ServiceContractName%2A> アクティビティは、同じサービス コントラクト (WSDL ポートの種類) にグループ化されます。 既定値は、トップ レベル (ルート) アクティビティの完全修飾 CLR 名です。 |
| <xref:System.ServiceModel.Activities.Receive.Content%2A> | いいえ | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドで **[Content]** フィールドの横にある省略記号ボタンを選択するか、**Receive** アクティビティ デザイナー画面で **[コンテンツ]** というラベルの横にある **[定義]** ボタンをクリックします。 どちらの場合も、 **[コンテンツ定義]** ダイアログ ボックスが表示されます。 このボックスの使用方法の詳細については、「[[コンテンツ定義] ダイアログ ボックス](../workflow-designer/content-definition-dialog-box.md)」トピックを参照してください。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> | いいえ | <xref:System.ServiceModel.Activities.Receive> オブジェクトを持つワークフローのサービス操作における <xref:System.ServiceModel.MessageQuerySet> アクティビティ間の相関関係を指定します。 プロパティ グリッドで <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> プロパティの横にある省略記号ボタンをクリックすると、 **[CorrelatesOn の定義]** ダイアログ ボックスが開きます。 このダイアログ ボックスの使用の詳細については、「[[コンテンツ定義] ダイアログ ボックス](../workflow-designer/content-definition-dialog-box.md)」トピックを参照してください。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> | いいえ | 適切なワークフロー インスタンスにメッセージをルーティングするために使用される <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。<br /><br /> プロパティ グリッドで <xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> プロパティの横にある省略記号ボタンをクリックすると、 **[式エディター]** ダイアログ ボックスが開きます。 このダイアログ ボックスの使用方法の詳細については、「[方法: 式エディターを使用する](../workflow-designer/how-to-use-the-expression-editor.md)」を参照してください。 |
| <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> | いいえ | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Receive> オブジェクトのコレクションを指定します。 プロパティ グリッドで <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> プロパティの横にある省略記号ボタンをクリックすると、 **[関連付け初期化子の追加]** ダイアログ ボックスが開きます。 このボックスの使用方法の詳細については、「[[関連付け初期化子の追加] ダイアログ ボックス](../workflow-designer/add-correlationinitializers-dialog-box.md)」トピックを参照してください。 |
| <xref:System.ServiceModel.Activities.Receive.CanCreateInstance%2A> | いいえ | メッセージが既存のワークフロー インスタンスと関連付けられていない場合に、新しいワークフロー インスタンスを作成して、このメッセージを処理するかどうかを決定する値を指定します。 この値を **true**, に設定すると、メッセージが既存のワークフロー インスタンスと関連付けられていない場合は、新しいワークフロー インスタンスを作成して、このメッセージを処理します。 |
| <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> | いいえ | この <xref:System.ServiceModel.Activities.Receive> アクティビティによって実装されるサービス操作の既知の型のコレクションを指定します。 このプロパティは、<xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> に設定された <xref:System.Runtime.Serialization.DataContractSerializer> プロパティと共に使用する必要があり、 <xref:System.Xml.Serialization.XmlSerializer> が使用されている場合は無視されます。<br /><br /> プロパティ グリッドで **[KnownTypes]** フィールドの横にある省略記号ボタンを選択して、 **[型コレクション エディター]** ダイアログ ボックスを開きます。このダイアログで、該当する型を追加できます。 このボックスの使用方法の詳細については、「[[型コレクション エディター] ダイアログ ボックス](../workflow-designer/type-collection-editor-dialog-box.md)」を参照してください。 |
| <xref:System.ServiceModel.Activities.Receive.ProtectionLevel%2A> | いいえ | メッセージの <xref:System.Net.Security.ProtectionLevel> を指定します。<br /><br /> 1. <xref:System.Net.Security.ProtectionLevel> は、認証のみを意味します。<br />2. <xref:System.Net.Security.ProtectionLevel> は、送信されるデータの整合性の確保に役立つ署名データを意味します。<br />3. <xref:System.Net.Security.ProtectionLevel> は、送信されるデータの機密性と整合性の確保に役立つ暗号化と署名データを意味します。 |
| <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> | いいえ | <xref:System.ServiceModel.Activities.Receive> アクティビティによって実装されるサービス操作に使用するシリアライザーの型を指定します。 既定値は <xref:System.Runtime.Serialization.DataContractSerializer> です。この場合、ある型のインスタンスが、提供されたデータ コントラクトを使用する XML ストリームまたはドキュメントへとシリアル化または逆シリアル化されます。 XML をより厳密に制御する必要がある場合は、<xref:System.Xml.Serialization.XmlSerializer> も使用できます。 |
| <xref:System.ServiceModel.Activities.Receive.Action%2A> | いいえ | メッセージのアクション ヘッダーを指定します。 これを明示的に設定しない場合は、次の既定値が設定されます: `https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`。 |

## <a name="see-also"></a>関連項目

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [Send](../workflow-designer/send-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)
