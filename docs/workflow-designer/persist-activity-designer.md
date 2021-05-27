---
title: ワークフロー デザイナー - Persist アクティビティ デザイナー
description: Persist アクティビティと、Persist アクティビティ デザイナーを使用して Persist アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Persist.UI
ms.assetid: be8648dd-3eb9-4a50-8ec1-57a8be804692
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 988c080b7b6c89baa4151858fcaf4e3320582e09
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968724"
---
# <a name="persist-activity-designer"></a>Persist アクティビティ デザイナー

**Persist** アクティビティ デザイナーは、<xref:System.Activities.Statements.Persist> アクティビティを作成および構成するために使用します。

## <a name="the-persist-activity"></a>Persist アクティビティ

<xref:System.Activities.Statements.Persist> アクティビティで、ワークフローをディスクに保存します (可能な場合)。 <xref:System.Activities.Statements.Persist> アクティビティは、<xref:System.Activities.Statements.TransactionScope> アクティビティ内などの非永続化ゾーンでは実行できません。 非永続化スコープで <xref:System.Activities.Statements.Persist> アクティビティを使用すると、実行時に例外がスローされます。

### <a name="using-the-persist-activity-designer"></a>Persist アクティビティ デザイナーの使用

**Persist** アクティビティ デザイナーは、 **[ツールボックス]** の **[ランタイム]** カテゴリにあります。アクセスするには、 **[ツールボックス]** タブをクリックします (または、 **[表示]** メニューの **[ツールボックス]** をクリックするか、CTRL + ALT + X キーを押します)。

**Persist** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが配置される通常のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 この操作により、Persist という既定の **DisplayName** を持つ <xref:System.Activities.Statements.Persist> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**Persist** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-persist-properties"></a>Persist のプロパティ

次の表に、<xref:System.Activities.Statements.Persist> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集でき、一部のプロパティは、ワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Persist> アクティビティの表示名。 既定値は Persist です。 表示名は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>関連項目

- [Runtime](../workflow-designer/runtime-activity-designers.md)
- [TerminateWorkflow](../workflow-designer/terminateworkflow-activity-designer.md)
