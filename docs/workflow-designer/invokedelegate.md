---
title: ワークフロー デザイナー - InvokeDelegate
description: InvokeDelegate デザイナーについて、および InvokeDelegate デザイナーを使用して InvokeDelegate アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InvokeDelegate Designer
- System.Activities.Statements.InvokeDelegate.UI
ms.assetid: 289a7498-5127-453f-beb5-05f05b80d26f
author: TerryGLee
ms.author: tglee
ms.workload:
- multiple
ms.openlocfilehash: a482f23b1df1587e9a1c7e3023bfb0d1737f1fae
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437750"
---
# <a name="invokedelegate"></a>InvokeDelegate

**InvokeDelegate** デザイナーは、<xref:System.Activities.Statements.InvokeDelegate> アクティビティを作成および構成するために使用します。

## <a name="the-invokedelegate-activity"></a>InvokeDelegate アクティビティ

<xref:System.Activities.Statements.InvokeDelegate> はパブリック デリゲートを呼び出します。

### <a name="use-the-invokedelegate-activity-designer"></a>InvokeDelegate アクティビティ デザイナーを使用する

**[ツールボックス]** の **[プリミティブ]** カテゴリで、**InvokeDelegate** アクティビティ デザイナーにアクセスします。 **InvokeDelegate** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 アクティビティ デザイナーをドロップすると、<xref:System.Activities.Statements.InvokeDelegate> アクティビティが InvokeDelegate の既定の <xref:System.Activities.Activity.DisplayName%2A> で作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**InvokeDelegate** アクティビティ デザイナーのヘッダーか、プロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-invokedelegate-properties"></a>InvokeDelegate プロパティ

次の表に、<xref:System.Activities.Statements.InvokeDelegate> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部はワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|<xref:System.Activities.Statements.InvokeDelegate> アクティビティの表示名。 既定値は InvokeDelegate です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は厳密には必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.InvokeDelegate.Delegate%2A>|True|アクティビティの実行時に呼び出す <xref:System.Activities.ActivityDelegate> の名前。 このプロパティは、デザイナー画面で設定できる必須のプロパティです。|
|<xref:System.Activities.Statements.InvokeDelegate.DelegateArguments%2A>|False|呼び出されたデリゲートの引数コレクション。 キーは <xref:System.Activities.ActivityDelegate> のパラメーター オブジェクトの名前であり、値は、式が評価され対応するパラメーター オブジェクトに割り当てられる引数です。 このプロパティを設定できる **[DelegateArguments]** ダイアログを表示するには、プロパティ グリッドで **[DelegateArguments]** フィールドの省略記号ボタンをクリックします。 **[引数の作成]** フィールドをクリックして引数を追加します。|

## <a name="see-also"></a>こちらもご覧ください

- [ワークフロー デザイナーでアクティビティ デリゲートを定義および使用する方法](../workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer.md)