---
title: カスタム マスター ページおよびイメージを含むサイト ページのインポート
description: このチュートリアルでは、SharePoint カスタム マスター ページとイメージが含まれているサイト ページを Visual Studio SharePoint プロジェクトにインポートします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 503ffc733a408787e7ecf188d893039759819c6d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952578"
---
# <a name="walkthrough-import-a-custom-master-page-and-site-page-with-an-image"></a>チュートリアル: イメージを備えたカスタム マスター ページおよびサイト ページのインポート
  このチュートリアルでは、SharePoint カスタム マスター ページとイメージが含まれているサイト ページを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトにインポートする方法について説明します。

 このチュートリアルで説明する内容は次のとおりです。

- SharePoint Designer のイメージを使用して、カスタム マスター ページとサイト ページを作成します。

- カスタム マスター ページ、イメージ、およびサイト ページを SharePoint ソリューション ( *.wsp*) ファイルにエクスポートします。

- SharePoint ソリューション パッケージのインポート プロジェクトを使用して、 *.wsp* ファイルをインポートし、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトに配置します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポートされているエディションの [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] と SharePoint。

- 見ることができます。

- SharePoint Designer 2010。

## <a name="create-items-in-sharepoint-designer"></a>SharePoint Designer で項目を作成する
 この例では、SharePoint Designer でエクスポート用に 3 つの項目 (カスタム マスター ページ、カスタム マスター ページを参照するサイト ページ、およびサイト ページに表示されるイメージ ファイル) を作成する方法を示します。 イメージは、SharePoint の /images/ フォルダーに追加されます。

#### <a name="to-create-a-custom-master-page-in-sharepoint-designer"></a>SharePoint Designer でカスタム マスター ページを作成するには

1. SharePoint Designer のナビゲーション ウィンドウで、 **[マスター ページ]** サイトオブジェクトを選択します。

2. **[マスター ページ]** リボンで、 **[空白のマスター ページ]** を選択します。

3. 新しいマスター ページを選択し、 **[マスター ページ]** リボンの **[ファイルの編集]** を選択します。

4. SharePoint Designer の下部にある **[コード]** タブを選択します。

5. 既存のマークアップを次のマークアップに置き換えます。

    ```aspx-csharp
    <%@ Master Language="C#" %>
    <%@ Register tagprefix="SharePoint" namespace="Microsoft.SharePoint.WebControls" assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <html dir="ltr">
    <head runat="server">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <SharePoint:RobotsMetaTag runat="server" __designer:Preview="" __designer:Values="<P N='InDesign' T='False' /><P N='ID' T='ctl00' /><P N='Page' ID='1' /><P N='TemplateControl' ID='2' /><P N='AppRelativeTemplateSourceDirectory' R='-1' />"></SharePoint:RobotsMetaTag>
    <title>Web Page</title>
    </head>
    <body>
    <form id="form1" runat="server">
    <asp:ContentPlaceHolder id="ContentPlaceHolderMain"
            runat="server">
          </asp:ContentPlaceHolder>
    </form>
    </body>
    </html>
    ```

6. ページを保存し、 **[マスター ページ]** タブを選択して、マスター ページの名前を **mybasic1.master** に変更します。

## <a name="add-an-image-to-the-content-database-in-sharepoint-designer"></a>SharePoint Designer でコンテンツ データベースにイメージを追加する
 これで、サイト ページに表示するイメージを追加できるようになりました。 イメージは SharePoint コンテンツ データベースに配置されます。

#### <a name="to-add-an-image-to-the-content-database-in-sharepoint-designer"></a>SharePoint Designer でコンテンツ データベースにイメージを追加するには

1. ナビゲーション ウィンドウで、 **[すべてのファイル]** サイト オブジェクトを選択し、ツリー ビューで **images** フォルダーを選択します。

2. **[すべてのファイル]** リボンで、 **[ファイルのインポート]** を選択し、任意のファイルを選択して、 **[OK]** をクリックします。 この例では、ファイルの名前は **myimg1.png** です。

     必要に応じて、イメージの整理に役立つサブフォルダーを作成することもできます。

3. **[インポート]** ダイアログ ボックスを閉じます。

## <a name="create-a-site-page"></a>サイト ページを作成する
 この基本的なサイト ページでは、カスタム マスター ページを使用し、前の手順で追加したイメージを表示します。

#### <a name="to-create-a-site-page"></a>サイト ページを作成するには

1. ナビゲーション ウィンドウで、 **[サイト ページ]** オブジェクトを選択します。

2. **[ページ]** リボンで **[ページ]** ボタンを選択し、 **[ASPX]** ページの種類を選択して、新しいファイルに「**mycontentpage1.aspx**」という名前を付けます。

     必要に応じて、サイト ページの整理に役立つサブフォルダーを作成することもできます。

3. サイト ページの一覧で **[MyContentPage1.aspx]** を選択してプロパティ ページを開き、ページの下部にある **[ファイルの編集]** リンクを選択します。

     このページにセーフ モードで編集可能な領域が含まれておらず、詳細設定モードでこのページを開くかどうかを確認するメッセージが表示された場合は、 **[はい]** をクリックします。

4. ページの下部にある **[コード]** ボタンをクリックします。

5. 既存のマークアップを次のマークアップに置き換えます。

    ```aspx-csharp
    <%@ Import Namespace="Microsoft.SharePoint.ApplicationPages" %>
    <%@ Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="Utilities" Namespace="Microsoft.SharePoint.Utilities" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="asp" Namespace="System.Web.UI" Assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" %>
    <%@ Import Namespace="Microsoft.SharePoint" %>
    <%@ Assembly Name="Microsoft.Web.CommandUI, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Page Language="C#" Inherits="Microsoft.SharePoint.WebControls.LayoutsPageBase" MasterPageFile="../_catalogs/masterpage/mybasic1.master" meta:progid="SharePoint.WebPartPage.Document" %>

    <asp:Content ID="Main" ContentPlaceHolderID="ContentPlaceHolderMain" runat="server">
    <img alt="My Image" longdesc="My image from images folder" src="../images/myimg1.png" />
    </asp:Content>
    ```

6. 更新されたサイト ページを保存します。

## <a name="export-the-items-from-sharepoint"></a>SharePoint から項目をエクスポートする
 SharePoint から SharePoint ソリューション ( *.wsp*) ファイルに項目をエクスポートします。

#### <a name="to-export-items-from-sharepoint-designer"></a>SharePoint Designer から項目をエクスポートするには

1. SharePoint Designer のナビゲーション ウィンドウで、 **[チーム サイト]** オブジェクトを選択し、 **[サイト]** リボンで **[テンプレートとして保存]** を選択します。

2. **[テンプレートとして保存]** ダイアログ ボックスで、ファイル名とテンプレート名を入力し、 **[コンテンツを含める]** チェック ボックスをオンにして、 **[OK]** をクリックします。

     これにより、サイトのコンテンツが *.wsp* ファイルに保存されます。

3. ソリューションのエクスポート後、 **[ソリューション ギャラリー]** リンクを選択して、使用可能なソリューション ファイルの一覧を表示します。

4. 新しい *.wsp* ファイルのショートカット メニューを開き、 **[対象をファイルに保存]** を選択してシステムに保存します。

## <a name="import-the-items-into-visual-studio"></a>項目を Visual Studio にインポートする
 *.wsp* ファイルを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートします。 コンテンツがインポートされたら、それをカスタマイズし、さらに項目を追加してから、配置することができます。

#### <a name="to-import-items-from-the-wsp-file-into-visual-studio"></a>.wsp ファイルから Visual Studio に項目をインポートするには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、"**SharePoint 2010 ソリューション パッケージのインポート**" プロジェクトを作成します。

2. **[インポートする項目の選択]** ページの **[型]** 列の **[モジュール]** で、次の表の中でインポートするファイルのチェック ボックスのみをオンにします。

   | ファイル名 | 説明 |
   |------------------------|-----------------------------------------------|
   | \_catalogsmasterpage\_ | カスタム マスター ページ。 |
   | images_ | SharePoint ファイル システム内のイメージ ファイル。 |
   | SitePages_ | サイト ページ。 |

3. **[完了]** ボタンを選択すると、選択した項目がインポートされます。

4. **ソリューション エクスプローラー** で、\_catalogsmasterpage\_ ノードを選択し、その **[配置競合の解決]** プロパティの値を **[自動]** に設定します。

    これにより、配置競合が自動的に解決されるようになります。

5. 新しいマスター ページに既存のページと同じ名前が付けられている場合は、既存のページが SharePoint Designer の既定のマスター ページまたはカスタム マスター ページのいずれとしてもマークされていないことを確認してください。

    既存のマスター ページが既定のマスター ページまたはカスタム マスター ページのいずれかとしてマークされている場合は、マスター ページを削除できないことを示す配置エラーが発生します。 この問題を回避するには、次の操作を行います。

   - 既存のマスター ページが既定のマスター ページとして設定されている場合は、一時的に別のマスター ページを既定のマスター ページとして設定します。 ファイルを SharePoint に配置した後、新しいマスター ページを既定のマスター ページとして設定します。

   - 既存のマスター ページがカスタム マスター ページとして設定されている場合は、一時的に別のマスター ページをカスタム マスター ページとして設定します。 ファイルを SharePoint に配置した後、新しいマスター ページをカスタム マスター ページとして設定します。

6. メニュー バーで **[ビルド]**  >  **[ソリューションの配置]** の順に選択します。

7. SharePoint サイトを開いて、配置された項目を確認します。

   ファイルを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートして SharePoint に配置する別の方法として、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のモジュールにファイルを追加する方法があります。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][マスター ページまたはテーマをインポートする方法](../sharepoint/how-to-import-a-master-page-or-theme.md)に関するページと、「[モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [既存の SharePoint サイトからの項目のインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
