---
title: '方法: ワークフロー デザイナーでワークフローにコメントを追加 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.Annotations.Annotation.UI
- Annotation
ms.assetid: 9aa0e8d6-8129-4438-8389-d460611581a7
caps.latest.revision: 7
author: steved0x
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 507bb70539019646f57f0aa9267573429d3fa202
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433544"
---
# <a name="how-to-add-comments-to-a-workflow-in-the-workflow-designer"></a>方法: ワークフロー デザイナーでワークフローにコメントを追加する
より大きく複雑なワーク フローを簡単に作成するため、[!INCLUDE[net_v45](../includes/net-v45-md.md)] では開発者がデザイナーで次の種類の項目に注釈を追加できます。  
  
- <xref:System.Activities.Activity>  
  
- <xref:System.Activities.Statements.State>  
  
- <xref:System.Activities.Statements.Transition>  
  
- クラス (派生) <xref:System.Activities.Statements.FlowNode>  
  
- <xref:System.Activities.Variable>  
  
- <xref:System.Activities.Argument>  
  
> [!IMPORTANT]
> 注釈の内容はワーク フローに関連付けられた XAML ファイルにテキスト形式で保存され、他のユーザーに読み取られる可能性があります。 注釈に機密情報を入力する場合は注意してください。  
  
### <a name="adding-an-annotation-to-an-activity-in-the-designer"></a>デザイナーのアクティビティへの注釈の追加  
  
1. デザイナーで選択し、ワークフロー内の項目を右クリックし、ワークフロー デザイナーで**注釈**、**注釈の追加**します。  
  
2. 注釈のテキストを提供された領域に追加します。  
  
3. 項目に注釈アイコンが表示されます。 注釈アイコン上にカーソルを置くと、注釈のテキストが表示されます。  
  
     ![注釈を表示するアクティビティをシーケンス](../workflow-designer/media/annotation.png "注釈")  
  
### <a name="displaying-an-annotation-in-an-activitys-designer"></a>アクティビティのデザイナーへの注釈の表示  
  
1. アクティビティの外部に注釈を表示するアクティビティ デザイナー、をクリックして、 **Pin**注釈の装飾のアイコン。  
  
2. 注釈がアクティビティ デザイナーに表示されます。 次のスクリーンショットでは、「ワーク フローのアクティビティを開始する」という注釈がアクティビティ デザイナーに表示されています。  
  
     ![アクティビティ デザイナーに表示されるアノテーション](../workflow-designer/media/annotationindesigner.png "AnnotationInDesigner")  
  
3. アクティビティ デザイナーの外部に注釈を表示するアクティビティのデザイナーでの注釈の領域をポイントし、をクリックして、**ピン解除**アイコン  
  
     ![注釈がアクティビティのデザイナーの外に表示されて](../workflow-designer/media/annotationoutsidedesigner.png "AnnotationOutsideDesigner")  
  
### <a name="showing-or-hiding-all-annotations"></a>すべての注釈の表示または非表示  
  
1. 注釈を持つアクティビティを右クリックします。 選択**注釈**、**すべての注釈を表示する**します。  
  
2. すべての注釈がアクティビティのデザイナーに表示されます。  
  
3. アクティビティのデザイナーの外部のすべての注釈を表示するには、アクティビティを選択します右クリックして**注釈**、**すべての注釈を非表示に**します。  
  
### <a name="editing-or-deleting-an-annotation-for-an-activity"></a>アクティビティの注釈の編集または削除  
  
1. 注釈を持つアクティビティを右クリックします。  
  
2. 選択**注釈**、 **注釈の編集**または**注釈の削除**します。  
  
3. 編集または削除用に注釈が開きます。  
  
4. すべての注釈を一度に削除するには、ワークフローのデザイナーと選択を右クリックして**注釈**、**注釈をすべて削除**します。  
  
### <a name="adding-editing-and-deleting-an-annotation-for-a-variable-or-argument"></a>変数または引数の注釈の追加、編集、削除  
  
1. 変数または引数を右クリックし、[注釈の追加] をクリックします。  
  
2. 注釈のテキストを入力します。 変数または引数に注釈アイコンが表示されます。  
  
3. 注釈を持つ変数または引数を右クリックします。 [注釈の編集] をクリックします。  
  
4. 編集用に注釈が開きます。  
  
5. 注釈を持つ変数または引数を右クリックします。 [注釈の削除] をクリックします。  
  
6. 注釈が削除されます。