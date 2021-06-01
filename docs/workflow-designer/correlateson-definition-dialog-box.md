---
title: ワークフロー デザイナー - [CorrelatesOn の定義] ダイアログ ボックス
description: ワークフロー デザイナーの [CorrelatesOn] ダイアログ ボックスを使用して、Receive アクティビティの CorrelatesOn プロパティを編集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CorrelatesOnDefinition.UI
ms.assetid: 8b2b627a-f236-4479-aa09-525df65e3413
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b4f371da2570d5573ce84c7e29393889202ae940
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955542"
---
# <a name="correlateson-definition-dialog-box"></a>[CorrelatesOn の定義] ダイアログ ボックス

**[CorrelatesOn]** ダイアログ ボックスは、ワークフロー デザイナーで <xref:System.ServiceModel.Activities.Receive> アクティビティの <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> プロパティを編集するために使用されます。 詳細については、「[Receive アクティビティ デザイナー](../workflow-designer/receive-activity-designer.md)」を参照してください。

<xref:System.ServiceModel.Activities.Receive> アクティビティの間の相関関係によって、ワークフロー内でさまざまなサービス操作が相互に接続される方法が指定されます。

次の表に、 **[CorrelatesOn]** ダイアログ ボックスのユーザー インターフェイス (UI) 要素を示します。

|UI 要素|説明|
|-|-----------------|
|**CorrelatesWith**|適切なワークフロー インスタンスにメッセージをルーティングするために使用される <xref:System.ServiceModel.Activities.CorrelationHandle>。|
|**XPath クエリ**|受信メッセージから相関関係データを抽出するためのクエリを含む、キーと値のペア。 この値は <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A> プロパティに対応します。 XPath クエリは、<xref:System.ServiceModel.MessageQuerySet> オブジェクトに含まれます。|

## <a name="to-launch-the-correlateson-dialog-box"></a>[CorrelatesOn] ダイアログ ボックスを起動するには

**Receive** アクティビティ デザイナーは、 **[ツールボックス]** からドラッグして、アクティビティが通常配置される任意のワークフロー デザイナー画面にドロップできます。 アクティビティ デザイナーをドロップすると、Receive の既定の <xref:System.Activities.Activity.DisplayName%2A> を持つ <xref:System.ServiceModel.Activities.Receive> アクティビティが作成されます。 **[CorrelatesOn の定義]** ダイアログ ボックスを開くには、**Receive** アクティビティ デザイナーを選択し、プロパティ グリッドで、**CorrelatesOn** プロパティのコレクションというテキストの横にある省略記号ボタンを選択します。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Activities.Receive>
- [[関連付け初期化子の追加] ダイアログ ボックス](../workflow-designer/add-correlationinitializers-dialog-box.md)
- [[関連付け初期化] ダイアログ ボックス](../workflow-designer/initialize-correlation-dialog-box.md)