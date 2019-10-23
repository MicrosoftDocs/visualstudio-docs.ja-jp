---
title: 従来のワークフロー活動 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- workflows, activities
- activities
- workflow activities
ms.assetid: 4af7a06b-1e82-43c8-aec8-0dc5fb63d08a
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f4f1110424aefc1771c0dc7600fb9996bff0e892
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658940"
---
# <a name="legacy-workflow-activities"></a>従来のワークフロー アクティビティ
[!INCLUDE[wf](../includes/wf-md.md)] に含まれる既定のアクティビティ セットは、制御フロー、条件、イベント処理、状態管理、アプリケーションやサービスとの通信などの機能を提供します。 ワークフローを設計するとき、[!INCLUDE[wfd1](../includes/wfd1-md.md)]に付属しているシステム標準のアクティビティを使用することも、独自のカスタム アクティビティを作成することもできます。

 次の表は、[!INCLUDE[wf2](../includes/wf2-md.md)] フレームワークに付属ですぐに使用できるアクティビティ セットの一覧です。 これらのアクティビティの多くは、すべてではなく、[!INCLUDE[wfd2](../includes/wfd2-md.md)] の**ツールボックス**からアクセスできるアクティビティデザイナーによって表されます。 アクティビティを作成するには、**ツールボックス**からデザイナーをドラッグし、デザインサーフェイスにドロップします。

|アクティビティ|説明|
|--------------|-----------------|
|[CallExternalMethodActivity](http://go.microsoft.com/fwlink?LinkID=65025)|ローカルサービスとの入出力通信に**HandleExternalEventActivity**アクティビティと共に使用されます。 [CallExternalMethodActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65060)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[CancellationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65050)|複合アクティビティのすべての子の実行が完了する前に取り消された複合アクティビティのクリーンアップ ロジックを格納するために使用されます。 [CancellationHandlerActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65061)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[CodeActivity](http://go.microsoft.com/fwlink?LinkID=65026)|Visual Basic または C# のコードをワークフローに追加できます。 [CodeActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65062)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[CompensatableSequenceActivity](http://go.microsoft.com/fwlink?LinkID=65027)|[Sequenceactivity](http://go.microsoft.com/fwlink?LinkID=65020)の補正可能バージョン。 [CompensatableSequenceActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65002)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[CompensatableTransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65051)|**TransactionScopeActivity**の補正可能バージョン。 [CompensatableTransactionScopeActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65063)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[CompensateActivity](http://go.microsoft.com/fwlink?LinkID=65052)|エラー発生時に、ワークフローによって実行された操作を取り消すか補正するコードを呼び出すことができます。 [CompensateActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65064)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[CompensationHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65053)|[CompensationHandlerActivity アクティビティ [!INCLUDE[crdefault](../includes/crdefault-md.md)] 使用して](http://go.microsoft.com/fwlink?LinkID=65065)、完了した TransactionScopeActivity アクティビティに対して補正を実行する1つ以上のアクティビティのラッパー。|
|[ConditionedActivityGroup](http://go.microsoft.com/fwlink?LinkID=65017)|[Conditionedactivitygroup](http://go.microsoft.com/fwlink?LinkID=65017)アクティビティ自体に適用される条件に基づいて子アクティビティを実行し、各子に個別に適用される条件に基づいて実行します。 [ConditionedActivityGroup アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65066)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[DelayActivity](http://go.microsoft.com/fwlink?LinkID=65028)|タイムアウト期間に基づいて、ワークフロー内に遅延を作成できます。 [Delayactivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65067)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029)|指定されたイベントが発生すると実行される 1 つまたは複数のアクティビティをラップします。 [EventDrivenActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65068)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018)|イベントをアクティビティに関連付けるフレームワークを提供します。 [EventHandlersActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65069)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[EventHandlingScopeActivity](http://go.microsoft.com/fwlink?LinkID=65030)|[EventHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65018)を使用して、メインの子アクティビティを同時に実行します。 [EventHandlingScopeActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65070)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[FaultHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65054)|指定した種類の例外を処理するために使用します。 [FaultHandlerActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65071)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[FaultHandlersActivity](http://go.microsoft.com/fwlink?LinkID=65055)|[FaultHandlerActivity](http://go.microsoft.com/fwlink?LinkID=65054)型の子アクティビティの順序付きリストを持つ複合アクティビティを表します。 [FaultHandlersActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65072)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[HandleExternalEventActivity](http://go.microsoft.com/fwlink?LinkID=65031)|ローカルサービスとの入出力通信のために、 [Callexternalmethodactivity](http://go.microsoft.com/fwlink?LinkID=65025)アクティビティと組み合わせて使用されます。 [HandleExternalEventActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65073)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033)|各分岐の条件をテストし、条件が**true**に等しい最初の分岐に対してアクティビティを実行します。 [IfElseActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65074)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[IfElseBranchActivity](http://go.microsoft.com/fwlink?LinkID=65034)|[IfElseActivity](http://go.microsoft.com/fwlink?LinkID=65033)の分岐を表します。 [IfElseBranchActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65075)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[InvokeWebServiceActivity](http://go.microsoft.com/fwlink?LinkID=65035)|ワークフローから Web サービスを呼び出すことができます。 [InvokeWebServiceActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65076)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[InvokeWorkflowActivity](http://go.microsoft.com/fwlink?LinkID=65036)|ワークフローから別のワークフローを呼び出すことができます。 [InvokeWorkflowActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65077)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[ListenActivity](http://go.microsoft.com/fwlink?LinkID=65037)|[EventDrivenActivity](http://go.microsoft.com/fwlink?LinkID=65029)子アクティビティだけを含む複合アクティビティ。 [ListenActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65078)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[ParallelActivity](http://go.microsoft.com/fwlink?LinkID=65038)|2つ以上の子**sequenceactivity**アクティビティ分岐を同時に処理するようにスケジュールする方法を提供します。 [Parallelactivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65079)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[PolicyActivity](http://go.microsoft.com/fwlink?LinkID=65019)|ルールのコレクションを表すために使用されます。 ルールは、条件とその結果としてのアクションから構成されます。 [Policyactivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65004)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[ReplicatorActivity](http://go.microsoft.com/fwlink?LinkID=65039)|1 つの子アクティビティから複数のインスタンスを作成します。 [ReplicatorActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65080)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020)|複数のアクティビティをまとめて順次実行するための簡単な方法を提供します。 [Sequenceactivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65081)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[SetStateActivity](http://go.microsoft.com/fwlink?LinkID=65041)|新しいステート (状態) への移行を指定します。 [SetStateActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65082)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[StateActivity](http://go.microsoft.com/fwlink?LinkID=65042)|ステート マシン ワークフローにおける状態を表します。 [Stateactivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65083)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[StateFinalizationActivity](http://go.microsoft.com/fwlink?LinkID=65043)|**Stateactivity**アクティビティを終了するときに実行される子アクティビティのコンテナーとして[stateactivity](http://go.microsoft.com/fwlink?LinkID=65042)アクティビティで使用されます。 [StateFinalizationActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65008)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[StateInitializationActivity](http://go.microsoft.com/fwlink?LinkID=65044)|**Stateactivity**アクティビティの開始時に実行される子アクティビティのコンテナーとして[stateactivity](http://go.microsoft.com/fwlink?LinkID=65042)アクティビティ内で使用されます。 [StateInitializationActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65006)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[SuspendActivity](http://go.microsoft.com/fwlink?LinkID=65056)|特に注意が必要なエラー条件が発生したとき、ワークフローの実行を保留して介入できるようにします。 [SuspendActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65084)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[SynchronizationScopeActivity](http://go.microsoft.com/fwlink?LinkID=65057)|同期されたドメイン内に含まれるアクティビティを順次実行します。 [SynchronizationScopeActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65085)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[TerminateActivity](http://go.microsoft.com/fwlink?LinkID=65058)|エラー条件が発生したとき、ワークフローの実行を即座に終了できます。 [TerminateActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65086)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[ThrowActivity](http://go.microsoft.com/fwlink?LinkID=65059)|ワークフローのプロセス メタデータの一部としてスローされた業務処理例外をキャプチャできます。 [ThrowActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65087)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[TransactionScopeActivity](http://go.microsoft.com/fwlink?LinkID=65093)|トランザクションと例外処理のフレームワークを提供します。 詳細については、「 [TransactionScopeActivity アクティビティの使用](http://go.microsoft.com/fwlink?LinkID=65088)」を参照してください。|
|[WebServiceFaultActivity](http://go.microsoft.com/fwlink?LinkID=65046)|Web サービスで発生するエラーをモデル化できます。 [WebServiceFaultActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65089)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[WebServiceInputActivity](http://go.microsoft.com/fwlink?LinkID=65047)|Web サービスからデータを取得します。 [WebServiceInputActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65090)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[WebServiceOutputActivity](http://go.microsoft.com/fwlink?LinkID=65048)|Web サービスからワークフローに対する要求に応答します。 [WebServiceOutputActivity アクティビティを使用して](http://go.microsoft.com/fwlink?LinkID=65092)[!INCLUDE[crdefault](../includes/crdefault-md.md)] します。|
|[WhileActivity](http://go.microsoft.com/fwlink?LinkID=65049)|条件が満たされるまで、ワークフローをループさせることができます。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][、アクティビティアクティビティを使用](http://go.microsoft.com/fwlink?LinkID=65091)します。|

 カスタムアクティビティの作成方法に [!INCLUDE[crabout](../includes/crabout-md.md)] ては、「[カスタムアクティビティの開発](http://go.microsoft.com/fwlink?LinkID=65023)」および「[従来のアクティビティデザイナーの使用](../workflow-designer/using-the-legacy-activity-designer.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [アクティビティビュー (レガシ)](../workflow-designer/activity-views-legacy.md)アクティビティのさまざまなデザインビューについて説明します。

 [方法: ツールボックスにアクティビティを追加する (レガシ)](../workflow-designer/how-to-add-activities-to-the-toolbox-legacy.md)ツールボックスにアクティビティを追加する方法について説明します。

 [方法: 宣言的ルール条件を作成する (レガシ)](../workflow-designer/how-to-create-a-declarative-rule-condition-legacy.md)宣言型の規則の条件を作成する手順を示します。

 [方法: PolicyActivity 規則セットを作成する (レガシ)](../workflow-designer/how-to-create-a-policyactivity-rule-set-legacy.md)PolicyActivity ルールセットを作成する手順について説明します。

 [方法: WCF コントラクト操作を実装する (レガシ)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md)@No__t_1 コントラクト操作を実装する手順について説明します。

 [方法: WCF コントラクト操作を呼び出す (レガシ)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)@No__t_1 コントラクト操作を呼び出す手順を示します。

## <a name="see-also"></a>参照
 [Windows Workflow Foundation アクティビティ](http://go.microsoft.com/fwlink?LinkID=65005)ワークフローの[開発](http://go.microsoft.com/fwlink?LinkID=65010)[ワークフローアクティビティの開発](http://go.microsoft.com/fwlink?LinkID=65023)