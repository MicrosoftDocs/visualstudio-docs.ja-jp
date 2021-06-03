---
title: 'パッケージ デザイナー: パッケージのフィーチャーおよび項目を追加および削除する'
titleSuffix: ''
description: Visual Studio のパッケージ デザイナーを使用して、SharePoint パッケージのフィーチャーおよび項目を追加および削除する方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerDesign
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
ms.openlocfilehash: 92503d8e29bac4f44df5376f3cecb24247b585d6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923595"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer"></a>方法: パッケージ デザイナーを使用してパッケージのフィーチャーおよび項目を追加および削除する
  SharePoint ソリューションを作成すると、Visual Studio によって既定の SharePoint フィーチャーがソリューションのパッケージに追加されます。 最終的なデプロイの前に、SharePoint プロジェクトの項目とフィーチャーを追加および削除して、SharePoint パッケージを変更することができます。

 または、パッケージング エクスプローラーを使用して、SharePoint プロジェクト項目を追加および削除することもできます。 また、パッケージ (.wsp) に配置される SharePoint プロジェクト項目とフィーチャーの階層を表示および変更することもできます。 詳細については、「[方法: パッケージング エクスプローラーを使用してパッケージのフィーチャーおよび項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)」を参照してください。

## <a name="add-features-to-a-sharepoint-package"></a>SharePoint パッケージにフィーチャーを追加する
 パッケージ デザイナーを使用すると、SharePoint パッケージにフィーチャーを追加できます。

#### <a name="to-add-sharepoint-features-with-the-package-designer"></a>パッケージ デザイナーを使用して SharePoint フィーチャーを追加するには

1. **パッケージ デザイナー** を開きます。

    詳細については、「[方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)」を参照してください。

2. 次の手順のうち 1 つまたは複数を実行して、1 つまたは複数の SharePoint フィーチャーを追加します。

   1. **[ソリューション内の項目]** 一覧で、追加する項目をダブルクリックします。

   2. 追加する項目を選択し、 **[追加]** ボタン (>) を選択します。

   3. すべての項目を一度に追加するには、 **[すべて追加]** ボタン (>>) を選択します。

      たとえば、 **[ソリューション内の項目]** 一覧内の項目をダブルクリックして、 **[パッケージ内の項目]** 一覧に追加することができます。

      SharePoint プロジェクト項目とフィーチャーが、 **[パッケージ内の項目]** 一覧に表示されます。

## <a name="remove-features-from-a-sharepoint-package"></a>SharePoint パッケージからフィーチャーを削除する
 パッケージ デザイナーを使用すると、SharePoint パッケージに対してフィーチャーを削除できます。

#### <a name="to-remove-sharepoint-features-with-the-package-designer"></a>パッケージ デザイナーを使用して SharePoint フィーチャーを削除するには

1. **[パッケージ内の項目]** 一覧で、削除する項目を選択して **[削除]** ボタン (<) を選択するか、 **[すべて削除]** ボタン (<<) を選択してすべての項目を削除します。

     SharePoint 項目が、 **[ソリューション内の項目]** 一覧に表示されます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューション パッケージを作成する](../sharepoint/creating-sharepoint-solution-packages.md)
- [方法: SharePoint ソリューション パッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージを作成する](/previous-versions/ee231585(v=vs.110))