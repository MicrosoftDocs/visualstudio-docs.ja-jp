---
title: 'ワークフロー デザイナー - 方法: ワークフローにコメントを追加'
ms.date: 11/04/2016
ms.topic: conceptual
ms.prod: visual-studio-dev15
ms.technology: vs-workflow-designer
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: d740614ed94d0fd91ba9f3e73a083791b9112919
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34752028"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>ワークフロー デザイナーでワークフローにコメントを追加する方法

大規模で複雑なワークフローを作成するためには、.NET Framework 4.5 には、デザイナー内の項目の次の種類に注釈を追加する開発者が使用できます。

-   <xref:System.Activities.Activity>

-   <xref:System.Activities.Statements.State>

-   <xref:System.Activities.Statements.Transition>

-   クラス (派生) <xref:System.Activities.Statements.FlowNode>

-   <xref:System.Activities.Variable>

-   <xref:System.Activities.Argument>

> [!IMPORTANT]
> 注釈の内容はワーク フローに関連付けられた XAML ファイルにテキスト形式で保存され、他のユーザーに読み取られる可能性があります。 注釈に機密情報を入力する場合は注意してください。

## <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>デザイナーのアクティビティへの注釈の追加

1. ワークフロー デザイナーと選択内の項目を右クリックし、ワークフロー デザイナーで**注釈**、**注釈の追加**です。

1. 注釈のテキストを提供された領域に追加します。

   アイテムには、注釈アイコンが表示されます。 注釈アイコンの上にマウスには、注釈のテキストが表示されます。

## <a name="displaying-an-annotation-in-an-activitys-designer"></a>アクティビティのデザイナーへの注釈の表示

1.  アクティビティの外部に注釈表示するアクティビティ デザイナー、をクリックして、 **Pin**注釈の装飾のアイコン。

   注釈は、アクティビティのデザイナーに表示されます。 次のスクリーンショットでは、「ワーク フローのアクティビティを開始する」という注釈がアクティビティ デザイナーに表示されています。

   ![注釈がアクティビティ デザイナーに表示されている](../workflow-designer/media/annotationindesigner.png)

1. アクティビティ デザイナーの外部に注釈を表示するアクティビティ デザイナーの注釈の領域を合わせるし をクリックして、**ピン解除** アイコン

   ![注釈がアクティビティ デザイナーの外部に表示されている](../workflow-designer/media/annotationoutsidedesigner.png)

## <a name="showing-or-hiding-all-annotations"></a>すべての注釈の表示または非表示

1. 注釈を持つアクティビティを右クリックします。 選択**注釈**、**すべての注釈を表示する**です。

   すべての注釈は、アクティビティのデザイナーに表示されます。

1. クリックし、アクティビティを右クリックし、アクティビティのデザイナーの外部のすべての注釈を表示する**注釈**、**すべての注釈を非表示に**です。

## <a name="editing-or-deleting-an-annotation-for-an-activity"></a>アクティビティの注釈の編集または削除

1. 注釈を持つアクティビティを右クリックします。

1. 選択**注釈**、 **注釈の編集**または**注釈を削除**です。

   注釈は編集用に開くか、削除します。

1. すべての注釈を一度に削除するには、ワークフロー デザイナーと選択を右クリックして**注釈**、**注釈をすべて削除**です。

## <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>変数または引数の注釈の追加、編集、削除

1. 変数または引数を右クリックし、[注釈の追加] をクリックします。

1. 注釈のテキストを入力します。 変数または引数に注釈アイコンが表示されます。

1. 注釈を持つ変数または引数を右クリックします。 [注釈の編集] をクリックします。

   注釈は編集用に開きます。

1. 注釈を持つ変数または引数を右クリックします。 [注釈の削除] をクリックします。

   注釈は削除されます。