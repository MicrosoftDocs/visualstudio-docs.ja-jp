---
title: '方法: リソース ファイルを追加する | Microsoft Docs'
description: ソリューション エクスプローラーのソリューション ノードとフィーチャー ノードでショートカット メニューのコマンドを使用して、Visual Studio にリソース ファイルを追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- resource files [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, resource files
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 22b5638f7251b34c74da348e55e755cd27132aff
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934846"
---
# <a name="how-to-add-a-resource-file"></a>方法: リソース ファイルを追加する
  リソース ファイルを追加するためのコマンドは、ソリューション エクスプローラーのソリューション ノードとフィーチャー ノードのショートカット メニューにあります。 詳細については、「[SharePoint ソリューションのローカライズ](../sharepoint/localizing-sharepoint-solutions.md)」を参照してください。

### <a name="to-add-a-global-resource-file-to-a-sharepoint-solution"></a>SharePoint ソリューションにグローバル リソース ファイルを追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、SharePoint ソリューションを開きます。

2. **ソリューション エクスプローラー** で、SharePoint プロジェクト ノードを選択します。次に、メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択します。

3. **[新しい項目の追加]** ダイアログ ボックスで **[グローバル リソース ファイル]** テンプレートを選択し、次に **[追加]** ボタンを選択します。

   > [!NOTE]
   > [グローバル リソース ファイル] プロジェクト項目テンプレートは、SharePoint プロジェクト項目が選択されている場合にのみ表示されます。

4. **[リソースの追加]** ダイアログ ボックスで、リソース ファイルのカルチャ ([英語 (米国)] など) を選択します。

    この手順では、Resource_x_ **.** <<em>カルチャ</em>><strong>.</strong>resx の形式でグローバル リソース ファイルをソリューションに追加します (*Resource1.en-US.resx* など)。

5. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で **リソース エディター** が開いたら、リソース ファイルにリソースを追加します。

### <a name="to-add-a-feature-resource-file-to-a-sharepoint-feature"></a>フィーチャー リソース ファイルを SharePoint フィーチャーに追加するには

1. SharePoint ソリューションが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でまだ開いていない場合は、ソリューションを開きます。

2. **ソリューション エクスプローラー** で、 **[フィーチャー]** ノードの下にあるフィーチャーの名前のショートカット メニューを開き、 **[フィーチャー リソースの追加]** を選択します。

     この手順では、<_リソース ファイル名_> **.** <_カルチャ_> **.resx** の形式でリソース ファイルをフィーチャーに追加します (*Feature1.en-US.resx* など)。

3. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で **リソース エディター** が開いたら、リソース ファイルにリソースを追加します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
