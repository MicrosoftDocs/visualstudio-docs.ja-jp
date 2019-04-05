---
title: メッセージング アクティビティ デザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 897e63cf-a42f-4edd-876f-c4ccfffaf6d6
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 250b213fc3bc54d67f55d41c5eb3aba7e3488cd4
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975074"
---
# <a name="messaging-activity-designers"></a>メッセージング アクティビティ デザイナー
Messaging アクティビティ デザイナーは、[!INCLUDE[indigo1](../includes/indigo1-md.md)] アプリケーション内から [!INCLUDE[wf](../includes/wf-md.md)] メッセージを送受信するメッセージング アクティビティを作成および構成するために使用します。 [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)] には、5 つのメッセージング アクティビティが導入され、[!INCLUDE[wfd1](../includes/wfd1-md.md)]には、ワークフロー内でメッセージングを管理できるようにする 2 つの新しいテンプレート デザイナーが用意されています。 次の表に示す、このセクションに含まれるトピックでは、[!INCLUDE[wfd2](../includes/wfd2-md.md)]のアクティビティ デザイナーおよびテンプレート デザイナーの使用方法についてのガイドラインを示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|メッセージ アクティビティ|説明|  
|----------------------|-----------------|  
|[CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)|<xref:System.ServiceModel.Activities.CorrelationScope> オブジェクトを使用して、子メッセージング アクティビティを暗黙で管理する <xref:System.ServiceModel.Activities.CorrelationHandle> アクティビティを作成および構成します。|  
|[InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)|メッセージを送受信せずに関連付けを初期化するために使用する <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを作成および構成します。|  
|[Receive](../workflow-designer/receive-activity-designer.md)|サービスからメッセージを受信する <xref:System.ServiceModel.Activities.Receive> アクティビティを作成および構成します。|  
|[ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)|<xref:System.ServiceModel.Activities.Send> アクティビティ内に、定義済みの <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティと <xref:System.Activities.Statements.Sequence> アクティビティのペアを作成します。|  
|[Send](../workflow-designer/send-activity-designer.md)|サービスにメッセージを送信する <xref:System.ServiceModel.Activities.Send> アクティビティを作成および構成します。|  
|[SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)|<xref:System.ServiceModel.Activities.Receive> アクティビティ内に、定義済みの <xref:System.ServiceModel.Activities.SendReply> アクティビティと <xref:System.Activities.Statements.Sequence> アクティビティのペアを作成します。|  
|[TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)|ワークフローへのトランザクションのフローを可能にする <xref:System.ServiceModel.Activities.TransactedReceiveScope> アクティビティを作成および構成します。|  
  
## <a name="reference"></a>参照  
 <xref:System.Activities.Activity>  
  
 <xref:System.ServiceModel.Activities.CorrelationScope>  
  
 <xref:System.ServiceModel.Activities.Receive>  
  
 <xref:System.ServiceModel.Activities.Send>  
  
 <xref:System.ServiceModel.Activities.ReceiveReply>  
  
 <xref:System.ServiceModel.Activities.SendReply>  
  
 <xref:System.ServiceModel.Activities.TransactedReceiveScope>  
  
## <a name="related-sections"></a>関連項目  
 他の種類のアクティビティ デザイナーについては、次のトピックを参照してください。  
  
 [制御フロー](../workflow-designer/control-flow-activity-designers.md)  
  
 [アクティビティ デザイナーの使用](../workflow-designer/using-the-activity-designers.md)  
  
 [フローチャート](../workflow-designer/flowchart-activity-designers.md)  
  
 [ランタイム](../workflow-designer/runtime-activity-designers.md)  
  
 [Primitives](../workflow-designer/primitives-activity-designers.md)  
  
 [トランザクション](../workflow-designer/transaction-activity-designers.md)  
  
 [コレクション](../workflow-designer/collection-activity-designers.md)  
  
 [エラー処理](../workflow-designer/error-handling-activity-designers.md)  
  
## <a name="external-resources"></a>外部リソース  
 [アクティビティ デザイナーの使用](../workflow-designer/using-the-activity-designers.md)