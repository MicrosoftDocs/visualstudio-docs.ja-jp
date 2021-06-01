---
title: ワークフロー デザイナー - ワークフローにコメントを追加する
description: .NET Framework 4.5 を使用して、開発者がデザイナーの特定の種類の項目 (アクティビティ、状態、遷移項目など) に注釈を追加できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 9417dd0084b381d8fc997a90b4690c49191f4785
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971701"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>ワークフロー デザイナーでワークフローにコメントを追加する方法

より大きく複雑なワーク フローを簡単に作成するため、.NET Framework 4.5 では開発者がデザイナーで次の種類の項目に注釈を追加できます。

- <xref:System.Activities.Activity>

- <xref:System.Activities.Statements.State>

- <xref:System.Activities.Statements.Transition>

- クラス (派生) <xref:System.Activities.Statements.FlowNode>

- <xref:System.Activities.Variable>

- <xref:System.Activities.Argument>

> [!IMPORTANT]
> 注釈の内容はワーク フローに関連付けられた XAML ファイルにテキスト形式で保存され、他のユーザーに読み取られる可能性があります。 注釈に機密情報を入力する場合は注意してください。

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>デザイナーのアクティビティへの注釈の追加

1. ワークフロー デザイナーで、ワークフロー デザイナーの項目を右クリックし、 **[注釈]** 、 **[注釈の追加]** の順に選択します。

1. 注釈のテキストを提供された領域に追加します。

   項目に注釈アイコンが表示されます。 注釈アイコン上にカーソルを置くと、注釈のテキストが表示されます。

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>アクティビティのデザイナーへの注釈の表示

1. アクティビティの外部に注釈を表示するアクティビティ デザイナーで、注釈の装飾の **[ピン]** アイコンをクリックします。

   注釈がアクティビティ デザイナーに表示されます。 次のスクリーンショットでは、「ワーク フローのアクティビティを開始する」という注釈がアクティビティ デザイナーに表示されています。

   ![注釈がアクティビティ デザイナーに表示されている](../workflow-designer/media/annotationindesigner.png)

2. アクティビティ デザイナーの外部に注釈を表示するには、アクティビティのデザイナーの注釈の領域にカーソルを置き、 **[ピン解除]** アイコンをクリックします。

   ![アクティビティ デザイナーの外部に表示されている注釈](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>すべての注釈の表示または非表示

1. 注釈を持つアクティビティを右クリックします。 **[注釈]** 、 **[すべての注釈を表示]** の順に選択します。

   すべての注釈がアクティビティのデザイナーに表示されます。

1. アクティビティのデザイナーの外部のすべての注釈を表示するには、アクティビティを右クリックし、 **[注釈]** 、 **[すべての注釈を非表示]** の順に選択します。

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>アクティビティの注釈の編集または削除

1. 注釈を持つアクティビティを右クリックします。

1. **[注釈]** 、 **[注釈の編集]** または **[注釈の削除]** を選択します。

   編集または削除用に注釈が開きます。

1. すべての注釈を一度に削除するには、ワークフロー デザイナーを右クリックし、 **[注釈]** 、 **[すべての注釈を削除]** の順に選択します。

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>変数または引数の注釈の追加、編集、削除

1. 変数または引数を右クリックし、[注釈の追加] をクリックします。

1. 注釈のテキストを入力します。 変数または引数に注釈アイコンが表示されます。

1. 注釈を持つ変数または引数を右クリックします。 [注釈の編集] をクリックします。

   編集用に注釈が開きます。

1. 注釈を持つ変数または引数を右クリックします。 [注釈の削除] をクリックします。

   注釈が削除されます。
