---
title: SharePoint アプリ ページまたは Web パーツのユーザー コントロールを作成する
titleSuffix: ''
description: SharePoint ソリューション向けの独自の機能を備えたカスタム ユーザー コントロールを作成し、その機能を Web パーツまたはアプリケーション ページ内で再利用します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- user controls [SharePoint development in Visual Studio], adding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 43386f3ba450058d6aaf8ab180e331d2f303a235
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925585"
---
# <a name="how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part"></a>方法: SharePoint アプリケーション ページまたは Web パーツのユーザー コントロールを作成する
  SharePoint ソリューション向けの独自の機能を備えたカスタム ユーザー コントロールを作成し、その機能をプロジェクト内で再利用することができます。 ユーザー コントロールは、Web パーツまたはアプリケーション ページに含めることができます。他の ASP.NET コントロールや SharePoint コントロールを追加し、コントロールのプロパティとメソッドを定義することもできます。 ユーザー コントロールの詳細については、「[Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)」と「[SharePoint のユーザー コントロールとサーバー コントロール](https://blogs.msdn.microsoft.com/kaevans/2011/04/28/user-controls-and-server-controls-in-sharepoint/)」を参照してください。

### <a name="to-create-a-user-control-for-sharepoint"></a>SharePoint のユーザー コントロールを作成するには

1. Visual Studio で、SharePoint プロジェクトを開くか作成します。

     「[SharePoint のプロジェクト テンプレートとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

3. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが開きます。

4. **[インストール済み]** ペインで、 **[Office/SharePoint]** ノードを選択します。

5. SharePoint テンプレートの一覧で、 **[ユーザー コントロール (ファーム ソリューションのみ)]** を選択します。

    > [!NOTE]
    > ユーザー コントロールはファーム ソリューションでのみ機能します。

6. **[名前]** ボックスにユーザー コントロールの名前を入力し、 **[追加]** ボタンを選択します。

     複数のフォルダーとファイルがプロジェクトに追加されます。 これらのファイルの詳細については、「[Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)」を参照してください。

     既定で、Visual Web Developer デザイナーの **ソース** ビューにユーザー コントロール ファイルが表示されます。 このビューで、コントロールの XML マークアップを編集できます。 **ツールボックス** からコントロールをドラッグしてコントロールを視覚的にデザインする場合は、**デザイン** ビューに切り替えます。 「[デザイン ビュー、Web Page Designer](/previous-versions/aspnet/ms178149\(v\=vs.100\))」を参照してください。

7. コントロールで発生するイベントを処理する場合は、ユーザー コントロールのコード ファイルにコードを追加します。

     このファイルは、**ソリューション エクスプローラー** のユーザー コントロール ファイルの下に表示されます。コード ファイルの拡張子は *.cs* または *.vb* です (プロジェクトの言語によって異なります)。

## <a name="see-also"></a>関連項目
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
