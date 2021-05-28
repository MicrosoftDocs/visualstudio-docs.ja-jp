---
title: CompensableActivity アクティビティ デザイナー
description: ワークフロー デザイナーの CompensableActivity アクティビティ デザイナーを使用して、CompensableActivity アクティビティを作成して構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9612e1b8e808437122df88ad0bbef3a4cce74c0c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955113"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity アクティビティ デザイナー

**CompensableActivity** アクティビティ デザイナーは、<xref:System.Activities.Statements.CompensableActivity> アクティビティを作成して構成するために使用します。

## <a name="the-compensableactivity-activity"></a>CompensableActivity アクティビティ
 <xref:System.Activities.Statements.CompensableActivity> で、正常に完了した後に確認または補正できる作業単位を定義します。

### <a name="using-the-compensableactivity-activity-designer"></a>CompensableActivity アクティビティ デザイナーの使用
 **CompensableActivity** アクティビティ デザイナーは、 **[ツールボックス]** の **[トランザクション]** カテゴリにあります。 **ツールボックス** を開くには、ワークフロー デザイナーの左側にある **[ツールボックス]** タブを選択します。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** + **Alt**+ **X** キーを押します。

 **CompensableActivity** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグしてワークフロー デザイナー画面にドロップできます。 <xref:System.Activities.Statements.Sequence> 内にアクティビティ デザイナーをドロップできます。 アクティビティ デザイナーをドロップすると、CompensableActivity の既定の <xref:System.Activities.Activity.DisplayName%2A> で <xref:System.Activities.Statements.CompensableActivity> アクティビティが作成されます。 **CompensableActivity** アクティビティ デザイナーのヘッダーの <xref:System.Activities.Activity.DisplayName%2A> 値を編集します。 プロパティ グリッドの **[DisplayName]** ボックスで編集することもできます。

### <a name="the-compensableactivity-properties"></a>CompensableActivity のプロパティ
 次の表に、<xref:System.Activities.Statements.CompensableActivity> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> と <xref:System.Activities.Activity%601.Result%2A> プロパティはプロパティ グリッドで編集できますが、その他のプロパティはワークフロー デザイナー画面で編集する必要があります。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.CompensableActivity> アクティビティの省略可能な表示名。 既定値は CompensableActivity です。|
|<xref:System.Activities.Activity%601.Result%2A>|いいえ|<xref:System.Activities.Statements.CompensableActivity> の戻り値を指定します。 このプロパティは、プロパティ グリッドで編集する必要があります。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|はい|補正、取り消し、および確認の各ロジックの提供対象のアクティビティを指定します。 <xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティを追加するには、アクティビティを **[ツールボックス]** から **CompensableActivity** アクティビティ デザイナーの **[Body]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒント テキストを追加します。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|いいえ|取り消しがあるときに実行されるアクティビティを指定します。 アクティビティを追加するには、 **[ツールボックス]** からデザイナーを **CompensableActivity** アクティビティ デザイナーの **[CancellationHandler]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒント テキストを追加します。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|いいえ|<xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティの補正を行うときに実行されるアクティビティを指定します。 このハンドラーは、<xref:System.Activities.Statements.Compensate> アクティビティを使用して明示的に呼び出すことができます。<br /><br /> アクティビティを追加するには、アクティビティ デザイナーを **[ツールボックス]** から **CompensableActivity** アクティビティ デザイナーの **[CompensationHandler]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒント テキストを追加します。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|いいえ|<xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティを確認するときに実行されるアクティビティを指定します。 このハンドラーは、<xref:System.Activities.Statements.Confirm> アクティビティを使用して明示的に呼び出すことができます。<br /><br /> アクティビティを追加するには、デザイナーを **[ツールボックス]** から **CompensableActivity** アクティビティ デザイナーの **[ConfirmationHandler]** ボックスにドロップします。 "ここにアクティビティをドロップします" というヒント テキストを追加します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md)
- [Compensate](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)
