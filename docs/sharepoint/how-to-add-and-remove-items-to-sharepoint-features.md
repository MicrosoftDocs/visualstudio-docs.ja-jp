---
title: '方法: SharePoint 機能の項目を追加および削除する | Microsoft Docs'
description: Visual Studio のフィーチャー デザイナーを使用して、SharePoint プロジェクト項目を SharePoint 機能に手動で追加および削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f18c46bb7bab2acd1d97e3154b53ab8ca52520e3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923466"
---
# <a name="how-to-add-and-remove-items-to-sharepoint-features"></a>方法: SharePoint 機能の項目を追加および削除する
  SharePoint ソリューションを作成すると、Visual Studio によって既定の SharePoint プロジェクト項目が機能に追加されます。 配置の前に、SharePoint プロジェクトの項目を追加および削除して、SharePoint フィーチャーを変更することができます。

## <a name="add-sharepoint-project-items-to-a-feature"></a>SharePoint プロジェクト項目をフィーチャーに追加する

#### <a name="to-add-sharepoint-project-items-with-the-feature-designer"></a>フィーチャー デザイナーを使用して SharePoint プロジェクト項目を追加するには

1. フィーチャー デザイナーを開きます。

    詳細については、「[方法:SharePoint フィーチャーをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-feature.md)」を参照してください。

2. 次の手順の 1 つ以上を実行して、 **[ソリューション内の項目]** 一覧から **[フィーチャー内の項目]** 一覧に 1 つ以上の項目を追加します。

   - 追加する各項目をダブルクリックします。

   - 追加する項目を選択し、 **[追加]** ボタン (>) を選択します。

   - **[すべて追加]** ボタン (>>) を選択します。

     SharePoint プロジェクト項目は、 **[フィーチャー内の項目]** 一覧に表示されます。

## <a name="remove-sharepoint-project-items-from-a-feature"></a>フィーチャーから SharePoint プロジェクト アイテムを削除する

#### <a name="to-remove-sharepoint-items-with-the-feature-designer"></a>フィーチャー デザイナーを使用して SharePoint 項目を削除するには

1. **[フィーチャー内の項目]** 一覧で 1 つ以上の項目を選択します。

2. **[削除]** ボタン (<) を選択して、一度に 1 つの項目を削除するか、 **[すべて削除]** ボタン (<<) を選択してすべての項目を削除します。

     SharePoint プロジェクト項目が、 **[ソリューション内の項目]** 一覧に表示されます。

## <a name="see-also"></a>関連項目
- [SharePoint フィーチャーを作成する](../sharepoint/creating-sharepoint-features.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
