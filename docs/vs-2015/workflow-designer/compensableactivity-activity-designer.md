---
title: CompensableActivity アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.CompensableActivity.UI
ms.assetid: e0340d89-d39e-4a52-8557-13e27040d7b5
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e2bc28c4586912d7c253c9629c2af0eefd30e47e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656994"
---
# <a name="compensableactivity-activity-designer"></a>CompensableActivity アクティビティ デザイナー
**CompensableActivity**アクティビティデザイナーは、<xref:System.Activities.Statements.CompensableActivity> アクティビティを作成および構成するために使用されます。

## <a name="the-compensableactivity-activity"></a>CompensableActivity アクティビティ
 <xref:System.Activities.Statements.CompensableActivity> で、正常に完了した後に確認または補正できる作業単位を定義します。

### <a name="using-the-compensableactivity-activity-designer"></a>CompensableActivity アクティビティ デザイナーの使用
 **CompensableActivity**アクティビティデザイナーは、**ツールボックス**の **[トランザクション]** カテゴリにあります。このカテゴリにアクセスするには、[!INCLUDE[wfd2](../includes/wfd2-md.md)] の左側にある **[ツールボックス]** タブをクリックします (または、 **[ツールバー]** を選択します)。 **[表示]** メニューから、または CTRL + ALT + X キーを押します)。

 **CompensableActivity**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置している任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) にドロップして [!INCLUDE[wfd2](../includes/wfd2-md.md)] 画面にドロップできます。 この操作により、CompensableActivity という既定の <xref:System.Activities.Statements.CompensableActivity> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 @No__t_0 値は、 **CompensableActivity**アクティビティデザイナーのヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-compensableactivity-properties"></a>CompensableActivity のプロパティ
 次の表に、<xref:System.Activities.Statements.CompensableActivity> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティと <xref:System.Activities.Activity%601.Result%2A> プロパティはプロパティ グリッドで編集できますが、それ以外のプロパティは[!INCLUDE[wfd2](../includes/wfd2-md.md)]画面で編集する必要があります。

|プロパティ名|必要|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.CompensableActivity> アクティビティの省略可能な表示名。 既定値は CompensableActivity です。|
|<xref:System.Activities.Activity%601.Result%2A>|False|<xref:System.Activities.Statements.CompensableActivity> の戻り値を指定します。 このプロパティは、プロパティ グリッドで編集する必要があります。|
|<xref:System.Activities.Statements.CompensableActivity.Body%2A>|True|補正、取り消し、および確認の各ロジックの提供対象のアクティビティを指定します。 @No__t_0 アクティビティを追加するには、"ここにアクティビティをドロップします" というヒントテキストが表示された**CompensableActivity**アクティビティデザイナーの **[Body]** ボックスに、 **[ツールボックス]** からアクティビティをドロップします。|
|<xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>|False|取り消しの際に実行されるアクティビティを指定します。 アクティビティを追加するには、"ここにアクティビティをドロップします" というヒントテキストが表示された**CompensableActivity**アクティビティデザイナーの **[CancellationHandler]** ボックスに、**ツールボックス**からデザイナーをドロップします。|
|<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>|False|<xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティの補正を行うときに実行されるアクティビティを指定します。 このハンドラーは、<xref:System.Activities.Statements.Compensate> アクティビティを使用して明示的に呼び出すことができます。<br /><br /> アクティビティを追加するには、"ここにアクティビティをドロップします" というヒントテキストが表示された**CompensableActivity**アクティビティデザイナーの **[CompensationHandler]** ボックスに、 **[ツールボックス]** からアクティビティデザイナーをドロップします。|
|<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>|False|<xref:System.Activities.Statements.CompensableActivity.Body%2A> アクティビティを確認するときに実行されるアクティビティを指定します。 このハンドラーは、<xref:System.Activities.Statements.Confirm> アクティビティを使用して明示的に呼び出すことができます。<br /><br /> アクティビティを追加するには、"ここにアクティビティをドロップします" というヒントテキストが表示された**CompensableActivity**アクティビティデザイナーの  **confirmationhandler**  ボックスに、**ツールボックス** からアクティビティデザイナーをドロップします。|

## <a name="see-also"></a>参照
 [トランザクション](../workflow-designer/transaction-activity-designers.md) [CancellationScope](../workflow-designer/cancellationscope-activity-designer.md) [補正](../workflow-designer/compensate-activity-designer.md)の[確認](../workflow-designer/confirm-activity-designer.md) [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)