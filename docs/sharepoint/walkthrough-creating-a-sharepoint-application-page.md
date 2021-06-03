---
title: 'チュートリアル: SharePoint アプリケーション ページの作成 | Microsoft Docs'
description: このチュートリアルでは、アプリケーション ページ (特殊な形式の ASP.NET ページ) を作成し、ローカルの SharePoint サイトを使用してデバッグします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6640373dac6d08144f1ef7fd230afa172540afe6
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217763"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>チュートリアル: SharePoint アプリケーション ページの作成

アプリケーション ページとは、特殊なフォームの ASP.NET ページです。 アプリケーション ページには、SharePoint のマスター ページとマージされるコンテンツが含まれます。 詳細については、[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)に関するページを参照してください。

このチュートリアルでは、アプリケーション ページを作成し、そのページをローカル SharePoint サイトを使ってデバッグする方法を説明します。 このページには、サーバー ファーム上のあらゆるサイトで、各ユーザーが作成または変更したすべての項目が表示されます。

このチュートリアルでは、次の作業について説明します。

- SharePoint プロジェクトを作成する
- SharePoint プロジェクトにアプリケーション ページを追加する
- アプリケーション ページに ASP.NET コントロールを追加する
- ASP.NET コントロールに分離コードを追加する
- アプリケーション ページをテストする

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- サポート対象エディションの Windows と SharePoint

## <a name="create-a-sharepoint-project"></a>SharePoint プロジェクトを作成する

まず、**空の SharePoint プロジェクト** を作成します。 後で、このプロジェクトに **[アプリケーション ページ]** 項目を追加します。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[新しいプロジェクト]** ダイアログ ボックスを開き、使用する言語の **[Office/SharePoint]** ノードを展開して、 **[SharePoint ソリューション]** ノードを選択します。

3. **[Visual Studio にインストールされたテンプレート]** ペインで **[SharePoint 2010 - 空のプロジェクト]** を選択します。 プロジェクトに **MySharePointProject** という名前を付け、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。 このウィザードを使用すると、プロジェクトのデバッグに使用するサイトや、ソリューションの信頼レベルを選択できます。

4. **[ファーム ソリューションとして配置する]** オプション ボタンをクリックしてから、 **[完了]** をクリックして、ローカル SharePoint サイトの構成を既定値のままにします。

## <a name="create-an-application-page"></a>アプリケーション ページを作成する

アプリケーション ページを作成するには、プロジェクトに **[アプリケーション ページ]** 項目を追加します。

1. **ソリューション エクスプローラー** で、**MySharePointProject** プロジェクトを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[アプリケーション ページ (ファーム ソリューションのみ)]** テンプレートを選択します。

4. このページに **SearchItems** という名前を付け、 **[追加]** をクリックします。

     Visual Web Developer デザイナーの **ソース** ビューにアプリケーション ページが表示されます。このビューでは、対象ページの HTML 要素を確認できます。 デザイナーにはいくつかの <xref:System.Web.UI.WebControls.Content> コントロールのマークアップが表示されます。 各コントロールは、既定のアプリケーション マスター ページに定義されている <xref:System.Web.UI.WebControls.ContentPlaceHolder> コントロールにマップされます。

## <a name="design-the-layout-of-the-application-page"></a>アプリケーション ページのレイアウトをデザインする

アプリケーション ページ項目を使用すると、デザイナーで ASP.NET コントロールをアプリケーション ページに追加できます。 このデザイナーは、Visual Web Developer で使用するデザイナーと同じです。 ラベル、オプション ボタン リスト、およびテーブルをデザイナーの **ソース** ビューに追加し、標準的な ASP.NET ページをデザインする場合と同様にプロパティを設定します。

1. メニュー バーで **[表示]** 、 **[ツールボックス]** の順にクリックします。

2. **ツールボックス** の [標準] ノードで、次のいずれかの手順に従います。

    - **[Label]** 項目のショートカット メニューを開き、 **[コピー]** を選択します。デザイナーで、**PlaceHolderMain** コンテンツ コントロールの下にある行のショートカット メニューを開き、 **[貼り付け]** を選択します。

    - **ツールボックス** の **[Label]** 項目を、**PlaceHolderMain** コンテンツ コントロールの本体までドラッグします。

3. 上記と同じ手順で、 **[DropDownList]** 項目と **[Table]** 項目を **PlaceHolderMain** コンテンツ コントロールに追加します。

4. デザイナーで、ラベル コントロールの `Text` 属性の値を **[すべての項目を表示]** に変更します。

5. デザイナーで、`<asp:DropDownList>` 要素を次の XML に置き換えます。

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>ページ上のコントロールのイベントを処理する

ASP.NET ページと同様に、アプリケーション ページのコントロールを処理します。 この手順では、ドロップダウン リストの `SelectedIndexChanged` イベントを処理します。

1. **[表示]** メニューの **[コード]** を選択します。

     コード エディターでアプリケーション ページ コード ファイルが開きます。

2. `SearchItems` クラスに次のメソッドを追加します。 このコードでは、このチュートリアルでこれから作成するメソッドを呼び出して、<xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> の <xref:System.Web.UI.WebControls.DropDownList> イベントを処理します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet5":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet5":::

3. アプリケーション ページ コード ファイルの先頭に次のステートメントを追加します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet1":::

4. `SearchItems` クラスに次のメソッドを追加します。 このメソッドでは、サーバー ファーム上のすべてのサイトについて反復処理を行い、現在のユーザーが作成または変更した項目を検索します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet2":::

5. `SearchItems` クラスに次のメソッドを追加します。 このメソッドでは、現在のユーザーが作成または変更した項目をテーブルに表示します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs" id="Snippet3":::

## <a name="test-the-application-page"></a>アプリケーション ページをテストする

プロジェクトを実行すると、SharePoint サイトが開き、アプリケーション ページが表示されます。

1. **ソリューション エクスプローラー** で、アプリケーション ページのショートカット メニューを開き、 **[スタートアップ アイテムとして設定]** を選択します。

2. **F5** キーを押します。

     SharePoint サイトが開きます。

3. アプリケーション ページで **[自分が更新者]** を選択します。

     アプリケーション ページが更新され、サーバー ファーム上のすべてのサイトで自分が変更したすべての項目が表示されます。

4. アプリケーション ページの一覧で **[現在のユーザーが作成]** を選択します。

     アプリケーション ページが更新され、サーバー ファーム上のすべてのサイトで自分が作成したすべての項目が表示されます。

## <a name="next-steps"></a>次のステップ

SharePoint アプリケーション ページの詳細については、「[SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)」を参照してください。

Visual Web Designer を使用して、SharePoint ページの内容をデザインする方法の詳細については、以下のトピックを参照してください。

- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>関連項目

[方法: アプリケーション ページを作成する](../sharepoint/how-to-create-an-application-page.md)
[Application _layouts ページの種類](/previous-versions/office/aa979604(v=office.14))
