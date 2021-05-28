---
title: ワークフロー デザイナー - Compensate アクティビティ デザイナー
description: Compensate アクティビティ デザイナーについて、および Compensate アクティビティ デザイナーを使用して Compensate アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Compensate.UI
ms.assetid: 7347c947-bfff-4bad-becd-5cd23e7b24cd
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 36ab20854adb952d098f71904cdd3cb092e27ac9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955685"
---
# <a name="compensate-activity-designer"></a>Compensate アクティビティ デザイナー

**Compensate** アクティビティ デザイナーは、<xref:System.Activities.Statements.Compensate> アクティビティを作成および構成するために使用します。

## <a name="the-compensate-activity"></a>Compensate アクティビティ

<xref:System.Activities.Statements.Compensate> アクティビティは、<xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> に含まれているアクティビティの <xref:System.Activities.Statements.CompensableActivity> を明示的に呼び出します。 <xref:System.Activities.Statements.Compensate> アクティビティが <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A> の <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 内、<xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A> 内、および <xref:System.Activities.Statements.CompensableActivity> 内のいずれでも使用されていない場合は、<xref:System.Activities.Statements.Compensate.Target%2A> プロパティを指定する必要があります。

<xref:System.Activities.Statements.CompensationToken> で指定された <xref:System.Activities.Statements.Compensate.Target%2A> は、<xref:System.Activities.Statements.CompensableActivity> の <xref:System.Activities.Statements.CompensableActivity.Body%2A> が正常に完了した後に <xref:System.Activities.Statements.CompensableActivity> を明示的に確認または補正する手段を提供します。

### <a name="using-the-compensate-activity-designer"></a>Compensate アクティビティ デザイナーの使用

**Compensate** アクティビティ デザイナーは、 **[ツールボックス]** の **[トランザクション]** カテゴリにあります。 **ツールボックス** を開くには、ワークフロー デザイナーの左側にある **[ツールボックス]** タブを選択します。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** + **Alt**+ **X** キーを押します。

**Compensate** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される任意のワークフロー デザイナー サーフェス (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 アクティビティ デザイナーをドロップすると、Compensate の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.Activities.Statements.Compensate> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> 値は、**Compensate** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-compensate-properties"></a>Compensate のプロパティ

次の表に、<xref:System.Activities.Statements.CancellationScope> のプロパティと、デザイナーでのその使用方法を示します。 <xref:System.Activities.Activity.DisplayName%2A> プロパティは、プロパティ グリッドまたはワークフロー デザイナー画面で編集できます。 <xref:System.Activities.Statements.Compensate.Target%2A> プロパティは、プロパティ グリッドで編集します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Compensate> アクティビティの表示名を指定します (省略可能)。 既定値は Compensate です。|
|<xref:System.Activities.Statements.Compensate.Target%2A>|はい|この <xref:System.Activities.InArgument%601> アクティビティの <xref:System.Activities.Statements.CompensationToken> を含む <xref:System.Activities.Statements.Compensate> を指定します。|

## <a name="see-also"></a>関連項目

- [トランザクション](../workflow-designer/transaction-activity-designers.md)
- [CompensableActivity](../workflow-designer/compensableactivity-activity-designer.md)
- [Compensate アクティビティ デザイナー](../workflow-designer/compensate-activity-designer.md)
- [Confirm](../workflow-designer/confirm-activity-designer.md)
- [TransactionScope](../workflow-designer/transactionscope-activity-designer.md)