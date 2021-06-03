---
title: '方法: SharePoint プロジェクトに項目を追加する | Microsoft Docs'
description: SharePoint ソリューションを開いたり作成したりした後、Visual Studio で新規または既存の項目を SharePoint プロジェクトに追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4a32d38b20b93cf215cb53c2c2d2b8767418de24
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923485"
---
# <a name="how-to-add-items-to-a-sharepoint-project"></a>方法: SharePoint プロジェクトに項目を追加する
  SharePoint ソリューションには 1 つ以上のプロジェクトが含まれており、それぞれに複数の SharePoint プロジェクト項目が含まれています。 SharePoint ソリューションを開いたり作成したりした後、これらのプロジェクトに新規または既存の項目を追加できます。 たとえば、新しいワークフロー プロジェクトには default.aspx という名前の既定のフォームが付属していますが、そのフォームを新しい形式または別の形式に置き換えることも、別の ASPX フォームを追加することもできます。

### <a name="to-add-a-new-project-item-to-a-sharepoint-solution"></a>SharePoint ソリューションに新しいプロジェクト項目を追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、SharePoint ソリューションを開くか作成します。

2. **ソリューション エクスプローラー** で、プロジェクトのノードを選択します。

3. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択して、 **[新しい項目の追加]** ダイアログ ボックスを表示します。

4. **[インストールされたテンプレート]** の一覧で **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

5. プロジェクト項目テンプレートの一覧で、テンプレートを選択します。

6. **[名前]** ボックスに名前を入力し、 **[OK]** ボタンを選択します。

### <a name="to-add-an-existing-project-item-to-a-sharepoint-solution"></a>SharePoint ソリューションに既存のプロジェクト項目を追加するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、SharePoint ソリューションを開くか作成します。

2. **ソリューション エクスプローラー** で、プロジェクトのノードを選択します。

3. メニュー バーで **[プロジェクト]**  >  **[既存の項目の追加]** を選択して、 **[既存の項目の追加]** ダイアログ ボックスを表示します。

4. 追加する項目が含まれているフォルダーを参照して選択し、 **[追加]** ボタンを選択します。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
