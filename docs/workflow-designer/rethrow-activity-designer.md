---
title: ワークフロー デザイナー - Rethrow アクティビティ デザイナー
description: Rethrow アクティビティと、Rethrow アクティビティ デザイナーを使用して Rethrow アクティビティを作成し、構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2e3615c73583e8c5c313d23fd5f9aa6d9fcd5ff4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847324"
---
# <a name="rethrow-activity-designer"></a>Rethrow アクティビティ デザイナー

**Rethrow** アクティビティ デザイナーは、<xref:System.Activities.Statements.Rethrow> アクティビティを作成および構成するために使用します。

## <a name="the-rethrow-activity"></a>Rethrow アクティビティ

<xref:System.Activities.Statements.Rethrow> アクティビティでは、以前にスローされた例外をスローします。 このアクティビティは、<xref:System.Activities.Statements.Catch> アクティビティの <xref:System.Activities.Statements.TryCatch> ハンドラーでのみ使用できます。

### <a name="use-the-rethrow-activity-designer"></a>ReThrow アクティビティ デザイナーを使用する

**[ツールボックス]** の **[エラー処理]** カテゴリにある **Rethrow** アクティビティ デザイナーにアクセスします。 **Rethrow** アクティビティ デザイナーを **[ツールボックス]** からドラッグして、アクティビティが配置される通常のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 アクティビティ デザイナーをドロップすると、Throw という既定の **DisplayName** を持つ <xref:System.Activities.Statements.Rethrow> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> 値は、**Rethrow** アクティビティ デザイナーのヘッダー、またはプロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-rethrow-properties"></a>Rethrow のプロパティ

次の表に、<xref:System.Activities.Statements.Rethrow> のプロパティと、それらがデザイナーでどのように使用されるかを示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Rethrow> アクティビティの表示名を指定します (省略可能)。 既定値は Rethrow です。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)
