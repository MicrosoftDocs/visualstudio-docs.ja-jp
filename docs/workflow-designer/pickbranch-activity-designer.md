---
title: ワークフロー デザイナー - PickBranch アクティビティ デザイナー
description: PickBranch アクティビティ デザイナーを使用して、受信イベントによってトリガー可能な Pick アクティビティ内のイベントベースの実行パスを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.PickBranch.UI
ms.assetid: f523ad47-bbc0-4cda-a35c-41e67c4ba081
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9d3ac314d5f8eb7980bdf5102d871546d3167141
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968672"
---
# <a name="pickbranch-activity-designer"></a>PickBranch アクティビティ デザイナー

<xref:System.Activities.Statements.PickBranch> は、受信イベントによってトリガー可能な、<xref:System.Activities.Statements.Pick> アクティビティ内のイベント ベースの実行パスを提供します。

## <a name="pickbranch"></a>PickBranch

<xref:System.Activities.Statements.PickBranch> オブジェクトは、<xref:System.Activities.Statements.Pick.Branches%2A> アクティビティの <xref:System.Activities.Statements.Pick> コレクションに格納されます。 各 <xref:System.Activities.Statements.PickBranch> は <xref:System.Activities.Statements.Pick> アクティビティの分岐に格納され、トリガーの役割を果たす受信イベントに応答して実行できます。 この方法で、ワークフロー デザイナーで、イベントベースの制御フロー モデリングを用意します。 各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> および <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。

### <a name="how-to-use-the-pick-activity-designer"></a>Pick アクティビティ デザイナーの使用方法

**[ツールボックス]** の **[制御フロー]** カテゴリにある **PickBranch** アクティビティ デザイナーにアクセスします。

**Pick** アクティビティ デザイナーをワークフロー デザイナーに初めてドロップすると、既定では、2 つの空の <xref:System.Activities.Statements.PickBranch> オブジェクト (表示名は **Branch1** と **Branch2**) が <xref:System.Activities.Statements.Pick> アクティビティの要素として作成されます。 それぞれの <xref:System.Activities.Statements.PickBranch.DisplayName%2A> プロパティの値は、**PickBranch** デザイナーのヘッダー内、または各分岐の **[プロパティ]** ウィンドウ内で編集できます。

<xref:System.Activities.Statements.PickBranch> オブジェクトを <xref:System.Activities.Statements.Pick> オブジェクトのコレクションに追加する方法は 2 つあります。 **[ツールボックス]** から **PickBranch** デザイナーをドラッグ アンド ドロップするか、**Pick** デザイン画面内から右クリックメニューを使用します。

- **PickBranch** デザイナーを **[ツールボックス]** からドラッグし、ワークフロー デザイナー画面上にある **Pick** アクティビティ デザイナーの分岐のいずれかにドロップすると、<xref:System.Activities.Statements.PickBranch> が作成されます。 新しい <xref:System.Activities.Statements.PickBranch> オブジェクトは、<xref:System.Activities.Statements.Pick> デザイナー内で、コレクションに含まれている既存の <xref:System.Activities.Statements.PickBranch> 要素の左側または右側に配置できます。 マウスを使用して **PickBranch** デザイナーを **Pick** デザイナー上にドラッグすると、**Pick** デザイナーには、マウス操作で追加された <xref:System.Activities.Statements.PickBranch> の位置が青灰色の縦の帯で示されます。

- **Pick** アクティビティ デザイナー (**PickBranch** デザイナーの内部ではない) を右クリックしてコンテキスト メニューを表示し、 **[分岐の作成]** をクリックして、新しい <xref:System.Activities.Statements.PickBranch> を追加します。 **Pick** デザイナー内の既存の <xref:System.Activities.Statements.PickBranch> オブジェクトの右側に新しい <xref:System.Activities.Statements.PickBranch> が追加されます。

**PickBranch** デザイナーは、ヘッダーの右側にある二重のキャレットをクリックすることで、 **[トリガー]** ボックスと **[アクション]** ボックスが表示されるように展開することも、折りたたむこともできます。 アクティビティをデザイナーの **[トリガー]** ボックスと **[アクション]** ボックスにドロップすることで、各 <xref:System.Activities.Statements.PickBranch> の <xref:System.Activities.Statements.PickBranch.Trigger%2A> と <xref:System.Activities.Statements.PickBranch.Action%2A> を編集します。

<xref:System.Activities.Statements.Pick> オブジェクトの <xref:System.Activities.Statements.Pick.Branches%2A> コレクションに含まれる <xref:System.Activities.Statements.PickBranch> オブジェクトを並べ替えるには、**Pick** デザイナー内の新しい位置にドラッグ アンド ドロップします。 **Pick** デザイナーには、マウス操作で追加された <xref:System.Activities.Statements.PickBranch> の位置が青灰色の縦の帯で示されます。

<xref:System.Activities.Statements.PickBranch> は 2 とおりの方法で削除できます。

- **PickBranch** デザイナーを選択して削除します。
- **PickBranch** デザイナーを選択し、右クリックしてコンテキスト メニューを表示し、 **[削除]** をクリックします。

**PickBranch** デザイナーを選択していることを確認してください。 **[トリガー]** ボックスまたは **[アクション]** ボックス内のいずれかのアクティビティを誤って選択すると、<xref:System.Activities.Statements.PickBranch> オブジェクトではなく、ボックス内のアクティビティが削除されます。

### <a name="pickbranch-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの PickBranch のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.PickBranch> のプロパティと、ワークフロー デザイナーでのそれらの使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Statements.PickBranch.DisplayName%2A>|いいえ|**PickBranch** デザイナーのヘッダーに表示されるフレンドリ名。 既定値は Branch です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.PickBranch.Trigger%2A>|はい|各 <xref:System.Activities.Statements.PickBranch> には、<xref:System.Activities.Statements.PickBranch.Trigger%2A> を呼び出すことのできる <xref:System.Activities.Statements.PickBranch.Action%2A> アクションが含まれます。|
|<xref:System.Activities.Statements.PickBranch.Action%2A>|いいえ|各 <xref:System.Activities.Statements.PickBranch> には、トリガーされたときに実行される <xref:System.Activities.Statements.PickBranch.Action%2A> が含まれます。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [Pick アクティビティ](/dotnet/framework/windows-workflow-foundation/pick-activity)
- [Pick アクティビティの使用](/dotnet/framework/windows-workflow-foundation/samples/using-the-pick-activity)