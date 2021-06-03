---
title: SharePoint のアプリケーション ページの作成 | Microsoft Docs
description: SharePoint のアプリケーション ページを作成します。 アプリケーション ページは、SharePoint Web サイトで使用するために設計された ASP.NET Web ページです。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web pages
- SharePoint development in Visual Studio, content pages
- SharePoint development in Visual Studio, application pages
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9ecd6573573d76c3e47a2c87a4f455cb9890fb31
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949182"
---
# <a name="create-application-pages-for-sharepoint"></a>SharePoint のアプリケーション ページの作成
  "*アプリケーション ページ*" は、SharePoint Web サイトで使用するために設計された ASP.NET Web ページです。 アプリケーション ページは特殊な種類の ASP.NET ページです。 アプリケーション ページと標準の ASP.NET ページの主な違いは、アプリケーション ページに SharePoint マスター ページとマージされたコンテンツが含まれていることです。 マスター ページを使用すると、アプリケーション ページでサイト上の他のページと同じ外観と動作を共有することができます。

 Visual Studio では、デザイナーを使用してアプリケーション ページをデザインすることができます。 デザイナーには、マスター ページで定義されている各コンテンツ プレースホルダーのコンテンツ領域が表示されます。 これらのコンテンツ領域にコントロールをドラッグすることで、アプリケーション ページをデザインすることができます。

## <a name="application-pages"></a>アプリケーション ページ
 アプリケーション ページは、サーバー上のすべてのサイトで共有されます。一方、サイト ページは、1 つのサイトに固有です。 詳細については、「[SharePoint のページの種類](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))」を参照してください。

 既定では、SharePoint サイトを作成するときに表示されるページのほとんどは、サイト ページです。 サイト ページは、SharePoint ページ ライブラリに追加できます。 ユーザーは、SharePoint Designer などのツールを使用して、サイト ページをカスタマイズすることができます。 サイト ページで動的 Web パーツや Web パーツ ゾーンなどの機能をホストすることもできます。

 アプリケーション ページでは、これらのことは実行できません。 ただし、ページにカスタム コードを含める場合は、アプリケーション ページを作成することをお勧めします。 サイト ページにカスタム コードを追加することはできますが、ユーザーが SharePoint Designer などのツールを使用してページをカスタマイズすると、コードの実行が停止します。

> [!NOTE]
> Visual Studio には、SharePoint サイトのサイト ページを作成するのに役立つテンプレートは用意されていません。 詳細については、「[SharePoint のページの種類](/previous-versions/office/developer/sharepoint-2010/aa979592(v=office.14))」を参照してください。

## <a name="create-an-application-page"></a>アプリケーション ページを作成する
 アプリケーション ページを作成するには、SharePoint プロジェクトに "**アプリケーション ページ**" 項目を追加します。 アプリケーション ページを作成すると、Visual Studio によってプロジェクトに次のフォルダーが追加されます。

|Folder|説明|
|------------|-----------------|
|Layouts|SharePoint ファイル システムの _layouts 仮想ディレクトリにマップされます。|
|Layouts サブフォルダー|アプリケーション ページを構成するファイルが含まれています。 既定では、このフォルダーの名前はプロジェクトと同じです。 このフォルダーの名前は、いつでも変更できます。 プロジェクトを実行すると、Visual Studio によってこのフォルダーが SharePoint ファイル システムの _layouts 仮想ディレクトリに配置されます。|

 Visual Studio によってプロジェクトに次のファイルが追加されます。

|ファイル|説明|
|----------|-----------------|
|ASP.NET ページ ファイル ( *.aspx*)|ページを定義する XML マークアップが含まれています。|
|アプリケーション ページのコード ファイル|アプリケーション ページの背後にあるコードが含まれています。 このファイルには、イベントを処理するコードを追加します。|
|アプリケーション ページ デザイナーのコード ファイル|デザイナーによって生成されるコードが含まれています。 このファイルは直接編集しないでください。|

## <a name="design-and-debug-an-application-page"></a>アプリケーション ページをデザインおよびデバッグする
 Visual Studio のデザイナー ビューを使用して、アプリケーション ページの内容をデザインします。 このデザイナーは、プロジェクトのアプリケーション ページを開いたときに表示されます (ダブルクリックするか、ショートカット メニューを開いて **[開く]** を選択します)。その後、エディターの下部にある **[デザイン]** ボタンを選択します。

> [!NOTE]
> ページのデザインは、デザイナーの **ソース** ビューでのみ行うことができます。 デザイナーの **デザイン** ビューは、アプリケーション ページでは無効になっています。

 Visual Studio で他の SharePoint プロジェクト項目をデバッグする場合と同じように、アプリケーション ページをデバッグできます。 Visual Studio デバッガーを開始すると、SharePoint サイトが開きます。

 アプリケーション ページを表示するには、アプリケーション ページの場所 (例: http://<em>Server_Name</em>/_layouts/*Project_Name*/ApplicationPage1.aspx) に手動で移動する必要があります。

 SharePoint プロジェクトのデバッグ方法の詳細については、「[SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

## <a name="choose-a-master-page"></a>マスター ページを選択する
 既定では、"**アプリケーション ページ**" 項目は、プロジェクトのデバッグに使用しているサイトのマスター ページを参照します。 このページには「v4.master」という名前が付けられ、SharePoint サイトの "**マスター ページ ギャラリー**" にある一覧で確認できます。

 アプリケーション ページで使用されるマスター ページは、アプリケーション `Page` 要素の `MasterPageFile` 属性を設定することによって明示的に変更できます。 (例: `MasterPageFile="~/_layouts/applicationv4.master"`)。 実際、SharePoint サーバーで動的なマスター ページが有効になっていない場合は、この属性を設定する必要があります。 SharePoint のマスター ページの詳細については、「[マスター ページ](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint Foundation 開発の詳細](/previous-versions/office/developer/sharepoint-2010/ee539092(v=office.14))
- [ASP.NET 概要](/aspnet/overview)
- [ASP.NET Web ページ](/aspnet/web-pages/index)
