---
title: '方法: プロジェクト出力参照を追加する | Microsoft Docs'
description: SharePoint 以外のプロジェクト アセンブリ (または Silverlight プロジェクトの .xap ファイル) を SharePoint に配置できるように、プロジェクト出力参照を追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c79c3d19dbd4b72bab9facdd81542fdc0620e1a2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965864"
---
# <a name="how-to-add-a-project-output-reference"></a>方法: プロジェクト出力参照を追加する
  SharePoint 以外のプロジェクト アセンブリ (または Silverlight プロジェクトの .xap ファイル) を SharePoint に配置するには、それらをプロジェクト出力参照として追加します。

 このプロセスでは、2 つのプロジェクト間のソリューション ビルド依存関係を作成します。 プロジェクト出力参照に関連付けられているプロジェクトは、SharePoint プロジェクトのビルドと配置の前にビルドされます。

### <a name="to-add-a-project-output-reference"></a>プロジェクト出力参照を追加するには

1. 少なくとも 1 つの SharePoint プロジェクトと 1 つの SharePoint 以外のプロジェクトが含まれているソリューションを読み込みます。

2. **ソリューション エクスプローラー** で、SharePoint プロジェクト ノード内の項目を選択します。

3. **[プロパティ]** ウィンドウで、 **[プロジェクト出力参照]** プロパティを選択し、その横にある省略記号 (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンを選択します。

4. **[プロジェクト出力参照]** ダイアログ ボックスで、 **[追加]** をクリックします。

5. [プロパティ] ウィンドウで、 **[配置の種類]** プロパティの横にある矢印を選択し、参照している SharePoint 以外の項目 (**ElementFile** など) に適切な値を選択します。

6. **[プロジェクト名]** の横にある矢印を選択し、SharePoint 以外のプロジェクト項目の名前を選択して、 **[OK]** を選択します。

## <a name="see-also"></a>関連項目
- [プロジェクト項目でのパッケージ化と配置の情報を提供する](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [方法: コントロールを安全なコントロールとしてマークする](../sharepoint/how-to-mark-controls-as-safe-controls.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
