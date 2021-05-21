---
title: ワークフロー デザイナー-InvokeMethod アクティビティ デザイナー
description: InvokeMethod アクティビティについて、および InvokeMethod アクティビティ デザイナーを使用して InvokeMethod アクティビティを作成して構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2ba7234ee0c5a4ab8096c020cb44345f17830540
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931215"
---
# <a name="invokemethod-activity-designer"></a>InvokeMethod アクティビティ デザイナー

**InvokeMethod** デザイナーは、<xref:System.Activities.Statements.InvokeMethod> アクティビティを作成して構成するために使用します。

## <a name="the-invokemethod-activity"></a>InvokeMethod アクティビティ

<xref:System.Activities.Statements.InvokeMethod> は、指定されたオブジェクトまたは型のパブリック メソッドを呼び出します。

### <a name="use-the-invokemethod-activity-designer"></a>InvokeMethod アクティビティ デザイナーを使用する

**[ツールボックス]** の **[プリミティブ]** カテゴリで、**InvokeMethod** アクティビティ デザイナーにアクセスします。 **InvokeMethod** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 アクティビティ デザイナーをドロップすると、<xref:System.Activities.Statements.InvokeMethod> アクティビティが InvokeMethod の既定の <xref:System.Activities.Activity.DisplayName%2A> で作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**InvokeMethod** アクティビティ デザイナーのヘッダーか、プロパティ グリッドの **[DisplayName]** ボックスで編集できます。

### <a name="the-invokemethod-properties"></a>InvokeMethod のプロパティ

次の表に、<xref:System.Activities.Statements.InvokeMethod> のプロパティと、それらがデザイナーでどのように使用されるかを示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部はワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.InvokeMethod> アクティビティの表示名。 既定値は InvokeMethod です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は厳密には必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|はい|アクティビティの実行時に呼び出すメソッドの名前。 呼び出されるメソッドは、**public** と宣言する必要があります。 このプロパティは、デザイナー画面で設定できる必須のプロパティです。|
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|いいえ|呼び出されたメソッドのパラメーター コレクション。 パラメーターは、メソッド シグネチャ内で出現する順序でコレクションに追加する必要があります。 このプロパティを設定できる **[パラメーター]** ダイアログを表示するには、プロパティ グリッドで **[パラメーター]** フィールドの省略記号ボタンをクリックします。 **[引数の作成]** ボタンをクリックしてパラメーターを追加します。|
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|いいえ|メソッド呼び出しの戻り値。|
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|はい|メソッドが非同期で呼び出されるかどうかを指定します。 既定値は **False** です。|
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|いいえ|呼び出すメソッドを格納するオブジェクト。 このプロパティは、デザイナー画面で設定することもできます。<br /><br /> <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> および <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> のいずれかを設定する必要があります。|
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|いいえ|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> の型。 このプロパティは、デザイナー画面で編集できます。 このプロパティは、メソッド呼び出しが静的である場合にのみ設定する必要があります。|

パラメーターを C# の **out** パラメーターとして渡すには (例: `Method1(out myParam))`)、**InOutArgument** の代わりに **OutArgument** を使用します。

**TargetObject** または **Result** という引数があるメソッドは、<xref:System.Activities.Statements.InvokeMethod> アクティビティを使用して呼び出すことはできません。 これは、<xref:System.Activities.Statements.InvokeMethod> アクティビティによって <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A>、<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>、および <xref:System.Activities.Statements.InvokeMethod.Result%2A> が <xref:System.Activities.Activity.CacheMetadata%2A> に登録されるためです。

<xref:System.Activities.Activity.CacheMetadata%2A> にパラメーターを登録するアルゴリズムは次のとおりです。

1. <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 引数を登録します。

2. <xref:System.Activities.Statements.InvokeMethod.Result%2A> 引数を登録します。

3. <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> コレクションを繰り返し処理し、各引数を登録します。

結果の例外の種類は <xref:System.Activities.InvalidWorkflowException> となり、メッセージの内容は、"'InvokeMethod': 名前が 'TargetObject' の変数 RuntimeArgument または DelegateArgument は既に存在します" となります。 名前は、環境スコープ内で一意であることが必要です。

この制限は、<xref:System.Activities.Statements.InvokeMethod.TargetType%2A> と <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A> には適用されません。 これらはワークフロー引数ではないため、<xref:System.Activities.Activity.CacheMetadata%2A> メソッドでの <xref:System.Activities.Statements.InvokeMethod> アクティビティの <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> コレクションに登録されません。

## <a name="see-also"></a>関連項目

- [Primitives](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [[遅延]](../workflow-designer/delay-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)
