---
title: ワークフロー デザイナー - Switch&lt;T&gt; アクティビティ デザイナー
description: Switch<T> アクティビティ デザイナーを使用して、ワークフロー デザイナーで Switch<T> アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.ModelItemKeyValuePair.UI
- System.Activities.Statements.Switch`1.UI
ms.assetid: 18a6c96e-49a9-4356-ab61-fbd7e3ab44bb
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 35dcc390dcf58e02a2c7c1fa2dba62840d433785
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882311"
---
# <a name="switcht-activity-designer"></a>Switch\<T> アクティビティ デザイナー

<xref:System.Activities.Statements.Switch%601> アクティビティは、指定した式を評価します。そして、その評価から得られた値と一致する、関連付けられたキーを持つアクティビティを、アクティビティのコレクションから実行します。

**Switch<T\>** アクティビティ デザイナーは、ワークフロー デザイナーで <xref:System.Activities.Statements.Switch%601> アクティビティを作成および構成するために使用します。

## <a name="the-switchtactivity"></a>Switch\<T> アクティビティ

<xref:System.Activities.Statements.Switch%601> アクティビティには、<xref:System.Activities.Statements.Switch%601.Expression%2A> と、<xref:System.Activities.Statements.Switch%601.Cases%2A> のディクショナリが含まれます。 ディクショナリ内の各 case は、*key* と、その対応する *value* として機能するアクティビティのペアで構成されます。 <xref:System.Activities.Statements.Switch%601> アクティビティは、<xref:System.Activities.Statements.Switch%601.Expression%2A> を評価し、それを各キーと比較します。 一致が見つかった場合は、対応するアクティビティが実行されます。 見つかる一致は 1 つのみです。これは、ディクショナリ キーは、ディクショナリの等値比較子により定義される等価性の型に従って一意である必要があるためです。 一致が検出されない場合は、<xref:System.Activities.Statements.Switch%601.Default%2A> アクティビティが実行されます。

## <a name="how-to-use-the-switcht-activity-designer"></a>Switch\<T> アクティビティ デザイナーの使用方法

**[ツールボックス]** の **[制御フロー]** カテゴリにある **Switch\<T>** アクティビティ デザイナーにアクセスします。 それをワークフロー デザイナーにドロップすると、 **[型の選択]** ダイアログが表示され、ユーザーは <xref:System.Activities.Statements.Switch%601> アクティビティで使用されるジェネリック型 *T* を指定できます。 既定値は **Int32** です。 ジェネリック型 *T* を選択すると、**Switch<T\>** デザイナーがワークフロー デザイナーに追加されます。

**Switch<T\>** デザイナーには次のプロパティがあります。 これらのプロパティはすべて、プロパティ グリッドで編集できます。 一部のプロパティは、デザイナー画面で設定することもできます。

次の表に、最も役に立つ <xref:System.Activities.Statements.Switch%601> プロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Switch%601> アクティビティ デザイナーの表示名を指定します。 既定値は Switch<Int32\> です。 この値は、 **[プロパティ]** ウィンドウで編集することも、デザイナーのヘッダーで直接編集することもできます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Switch%601.Expression%2A>|はい|cases コレクション内のキーを比較して、実行する case を決定するために使用される式を指定します。|
|<xref:System.Activities.Statements.Switch%601.Default%2A>||一致が検出されなかった場合に実行するアクティビティを指定します。 デザイナーの **[アクティビティの追加]** ボタンをクリックすると、アクティビティをドロップできる **[既定値]** ボックスが表示されます。|
|<xref:System.Activities.Statements.Switch%601.Cases%2A>||評価する case を指定します。 case を追加するには、**Switch\<T>** デザイナーの下部にある **[新しい case の追加]** ボタンをクリックします。 ボタンがテキスト ボックス (Switch\<T> を追加するときに選択したジェネリック型が String または Enum である場合は、コンボ ボックス) に変わります。 **[Case 値]** ボックスにキーを追加すると、case の領域が展開され、"ここにアクティビティをドロップ" というヒント テキストが表示される位置にアクティビティをドロップして、case の実行ロジックを定義することができます。|

case キーが重複しない限り、複数の case を追加できます。 case キーが重複している場合は、エラー ダイアログが表示され、指定した case キーが既に存在しているために別のキーを選択する必要があることが示されます。 **Switch\<T>** デザイナーでは、一度に 1 つの case の領域のみが、展開されたビューに表示されます。 折りたたまれたビューに case の領域が表示されている場合は、case の領域をクリックすると展開されます。 case が折りたたまれており、この case 内にアクティビティが存在する場合は、このアクティビティの表示名が右側に表示されます。 アクティビティが存在しない場合は、 **[アクティビティの追加]** ボタンが表示されます。このボタンをクリックすると、case が展開され、アクティビティを追加できます。

既存の case のキーをクリックすると、キーがラベルからテキスト ボックスに変わり、case キーを編集できます。

case を削除する方法には、次の 2 つがあります。

- case を選択して削除します。

- case を選択し、右クリックしてコンテキスト メニューを表示し、 **[削除]** をクリックします。

case を削除するには、case 自体を選択する必要があることに注意してください。 case 内のアクティビティを選択して削除すると、case ではなく、アクティビティのみが削除されます。

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
