---
title: ワークフロー デザイナーの ParallelForEach&lt;T&gt;アクティビティ デザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.ParallelForEach`1.UI
ms.assetid: e93a4843-aef2-4d3e-9a0a-a2d3d1411aa7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: be522112dd4cfa16744d0c9e54601ba7a0492704
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004229"
---
# <a name="parallelforeach-activity-designer"></a>ParallelForEach アクティビティ デザイナー

<xref:System.Activities.Statements.ParallelForEach%601> アクティビティでは、コレクションの要素を列挙し、コレクションの各要素に対して埋め込みステートメントを並列的に (同じスレッドで非同期的に) 実行します。 このフロー制御アクティビティは、その子アクティビティがアイドル状態になると予想される場合に、<xref:System.Activities.Statements.Sequence> アクティビティの代わりに使用します。

<xref:System.Activities.Statements.ParallelForEach%601>アクティビティには、<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>ユーザーを含むプロパティは、Visual Basic の式を指定します。 このプロパティは、各分岐の完了後に、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティによって評価されます。 評価されると、 **true**、<xref:System.Activities.Statements.ParallelForEach%601>アクティビティが他の分岐を実行せずに完了します。 場合、<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>に評価されない**true**、<xref:System.Activities.Statements.ParallelForEach%601>アクティビティのすべての子アクティビティが完了したときに完了します。

## <a name="the-parallelforeacht-activity"></a>ParallelForEach < T\>アクティビティ

<xref:System.Activities.Statements.ParallelForEach%601> はそれ自体の値を列挙し、列挙した値ごとに <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> をスケジュールします。 スケジュールされるのは <xref:System.Activities.Statements.ParallelForEach%601.Body%2A> のみです。 本文の実行方法は、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がアイドル状態になるかどうかによって異なります。

<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> がアイドル状態にならない場合は、スケジュールされたアクティビティがスタックとして扱われるため、逆の順序で実行されます。つまり、最後にスケジュールされたアクティビティが最初に実行されます。 コレクションがある場合など{1,2,3,4}で<xref:System.Activities.Statements.ParallelForEach%601>を使用して、 **WriteLine**値を書き込む本文として。この場合は、4、3、2、1 の順にコンソールに出力されます。 これは、ため**WriteLine** 4 の後にアイドル状態のためには説明しません**WriteLine**アクティビティがスケジュールされた、スタックの動作を使用してを実行する (最初の出し)。

ただし、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A> アクティビティや <xref:System.ServiceModel.Activities.Receive> アクティビティのように、アイドル状態になる可能性のあるアクティビティが <xref:System.Activities.Statements.Delay> に含まれている場合は、 それぞれのアクティビティが完了するまで待機する必要はありません。 <xref:System.Activities.Statements.ParallelForEach%601> は、スケジュールされている次の本文アクティビティに進み、実行を試みます。 そのアクティビティもアイドル状態になる場合は、<xref:System.Activities.Statements.ParallelForEach%601> が、さらに次の本文アクティビティに進みます。

### <a name="using-the-parallelforeacht-activity-designer"></a>ParallelForEach を使用して\<T > アクティビティ デザイナー

アクセス、 **ParallelForEach\<T >** 内のアクティビティ デザイナー、**制御フロー**のカテゴリ、**ツールボックス**します。

**ParallelForEach\<T >** からアクティビティ デザイナーをドラッグすることができます、**ツールボックス**アクティビティ デザイナーは、通常、任意の場所は、ワークフロー デザイナー画面にドロップしてのたとえば、内部の**シーケンス**アクティビティ デザイナー。 ワークフロー デザイナーにドロップすると、作成、<xref:System.Activities.Statements.ParallelForEach%601>を既定で含む、アクティビティ、<xref:System.Activities.Activity.DisplayName%2A>の**ParallelForEach < Int32\>します。**

### <a name="parallelforeacht-properties-in-the-workflow-designer"></a>ParallelForEach < T\>ワークフロー デザイナーでのプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.ParallelForEach%601> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|False|ヘッダーのアクティビティ デザイナーの表示名を指定します。 既定値は**ParallelForEach\<Int32 >** します。 値を必要に応じて編集、**プロパティ**グリッドまたは直接アクティビティ デザイナーのヘッダー。|
|<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>|False|コレクション内の各項目に対して実行するアクティビティ。 追加する、<xref:System.Activities.Statements.ParallelForEach%601.Body%2A>アクティビティ、アクティビティをツールボックスからドロップ、**本文**ボックスに、 **ParallelForEach\<T >** アクティビティ デザイナーの「ドロップ アクティビティここ」ヒント テキスト。|
|**TypeArgument**|True|内の項目の種類、<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>ジェネリック パラメーターで指定されたコレクション*T*します。既定では、 **TypeArgument**に設定されている**Int32**します。 型 T を変更する、 **ParallelForEach < T\>** アクティビティ デザイナーの値を変更、 **TypeArgument**プロパティ グリッドのコンボ ボックス。|
|<xref:System.Activities.Statements.ParallelForEach%601.Values%2A>|True|反復処理を行う項目のコレクション。 設定する、 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A>、Visual Basic の式を入力、**値**ボックスに、 **ForEach < T\>**  または「VBの式を入力してください」ヒントテキストボックスに、アクティビティデザイナー**値**ボックスに、**プロパティ**ウィンドウ。|
|<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>||各イテレーションの完了後に評価されます。 true であると評価する場合、スケジュールされた保留イテレーションはキャンセルされます。 このプロパティが設定されていない場合、スケジュールされたすべてのステートメントは、完了するまで実行されます。|

既定では、ループ反復子には、item という名前が付けられます。 反復子変数の名前を変更することができます、 **ForEach**ボックス**ParallelForEach\<T >** アクティビティ デザイナー。 ループ反復子は、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティの子の式で使用できます。

## <a name="see-also"></a>関連項目

- [Sequence](../workflow-designer/sequence-activity-designer.md)
- [Parallel](../workflow-designer/parallel-activity-designer.md)
- [制御フロー](../workflow-designer/control-flow-activity-designers.md)