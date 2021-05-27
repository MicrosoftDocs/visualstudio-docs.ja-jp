---
title: ワークフロー デザイナー - [関連付けの初期化] ダイアログ ボックス
description: ワークフロー デザイナーの [関連付けの初期化] ダイアログ ボックスを使用して、InitializeCorrelation アクティビティの CorrelationData プロパティを編集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- InitializeCorrelation.UI
ms.assetid: 2a0a1cd3-7b9e-493e-9264-fcf85289ffcf
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a41511f9bfb381eeb422cc9cf7ec015d55ceff70
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931514"
---
# <a name="initialize-correlation-dialog-box"></a>[関連付け初期化] ダイアログ ボックス

**[関連付けの初期化]** ダイアログ ボックスは、ワークフロー デザイナーで <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティの <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> プロパティを編集するために使用されます。 詳細については、[InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md) に関するページを参照してください。

**[関連付けの初期化]** ダイアログ ボックスのユーザー インターフェイス (UI) 要素を次の表に示します。

|UI 要素|説明|
|-|-----------------|
|**相関関係**|初期化する関連付けの <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**初期化**|初期化するデータが格納されているキー/値ペア。 この値は <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> プロパティに対応しています。 有効なキーと値ペアには、"OrderID" という名前のキーと、OrderID という名前の変数のペアなどがあります。|

## <a name="to-launch-the-initialize-correlation-dialog-box"></a>[関連付け初期化] ダイアログ ボックスを開くには

**InitializeCorrelation** アクティビティ デザイナーで **[表示]** をクリックするか、ワークフロー デザイナーで <xref:System.ServiceModel.Activities.InitializeCorrelation> アクティビティを選択します。 次に、プロパティ グリッドの <xref:System.ServiceModel.Activities.InitializeCorrelation.CorrelationData%2A> プロパティの横にある省略記号ボタンをクリックします。

## <a name="see-also"></a>関連項目

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
