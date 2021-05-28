---
title: ワークフロー デザイナー - Flowchart アクティビティ デザイナー
description: Flowchart アクティビティを使用して、複雑なフロー制御を定義および管理するワークフローを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Flowchart.UI
- System.Activities.Statements.FlowStep.UI
- System.Activities.Core.Presentation.FlowStart.UI
ms.assetid: d5af2276-5215-4138-880a-cf2b90bbf3a0
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c9c46ae3dcc0063c7a2664e032fba14ce320af18
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961301"
---
# <a name="flowchart-activity-designer"></a>フローチャート アクティビティ デザイナー

<xref:System.Activities.Statements.Flowchart> アクティビティは、複雑なフロー制御を定義および管理するワークフローを作成するために使用します。 <xref:System.Activities.Statements.Flowchart> は、コードまたはワークフロー デザイナーを使用して作成できます。 このトピックでは、ワークフロー デザイナー エクスペリエンスを文書化しています。 ワークフロー デザイナーのワークフロー アクティビティ デザイナーを使用すると、ワークフローを自然な形で作成できます。

## <a name="the-flowchart-activity"></a>Flowchart アクティビティ

<xref:System.Activities.Statements.Flowchart> では、ワークフローの開始時に実行される一意の <xref:System.Activities.Statements.Flowchart.StartNode%2A> を指定します。また、リンクされた <xref:System.Activities.Statements.Flowchart.Nodes%2A> のネットワークを使用して、任意のループを作成したり、特定の時点で実行フローの経路をワークフロー内の任意のポイントへ移動したりします。

### <a name="using-the-flowchart-activity-designer"></a>Flowchart アクティビティ デザイナーの使用

**Flowchart** アクティビティ デザイナーは、 **[ツールボックス]** の **[フローチャート]** カテゴリにあります。ワークフロー デザイナーの **[ツールボックス]** タブをクリックすることでアクセスします。 または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** + **Alt**+ **X** キーを押します。

**Flowchart** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティ デザイナーを通常配置するワークフロー デザイナー画面の任意の場所に、ルート アクティビティとして、または他の制御フロー アクティビティの子としてドロップできます。 **Flowchart** アクティビティ デザイナーを空のワークフロー デザイナー画面にドロップした場合は、<xref:System.Activities.Statements.Flowchart> アクティビティが作成され、既定では、実行を開始する開始ノードが緑色の丸で示された展開されたビューで表示されます。 **Flowchart** アクティビティ デザイナーを別の制御フロー アクティビティにドロップした場合は、最小化されたビューで表示され、**Flowchart** アクティビティ デザイナーをダブルクリックすることで展開できます。 **Flowchart** アクティビティ デザイナー上には、他の制御フロー アクティビティを含め、 **[ツールボックス]** にある任意のアクティビティを直接ドラッグできます。

さまざまなアクティビティ デザイナーをワークフロー デザイナー キャンバスにドラッグした後、それらが表す <xref:System.Activities.Activity> オブジェクトを互いにリンクさせて、実行の順序を指定できます。 接続元アクティビティと接続先アクティビティの間のリンクを作成するには、接続元アクティビティのデザイナー上にマウス ポインターを置きます。これで、その両側に正方形のハンドルが表示されます。 そのハンドルのどちらかをクリックし、マウス ボタンを押したまま、接続先アクティビティをマウスでポイントしたときにその周りに同様に表示されるハンドルのどちらかにドラッグします。 マウス ボタンを放すと、この 2 つのアクティビティの間にリンクが作成されます。このリンクは、接続元デザイナーから接続先デザイナーへの矢印で表されます。

### <a name="flowchart-activity-properties"></a>Flowchart アクティビティのプロパティ

次の表に、<xref:System.Activities.Statements.Flowchart> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはデザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|ヘッダーのアクティビティ デザイナーの表示名を指定します。 既定値は Flowchart です。 この値は、 **[プロパティ]** ウィンドウで編集することも、アクティビティ デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Flowchart.Variables%2A>|いいえ|子アクティビティ間で状態を共有するために、この <xref:System.Activities.Statements.Flowchart> 内にスコープ設定された変数のコレクション。|
|<xref:System.Activities.Statements.Flowchart.StartNode%2A>|いいえ|<xref:System.Activities.Statements.FlowNode> の開始時に実行される <xref:System.Activities.Statements.Flowchart>。|
|<xref:System.Activities.Statements.Flowchart.Nodes%2A>|いいえ|<xref:System.Activities.Statements.FlowNode> 内の <xref:System.Activities.Statements.Flowchart> オブジェクトのコレクションが格納されます。|

## <a name="see-also"></a>関連項目

- [フローチャート](../workflow-designer/flowchart-activity-designers.md)
- [FlowDecision](../workflow-designer/flowdecision-activity-designer.md)
- [FlowSwitch\<T>](../workflow-designer/flowswitch-t-activity-designer.md)
