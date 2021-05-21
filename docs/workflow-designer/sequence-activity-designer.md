---
title: ワークフロー デザイナー - Sequence アクティビティ デザイナー
description: Sequence アクティビティには、子アクティビティの順序付きコレクションが含まれ、これによって子アクティビティが順番に実行されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Sequence.UI
ms.assetid: 51c8d3cb-4d43-458f-9631-b63755f9ac94
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c7bfc8c850cee9273af2af3b28f71b9d27209d9a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943641"
---
# <a name="sequence-activity-designer"></a>Sequence アクティビティ デザイナー

<xref:System.Activities.Statements.Sequence> アクティビティには、子アクティビティの順序付きコレクションが含まれており、これらのコレクションが順番に実行されます。

他の方法でアクティビティのセットを順番に実行するには、<xref:System.Activities.Statements.Flowchart> アクティビティを使用します。 単純な分岐またはループのプログラム フローをダイアグラムでモデル化する場合は、[フローチャート](../workflow-designer/flowchart-activity-designer.md)の使用を検討してください。

## <a name="using-the-sequence-activity-designer"></a>Sequence アクティビティ デザイナーの使用

<xref:System.Activities.Statements.Sequence> アクティビティを追加するには、**ツールボックス** から **Sequence** アクティビティ デザイナーをドラッグして、ワークフロー デザイナー画面にドロップします。 この <xref:System.Activities.Statements.Sequence> アクティビティに子アクティビティを追加するには、**ツールボックス** から他のアクティビティをドラッグして、"ここにアクティビティをドロップ" というヒント テキストが表示される、ボックス内の三角形にドロップします。

### <a name="sequence-activity-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Sequence アクティビティのプロパティ

次の表に、<xref:System.Activities.Statements.Sequence> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|ヘッダーの <xref:System.Activities.Statements.Sequence> アクティビティ デザイナーの表示名を指定します。 既定値は Sequence です。 この値は、プロパティ グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)