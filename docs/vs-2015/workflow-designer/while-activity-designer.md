---
title: While アクティビティ デザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.While.UI
ms.assetid: ea008091-2e4c-4f64-bfa5-afb919552446
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 36752df3d8ffbf33b8ea95570d6a4efe8c8cd3be
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973588"
---
# <a name="while-activity-designer"></a>While アクティビティ デザイナー

<xref:System.Activities.Statements.While>アクティビティに含まれるアクティビティを実行します。 その<xref:System.Activities.Statements.While.Body%2A>に指定された条件の評価中に**true**します。 場合によっては、含まれているアクティビティが実行されない可能性があります。 含まれているアクティビティを少なくとも 1 回は実行する必要がある場合は、<xref:System.Activities.Statements.DoWhile> アクティビティを代わりに使用します。

## <a name="while-properties-in-workflow-designer"></a>ワークフロー デザイナーでの While のプロパティ

次の表に、最も役に立つ <xref:System.Activities.Statements.While> アクティビティのプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必須|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|False|ヘッダーの <xref:System.Activities.Statements.While> アクティビティ デザイナーの表示名を指定します。 既定値は While です。 値を編集できる、**プロパティ**ウィンドウまたは直接アクティビティ デザイナーのヘッダー。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.While.Body%2A>|False|実行するアクティビティが含まれています中に、<xref:System.Activities.Statements.While.Condition%2A>に評価される**true**します。|
|<xref:System.Activities.Statements.While.Condition%2A>|True|[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] に含まれるアクティビティを実行するかどうかを決定するために評価される <xref:System.Activities.Statements.While.Body%2A> の式が含まれます。|

## <a name="see-also"></a>関連項目

- [制御フロー](../workflow-designer/control-flow-activity-designers.md)
- [DoWhile](../workflow-designer/dowhile-activity-designer.md)