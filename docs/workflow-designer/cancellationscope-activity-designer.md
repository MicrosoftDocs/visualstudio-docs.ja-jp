---
title: CancellationScope アクティビティ デザイナー
description: ワークフロー デザイナーの CancellationScope アクティビティ デザイナーを使用して、CancellationScope アクティビティを作成して構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CancellationScope.UI
ms.assetid: 2c85d663-b219-4142-9866-7693ffd46379
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ef415763a67232f79b269650abecfe6bcabe6bd2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937200"
---
# <a name="cancellationscope-activity-designer"></a>CancellationScope アクティビティ デザイナー

**CancellationScope** アクティビティ デザイナーは、<xref:System.Activities.Statements.CancellationScope> アクティビティを作成して構成するために使用します。

## <a name="the-cancellationscope-activity"></a>CancellationScope アクティビティ

<xref:System.Activities.Statements.CancellationScope> アクティビティを使用すると、実行のアクティビティと、そのアクティビティの取り消しロジックを指定できます。

### <a name="using-the-cancellationscope-activity-designer"></a>CancellationScope アクティビティ デザイナーの使用

**CancellationScope** アクティビティデザイナーは、 **[ツールボックス]** の **[トランザクション]** カテゴリにあります。 **ツールボックス** を開くには、ワークフロー デザイナーの **[ツールボックス]** タブを選択します。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl**+**Alt**+**X** キーを押します。

**CancellationScope** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される任意のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 **CancellationScope** アクティビティ デザイナーをドロップすると、CancellationScope の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.Activities.Statements.CancellationScope> アクティビティが作成されます。 **CancellationScope** アクティビティ デザイナーのヘッダーの <xref:System.Activities.Activity.DisplayName%2A> 値を編集します。 プロパティ グリッドの **[DisplayName]** ボックスで編集することもできます。

### <a name="the-cancellationscope-properties"></a>CancellationScope プロパティ

次の表に、<xref:System.Activities.Statements.CancellationScope> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティはプロパティ グリッドで編集できますが、その他のプロパティはワークフロー デザイナー画面で編集する必要があります。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.CancellationScope> アクティビティの省略可能な表示名。 既定では、CancellationScope です。 <xref:System.Activities.Activity.DisplayName%2A> 値は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.CancellationScope.Body%2A>|はい|取り消しロジックの対象となるアクティビティを指定します。 <xref:System.Activities.Statements.CancellationScope.Body%2A> アクティビティを追加するには、アクティビティを **[ツールボックス]** から **CancellationScope** アクティビティ デザイナーの **[Body]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒント テキストを追加します。|
|<xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A>|はい|取り消しがある場合に実行されるアクティビティを指定します。 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> アクティビティを追加するには、アクティビティを **[ツールボックス]** から **CancellationScope** アクティビティ デザイナーの **[CancellationHandler]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒント テキストを追加します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
