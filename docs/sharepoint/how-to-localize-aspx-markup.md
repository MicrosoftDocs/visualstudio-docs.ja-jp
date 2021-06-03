---
title: '方法: ASPX マークアップをローカライズする | Microsoft Docs'
description: ハードコーディングされた文字列値を、ローカライズされたリソースを参照する式に置き換えることにより、SharePoint で ASPX マークアップをローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1876e06348d60f8a960b352525fd72ad06795101
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931735"
---
# <a name="how-to-localize-aspx-markup"></a>方法: ASPX マークアップをローカライズする
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] (.aspx) ページでは通常、ハードコーディングされた文字列値を使用します。 これらの文字列をローカライズするには、ローカライズされたリソースを参照する式で置き換えます。

## <a name="localize-aspx-markup"></a>ASPX マークアップをローカライズする

#### <a name="to-localize-aspx-markup"></a>ASPX マークアップをローカライズするには

1. 個別のリソース ファイルを追加します。既定の言語用に 1 つと、ローカライズされた言語ごとに 1 つです。

     コードではなくマークアップのみをローカライズする場合は、グローバル リソース ファイル プロジェクト項目を追加します。 コードとマークアップをローカライズする場合は、リソース ファイル プロジェクト項目を追加します。

    1. グローバル リソース ファイルを追加するには、**ソリューション エクスプローラー** で、SharePoint プロジェクト項目のショートカット メニューを開き、 **[追加]**  >  **[新規項目]** を選択します。 SharePoint の **[2010]** ノードで、 **[グローバル リソース ファイル]** テンプレートを選択します。

    2. リソース ファイルを追加するには、**ソリューション エクスプローラー** で、SharePoint プロジェクト項目のショートカット メニューを開き、 **[追加]**  >  **[新規項目]** を選択します。 **[Visual Basic]** または **[Visual C#]** のいずれかのノードで、 **[リソース ファイル]** テンプレートを選択します。

    > [!NOTE]
    > [配置タイプ] プロパティを有効にするために、SharePoint プロジェクト項目にリソース ファイルを必ず追加します。 このプロパティは、後で必要になります。 ソリューションに SharePoint プロジェクト項目がない場合は、空の SharePoint プロジェクトを追加して、既定の *Elements.xml* ファイルを削除できます。

2. 既定の言語のリソース ファイルには、 *.resx* 拡張子が付いた任意の名前を付けます (MyAppResources.resx など)。 ローカライズされた各リソース ファイルに対しては、同じ基本名にカルチャ [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] を加えた名前を使用します (ドイツ語の場合は *MyAppResources.de-DE.resx* など)。

3. 各リソース ファイルの **[配置タイプ]** プロパティの値を **[AppGlobalResource]** に変更して、サーバーの App_GlobalResources フォルダーに配置されるようにします。

4. リソースを ASPX マークアップだけでなくコードのローカライズにも使用する場合は、各ファイルの **[ビルド アクション]** プロパティの値を **[埋め込まれたリソース]** のままにします。 リソース ファイルのみを使用してマークアップをローカライズする場合は、必要に応じて、ファイルのプロパティ値を **[コンテンツ]** に変更できます。 詳細については、「[SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)」を参照してください。

5. 各リソース ファイルを開き、各ファイルで同じ文字列 ID を使用して、ローカライズされた文字列を追加します。

6. ASPX ページまたはコントロールの [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] マークアップで、ハードコーディングされた文字列を、次の形式を使用する値に置き換えます。

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     たとえば、アプリケーション ページのラベル コントロールのテキストをローカライズするには、次のように変更します。

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>
    </asp:Content>
    ```

     to

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>
    </asp:Content>
    ```

7. **F5** キーを押してアプリケーションをビルドし、実行します。

8. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされた文字列がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: フィーチャーをローカライズする](../sharepoint/how-to-localize-a-feature.md)
- [方法: リソース ファイルを追加する](../sharepoint/how-to-add-a-resource-file.md)
- [方法: コードをローカライズする](../sharepoint/how-to-localize-code.md)
