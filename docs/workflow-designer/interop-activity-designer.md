---
title: ワークフロー デザイナー - Interop アクティビティ デザイナー
description: Interop アクティビティ デザイナーについて、および Interop アクティビティ デザイナーを使用して Interop アクティビティを作成して構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Interop.UI
ms.assetid: 800a3403-ba86-41c4-8de1-c4fee9703eb1
author: jillre
ms.author: jillfra
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: edf4658743bb719c1c23f93b2d1d3cc33afdbaba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847389"
---
# <a name="interop-activity-designer"></a>Interop アクティビティ デザイナー

**Interop** アクティビティ デザイナーは、<xref:System.Activities.Statements.Interop> アクティビティを作成および構成するために使用します。

## <a name="the-interop-activity"></a>Interop アクティビティ

<xref:System.Activities.Statements.Interop> アクティビティでは、ワークフロー内の <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName> から派生する型の実行を管理します。

### <a name="use-the-interop-activity-designer"></a>Interop アクティビティ デザイナーの使用

**Interop** アクティビティ デザイナーは、 **[ツールボックス]** の **[移行]** カテゴリにあります。[ツールボックス] にアクセスするには、 **[ツールボックス]** タブをクリックします (または、 **[表示]** メニューの **[ツールボックス]** を選択するか、**Ctrl** キーと **Alt** キーを押しながら **X** キーを押します)。

プロジェクトの対象が .NET Framework 4 (完全版) 以降である場合は、 **[ツールボックス]** に、<xref:System.Activities.Statements.Interop> アクティビティを含む [[移行]](../workflow-designer/migration-activity-designers.md) カテゴリのみが表示されます。 必要に応じて、プロジェクトの対象となっているフレームワークのバージョンを変更できます。

**Interop** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティを通常配置しているワークフロー デザイナー画面の任意の場所 (<xref:System.Activities.Statements.Sequence> 内など) にドロップできます。 **Interop** アクティビティ デザイナーをドロップすると、Interop という既定の **DisplayName** を持つ <xref:System.Activities.Statements.Interop> アクティビティが作成されます。 <xref:System.Activities.Activity.DisplayName%2A> は、**Interop** アクティビティ デザイナーのヘッダーか、プロパティ グリッドの **[DisplayName]** ボックスで編集できます。

**Interop** アクティビティ デザイナーまたはプロパティ グリッドで、 **[ActivityType]** ボックスの **[クリックして参照]** というテキストをクリックして、 **[.NET 型の参照と選択]** ダイアログ ボックスを表示します。 ワークフロー 3.0 またはワークフロー 3.5 のアクティビティの型のみ表示されます。 つまり、<xref:System.Workflow.ComponentModel.Activity> から派生した型のみが表示されます。 このボックスを使用して型を特定する方法の詳細については、「[[.NET 型の参照と選択] ダイアログ ボックス](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box.md)」を参照してください。

### <a name="the-interop-properties"></a>Interop のプロパティ

次の表に、<xref:System.Activities.Statements.Interop> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはワークフロー デザイナー画面で編集できます。

|プロパティ名|必須|使用方法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|いいえ|<xref:System.Activities.Statements.Interop> アクティビティの表示名。 既定値は **Interop** です。 表示名は必須ではありませんが、指定することをお勧めします。|
|<xref:System.Activities.Statements.Interop.ActivityType%2A>|はい|<xref:System.Activities.Statements.Interop> アクティビティに含まれているアクティビティの型を指定します。 指定されたこの型は、<xref:System.Workflow.ComponentModel.Activity> から派生していることが必要です。|

## <a name="see-also"></a>関連項目

- [移行](../workflow-designer/migration-activity-designers.md)