---
title: ワークフローデザイナー-再スローアクティビティデザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Rethrow.UI
ms.assetid: 9cfa2eda-395f-4cf3-9154-83fadd4f7452
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d015ad500537a17cfc2c48c8076df43a38534ea
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650015"
---
# <a name="rethrow-activity-designer"></a>Rethrow アクティビティ デザイナー

再**スロー**アクティビティデザイナーは、<xref:System.Activities.Statements.Rethrow> アクティビティを作成および構成するために使用されます。

## <a name="the-rethrow-activity"></a>再スローアクティビティ

<xref:System.Activities.Statements.Rethrow> アクティビティでは、以前にスローされた例外をスローします。 このアクティビティは、<xref:System.Activities.Statements.Catch> アクティビティの <xref:System.Activities.Statements.TryCatch> ハンドラーでのみ使用できます。

### <a name="use-the-rethrow-activity-designer"></a>再スローアクティビティデザイナーの使用

**ツールボックス**の**エラー処理**カテゴリの再**スロー**アクティビティデザイナーにアクセスします。 再**スロー**アクティビティデザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置している任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) にドロップしてワークフローデザイナー画面にドロップできます。 アクティビティデザイナーを削除すると、Throw という既定の**DisplayName**を持つ <xref:System.Activities.Statements.Rethrow> アクティビティが作成されます。 @No__t_0 値は、再**スロー**アクティビティデザイナーのヘッダー、またはプロパティグリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-rethrow-properties"></a>再スロープロパティ

次の表は、<xref:System.Activities.Statements.Rethrow> のプロパティと、デザイナーでのそれらの使用方法を示しています。

|プロパティ名|必要|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.Rethrow> アクティビティの表示名を指定します (省略可能)。 既定値は Rethrow です。|

## <a name="see-also"></a>関連項目

- [コレクション](../workflow-designer/collection-activity-designers.md)
- [Throw](../workflow-designer/throw-activity-designer.md)
- [TryCatch](../workflow-designer/trycatch-activity-designer.md)