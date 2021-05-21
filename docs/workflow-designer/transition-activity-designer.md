---
title: ワークフロー デザイナー - Transition アクティビティ デザイナー
description: Transition アクティビティ デザイナーを使用して、2 つの状態間の遷移を構成する方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Transition.UI
ms.assetid: f6e8b5cc-7fb8-4699-9703-f3c9fc7cc316
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 24a20ca9f7905adee3b7d0d83801d0033a1752ce
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875277"
---
# <a name="transition-activity-designer"></a>Transition アクティビティ デザイナー

<xref:System.Activities.Statements.Transition> は、2 つの状態間の遷移を表します。

## <a name="using-the-transition-activity-designer"></a>Transition アクティビティ デザイナーの使用

Transition アクティビティ デザイナーを使用すると、2 つの状態間の遷移を構成できます。

### <a name="transition-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Transition のプロパティ

次の表に、ワークフロー デザイナーを使用して設定できる <xref:System.Activities.Statements.Transition> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.Transition.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Transition> アクティビティ デザイナーの表示名を指定します。 既定値は **T1** です。 値は、プロパティ グリッド、展開された Transition デザイナーのヘッダー、および展開された Transition デザイナー内のアクション セクションのヘッダーで編集できます。 <xref:System.Activities.Activity.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Transition.Condition%2A>|いいえ|存在する場合、コントロールが遷移先の状態に渡される前に **True** と評価される必要がある式を指定します。 この条件は、プロパティ グリッドおよび展開された Transition デザイナーで編集できます。 共有遷移に含まれる複数の条件は、Transition デザイナーに表示される順に評価されます。 **注:** 遷移の <xref:System.Activities.Statements.Transition.Condition%2A> が **False** と評価された場合 (またはトリガーを共有する遷移すべての状態が **False** と評価された場合)、遷移は行われず、その状態からのすべての遷移のすべてのトリガーが再スケジュールされます。 このチュートリアルでは、条件の構成方法 (推定値が正しいか間違っているかを判断する特定のアクションが用意されています) により、この状況は発生しません。|
|**ソース**|はい|この遷移の発生元の状態を示します。 元の状態の名前をクリックすると、デザイナー ビューはその状態の展開ビューに切り替わります。 この値は、遷移が作成されていて、変更できない場合に設定されます。|
|<xref:System.Activities.Statements.Transition.Trigger%2A>|いいえ|完了時に遷移を開始するアクティビティを指定します。 このアクティビティを設定するには、 **[ツールボックス]** からアクティビティをドラッグし、遷移の **Trigger** セクションにドロップします。|
|<xref:System.Activities.Statements.Transition.Action%2A>|いいえ|Trigger アクティビティが完了し、<xref:System.Activities.Statements.Transition.Condition%2A> (存在する場合) が **true** と評価された場合に実行されるアクティビティを指定します。 このアクティビティは、元の状態の <xref:System.Activities.Statements.State.Exit%2A> アクティビティ (存在する場合) が実行された後、遷移先の状態に遷移するときに実行されます。 Transition デザイナーが展開されている場合、この値を設定するには、 **[ツールボックス]** からアクティビティをドラッグし、遷移の **Action** セクションにドロップします。 1 つの遷移に対して複数のアクションが存在する場合があります。 遷移内に複数のアクションがある場合は、アクションに表示される上向き矢印または下向き矢印をクリックすることで、個々のアクションの展開と折りたたみ、および並べ替えを実行できます。|
|**宛先**|はい|遷移の完了後にステート マシンが遷移した状態を示します。 これは、オブジェクト モデルにおける遷移の <xref:System.Activities.Statements.Transition.To%2A> プロパティに対応します。 遷移先の状態の名前をクリックすると、デザイナー ビューはその状態の展開ビューに切り替わります。 この値は、遷移が作成されたときに設定され、デザイナーで遷移を遷移先の状態に接続する矢印をドラッグすると変更できます。|

### <a name="creating-transitions"></a>遷移の作成

遷移を作成するには、ある状態から別の状態へ線をドラッグするか、ある状態を別の状態の上にドラッグすると表示される三角形に状態をドロップします。 ドラッグによって遷移を作成するには、元の状態の端にマウス ポインターを置き、元の状態から遷移先の状態に線をドラッグします。 ドロップによって遷移を作成するには、遷移先の状態をドラッグして元の状態の上にマウス ポインターを置き、元の状態の周囲に表示される 4 つの三角形のうち 1 つにドロップします。 遷移先の状態は、 **[ツールボックス]** からドラッグされた新しい状態と、ワークフロー デザイナーからドラッグされた既存の状態のいずれかになります。

> [!NOTE]
> ステート マシンの 1 つの状態では、ワークフロー デザイナーを使用して作成された遷移を最大 76 個まで含めることができます。 デザイナー以外で作成されたワークフローの状態の遷移に関する制限は、システム リソースによってのみ制限されます。

トリガーを共有する遷移とは、同じトリガー イベントを共有する遷移のセットです。 共有されるトリガーにより、共通のトリガー イベントを共有する複数の遷移用に構成された式の評価に基づいて、条件に従って遷移先の状態に移行することができます。 遷移に追加のアクションを追加して共有遷移を作成するには、目的の遷移の始点を表す円をクリックし、目的の状態にドラッグします。 新しい遷移では最初の遷移と同じトリガーが共有されますが、その条件とアクションは一意になります。 共有遷移は、遷移デザイナー内から作成することもできます。これには、遷移デザイナーの下部にある **[トリガーを共有する遷移の追加]** をクリックし、 **[接続の使用可能な状態]** ボックスの一覧で、目的となる対象の状態を選択します。

## <a name="see-also"></a>関連項目

- [StateMachine](../workflow-designer/statemachine-activity-designer.md)
- [FinalState](../workflow-designer/finalstate-activity-designer.md)
- [State](../workflow-designer/state-activity-designer.md)
