---
title: ワークフロー デザイナー - DoWhile アクティビティ デザイナー
description: DoWhile アクティビティで、指定した条件が false に評価されるまで、Body に含まれるアクティビティを 1 回以上実行するしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.DoWhile.UI
ms.assetid: 948deb35-d72f-462b-bea6-4b119c10a148
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6e117fcbea0488c4b6a42125971984b86cf78251
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894258"
---
# <a name="dowhile-activity-designer"></a>DoWhile アクティビティ デザイナー

<xref:System.Activities.Statements.DoWhile> アクティビティでは、指定した条件が **false** に評価されるまで、<xref:System.Activities.Statements.DoWhile.Body%2A> に含まれるアクティビティを 1 回以上実行します。 ループの本体に含まれるアクティビティを 0 回以上実行する必要がある場合は、代わりに、<xref:System.Activities.Statements.While> アクティビティを使用します。

## <a name="dowhile-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの DoWhile のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.DoWhile> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.DoWhile.Body%2A>|いいえ|条件が **true** に評価されるときに実行されるアクティビティ。 <xref:System.Activities.Statements.DoWhile.Body%2A> アクティビティを追加するには、"ここにアクティビティをドロップします" というヒント テキストが表示された **DoWhile** アクティビティ デザイナーの **[Body]** ボックスに、[ツールボックス] からアクティビティをドロップします。|
|<xref:System.Activities.Statements.DoWhile.Condition%2A>|はい|ループの各繰り返しの後に評価する条件。 <xref:System.Activities.Statements.DoWhile.Condition%2A> を設定するには、**DoWhile** アクティビティ デザイナーまたはプロパティ グリッドの **[Condition]** ボックスに Visual Basic の式を入力します。|

## <a name="see-also"></a>関連項目

- [While](../workflow-designer/while-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)