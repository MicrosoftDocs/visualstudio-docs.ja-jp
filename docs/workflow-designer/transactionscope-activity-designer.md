---
title: ワークフロー デザイナー - TransactionScope アクティビティ デザイナー
description: TransactionScope アクティビティ デザイナーを使用し、TransactionScope アクティビティを作成し、構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.TransactionScope.UI
ms.assetid: 8d7ebfc6-7478-4888-b3b0-b14f296096af
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 234e6c2d0349cf610d9ba22d53ce59e3768ad64e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99838010"
---
# <a name="transactionscope-activity-designer"></a>TransactionScope アクティビティ デザイナー

**TransactionScope** アクティビティ デザイナーは、<xref:System.Activities.Statements.TransactionScope> アクティビティを作成および構成するために使用します。

## <a name="the-transactionscope-activity"></a>TransactionScope アクティビティ

<xref:System.Activities.Statements.TransactionScope> アクティビティでは、含まれているアクティビティを単一のトランザクションで実行します。 <xref:System.Activities.Statements.TransactionScope.Body%2A> アクティビティおよびトランザクションの他のすべての参加要素が正常に完了すると、トランザクションはコミットされます。

### <a name="using-the-transactionscope-activity-designer"></a>TransactionScope アクティビティ デザイナーの使用

**[ツールボックス]** の **[トランザクション]** カテゴリで **TransactionScope** アクティビティにアクセスします。 **TransactionScope** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される通常のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 この操作により、TransactionScope という既定の <xref:System.Activities.Statements.TransactionScope> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> 値は、**TransactionScope** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-transactionscope-properties"></a>TransactionScope プロパティ

次の表に、<xref:System.Activities.Statements.TransactionScope> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティと <xref:System.Activities.Statements.TransactionScope.Body%2A> プロパティは、ワークフロー デザイナー画面で編集できます。 ただし、他のプロパティは、プロパティ グリッドで編集する必要があります。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.TransactionScope> アクティビティの省略可能な表示名。 既定値は、TransactionScope です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.TransactionScope.Body%2A>|はい|単一のトランザクションで実行するアクティビティを指定します。 <xref:System.Activities.Statements.TransactionScope.Body%2A> アクティビティを追加するには、"ここにアクティビティをドロップします" というヒント テキストが表示された **TransactionScope** アクティビティ デザイナーの **[Body]** ボックスに、 **[ツールボックス]** からアクティビティをドロップします。|
|<xref:System.Activities.Statements.TransactionScope.IsolationLevel%2A>|はい|この <xref:System.Transactions.IsolationLevel> の <xref:System.Activities.Statements.TransactionScope> を指定します。|
|<xref:System.Activities.Statements.TransactionScope.Timeout%2A>|いいえ|トランザクションが完了するまでの時間間隔を "00:00:00" (時:分:秒) という形式で指定します。 既定値は 1 分 (00:01:00) です。|
|<xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure*>|はい|トランザクションが中止した場合にワークフローを中止する必要があるかどうかを示す値を指定します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
