---
title: ParallelForEach&lt;T&gt; アクティビティ デザイナー
description: ワークフロー デザイナーで、ParallelForEach <T> アクティビティを使用して、コレクションの要素を列挙し、コレクションの各要素に対して埋め込みステートメントを並列で実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ParallelForEach`1.UI
ms.assetid: e93a4843-aef2-4d3e-9a0a-a2d3d1411aa7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4b35bcb6fcd1dc2ac3826d5dccb17ff764979321
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968750"
---
# <a name="parallelforeach-activity-designer"></a>ParallelForEach アクティビティ デザイナーの使用

<xref:System.Activities.Statements.ParallelForEach%601> アクティビティでは、コレクションの要素を列挙し、コレクションの各要素に対して埋め込みステートメントを並列的に (同じスレッドで非同期的に) 実行します。 このフロー制御アクティビティは、その子アクティビティがアイドル状態になると予想される場合に、<xref:System.Activities.Statements.Sequence> アクティビティの代わりに使用します。

<xref:System.Activities.Statements.ParallelForEach%601> アクティビティには、ユーザーによって指定された Visual Basic 式を保持する <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> プロパティがあります。 このプロパティは、各分岐の完了後に、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティによって評価されます。 評価結果が **true** の場合、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティは他の分岐を実行せずに完了します。 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> が **true** に評価されない場合、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティは、すべての子アクティビティが完了したときに完了します。

## <a name="the-parallelforeacht-activity"></a>ParallelForEach<T\> アクティビティ

<xref:System.Activities.Statements.ParallelForEach%601> では値が列挙され、列挙されているすべての値に対して <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がスケジュールされます。 スケジュールされるのは <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> のみです。 本文の実行方法は、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がアイドル状態になるかどうかによって異なります。

<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がアイドル状態にならない場合は、スケジュールされたアクティビティがスタックとして扱われるため、逆の順序で実行されます。つまり、最後にスケジュールされたアクティビティが最初に実行されます。 たとえば、コレクション {1,2,3,4} が <xref:System.Activities.Statements.ParallelForEach%601> 内にあるときに、本文として **WriteLine** を使用して値を書き出すとします。コンソールには、4、3、2、1 が出力されます。 これは、**WriteLine** がアイドル状態にならないことで 4 つの **WriteLine** アクティビティがスケジュールされた後、スタック動作 (先入れ後出し) に従って実行されたためです。

ただし、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> アクティビティや <xref:System.ServiceModel.Activities.Receive> アクティビティのように、アイドル状態になる可能性のあるアクティビティが <xref:System.Activities.Statements.Delay> に含まれている場合は、 それぞれのアクティビティが完了するまで待機する必要はありません。 <xref:System.Activities.Statements.ParallelForEach%601> は、スケジュールされている次の本文アクティビティに進み、実行を試みます。 そのアクティビティもアイドル状態になる場合は、<xref:System.Activities.Statements.ParallelForEach%601> が、さらに次の本文アクティビティに進みます。

### <a name="using-the-parallelforeacht-activity-designer"></a>ParallelForEach\<T> アクティビティ デザイナーの使用

**[ツールボックス]** の **[制御フロー]** カテゴリにある **ParallelForEach\<T>** アクティビティ デザイナーにアクセスします。

**ParallelForEach\<T>** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、通常アクティビティ デザイナーが配置されるワークフロー デザイナー サーフェス (**Sequence** アクティビティ デザイナーなど) にドロップできます。 ワークフロー デザイナーにドロップすると、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティが作成されます。それには、既定で **ParallelForEach<Int32\> の <xref:System.Activities.Activity.DisplayName%2A> が含まれています。**

### <a name="parallelforeacht-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの ParallelForEach<T\> のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.ParallelForEach%601> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|ヘッダーのアクティビティ デザイナーの表示名を指定します。 既定値は **ParallelForEach\<Int32>** です。 この値は、 **[プロパティ]** グリッドで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。|
|<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>|いいえ|コレクション内の各項目に対して実行するアクティビティ。 <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> アクティビティを追加するには、"ここにアクティビティをドロップします" というヒント テキストが表示された **ParallelForEach\<T>** アクティビティ デザイナーの **[Body]** ボックスに、[ツールボックス] からアクティビティをドロップします。|
|**TypeArgument**|はい|ジェネリック パラメーター *T* によって指定された <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> コレクション内の項目の型。既定では、**TypeArgument** は **Int32** に設定されます。 **ParallelForEach<T\>** アクティビティ デザイナーで型 T を変更するには、プロパティ グリッドの **[TypeArgument]** コンボ ボックスの値を変更します。|
|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>|はい|反復処理を行う項目のコレクション。 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> を設定するには、"VB の式を入力してください" というヒント テキストが表示された **ForEach<T\>** アクティビティ デザイナーの **[値]** ボックス、または **[プロパティ]** ウィンドウの **[値]** ボックスに、Visual Basic の式を入力します。|
|<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>||各イテレーションの完了後に評価されます。 true であると評価する場合、スケジュールされた保留イテレーションはキャンセルされます。 このプロパティが設定されていない場合、スケジュールされたすべてのステートメントは、完了するまで実行されます。|

既定では、ループ反復子には、item という名前が付けられます。 反復子変数の名前は、**ParallelForEach\<T>** アクティビティ デザイナーの **[ForEach]** ボックスで変更できます。 ループ反復子は、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティの子の式で使用できます。

## <a name="see-also"></a>関連項目

- [Sequence](../workflow-designer/sequence-activity-designer.md)
- [Parallel](../workflow-designer/parallel-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)