---
title: '方法: アプリケーション ページを作成する | Microsoft Docs'
description: 1 つまたは複数の SharePoint サイトに対して、Visual Studio で ASP.NET Web ページ (アプリケーション ページとも呼ばれます) を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], adding
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 74e7aab4cbc012afbf045672dbf4af248ada4c61
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925619"
---
# <a name="how-to-create-an-application-page"></a>方法: アプリケーション ページを作成する
  1 つまたは複数の SharePoint サイトに対して ASP.NET Web ページを作成できます。 SharePoint では、これらのページはアプリケーション ページと呼ばれます。 サイト ページとは異なり、アプリケーション ページには、ページの背後で実行されるコードが含まれています。 詳細については、[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)に関するページを参照してください。

### <a name="to-create-an-application-page"></a>アプリケーション ページを作成するには

1. Visual Studio で、SharePoint プロジェクトを開くか作成します。

     詳細については、「[SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

3. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

4. **[新しい項目の追加]** ダイアログ ボックスで、 **[SharePoint]** ノードを展開し、 **[2010]** 項目を選択します。

5. SharePoint テンプレートの一覧で、 **[アプリケーション ページ]** を選択します。

6. **[名前]** ボックスにアプリケーション ページの名前を入力し、 **[追加]** ボタンを選択します。

     複数のフォルダーとファイルがプロジェクトに追加されます。 これらのファイルの詳細については、「[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)」を参照してください。

     Visual Web Developer デザイナーの **ソース** ビューに、ASP.NET ページ ファイルが表示されます。 **ツールボックス** からコントロールを追加して、コンテンツ プレースホルダーに配置することで、ページをデザインできます。 詳細については、「[ソース ビュー、Web Page Designer](/previous-versions/aspnet/ms178154\(v\=vs.100\))」を参照してください。

7. コントロール イベントを処理する場合は、アプリケーション ページのコード ファイルにコードを追加します。

     コード ファイルは ASP.NET ページ ファイルのノードを展開した場合に表示され、プロジェクトの言語に応じて *.cs* または *.vb* の拡張子を持ちます。 アプリケーション ページを作成する方法のエンド ツー エンドの例については、「[チュートリアル: SharePoint アプリケーション ページの作成](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [チュートリアル: SharePoint アプリケーション ページの作成](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)
