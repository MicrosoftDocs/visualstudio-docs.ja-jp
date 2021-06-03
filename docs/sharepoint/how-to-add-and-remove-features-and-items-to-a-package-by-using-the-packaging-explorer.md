---
title: 'パッケージ エクスプローラー: パッケージのフィーチャーおよび項目を追加および削除する'
titleSuffix: ''
description: Visual Studio のパッケージ エクスプローラーを使用して、SharePoint パッケージのフィーチャーおよび項目を追加および削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackagingExplorer
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: eec1468fc2e0c51d7dea7aa5f3ffa808b484ec87
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923570"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>方法: パッケージング エクスプローラーを使用してパッケージのフィーチャーおよび項目を追加および削除する
  SharePoint の項目とフィーチャーを配置するようにパッケージを構成するには、パッケージング エクスプローラーを使用します。 SharePoint プロジェクトの項目と機能は、.wsp ファイル内で調整できます。

 または、パッケージング デザイナーを使用して、フィーチャーを表示して順序を変更し、アクティベーションの順序を変更することもできます。 詳細については、「[方法: パッケージ デザイナーを使用してパッケージの機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)」を参照してください。

## <a name="open-the-packaging-explorer"></a>パッケージング エクスプローラーを開く
 Visual Studio ソリューションに少なくとも 1 つの SharePoint プロジェクトがある場合は、次の手順を使用して、パッケージング エクスプローラーを開くことができます。 また、フィーチャーまたはパッケージ デザイナーを表示すると、パッケージング エクスプローラーが自動的に開きます。 すべてのフィーチャーとパッケージ デザイナーを閉じると、パッケージング エクスプローラーも閉じます。

#### <a name="to-open-the-packaging-explorer"></a>パッケージング エクスプローラーを開くには

1. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[パッケージング エクスプローラー]** を選択します。

     **パッケージ エクスプローラー** が **[ツールボックス]** に表示されます。

## <a name="adding-a-feature-to-a-package"></a>パッケージにフィーチャーを追加する
 パッケージング エクスプローラーを使用して、パッケージに新規および既存のフィーチャーを追加できます。

#### <a name="to-add-a-sharepoint-feature"></a>SharePoint フィーチャーを追加するには

1. **パッケージ エクスプローラー** を開き、プロジェクトのショートカット メニューを開き、 **[フィーチャーの追加]** を選択します。

#### <a name="to-move-an-existing-sharepoint-feature"></a>既存の SharePoint フィーチャーを移動するには

1. **パッケージング エクスプローラー** を開き、次のいずれかの手順を実行します。

    - **フィーチャー** をあるプロジェクトから別のプロジェクトにドラッグします。

    - フィーチャーのショートカット メニューを開き、 **[切り取り]** を選択し、フィーチャーの移動先となるプロジェクトのショートカット メニューを開き、 **[貼り付け]** を選択します。

    > [!NOTE]
    > ソリューションに複数の SharePoint プロジェクトがある場合は、この手順を使用します。

## <a name="validate-a-feature-or-package"></a>フィーチャーまたはパッケージを検証する
 SharePoint のフィーチャーとパッケージで、ファイルを検証することにより潜在的な問題を特定できます。 警告とエラーは、[出力] ウィンドウと [エラー一覧] ウィンドウに表示されます。

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>SharePoint のフィーチャーまたはパッケージを検証するには

1. **パッケージング エクスプローラー** を開きます。

2. フィーチャーまたはパッケージのショートカット メニューを開き、 **[検証]** を選択します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
