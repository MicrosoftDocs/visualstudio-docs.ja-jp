---
title: '方法: SharePoint 接続を追加または削除する | Microsoft Docs'
description: Visual Studio の [サーバー エクスプローラー] ウィンドウの [SharePoint 接続] ノードを使用して、SharePoint 接続を追加または削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 57ff132274ba7f720a845078b0424fe235d9c31e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923458"
---
# <a name="how-to-add-or-remove-sharepoint-connections"></a>方法: SharePoint 接続を追加または削除する
  サーバー エクスプローラーを使用すると、データ接続だけでなく SharePoint サイトを参照することもできます。 ただし、SharePoint サイトのコンテンツを参照するには、 **[SharePoint 接続]** ノードに SharePoint サイトを追加する必要があります。

### <a name="to-add-a-sharepoint-site-to-the-sharepoint-connections-node"></a>Sharepoint サイトを SharePoint 接続ノードに追加するには

1. メニュー バーで、 **[表示]** 、 **[サーバー エクスプローラー]** を選択します。

2. **サーバー エクスプローラー** で、 **[SharePoint 接続]** ノードを選択し、メニュー バーで **[ツール]**  >  **[SharePoint 接続の追加]** の順に選択します。

3. **[SharePoint 接続の追加]** ボックスに、SharePoint サイトの [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] を入力します (たとえば、 http://testserver/sites/unittests) )。

### <a name="to-delete-a-sharepoint-site-from-the-sharepoint-connections-node"></a>SharePoint サイトを SharePoint 接続ノードから削除するには

1. メニュー バーで **[表示]** 、 **[サーバー エクスプローラー]** と選択して **サーバー エクスプローラー** を開きます。

2. **[SharePoint 接続]** ノードを展開して、**サーバー エクスプローラー** から削除したい SharePoint サイトを表示します。

3. サイトを選択し、メニューバーで **[編集**] >  **[削除]** を選択します。

    > [!NOTE]
    > この手順では、基になるサイトは削除されません。**サーバー エクスプローラー** からの接続のみが削除されます。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーを使用して SharePoint 接続を参照する](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
