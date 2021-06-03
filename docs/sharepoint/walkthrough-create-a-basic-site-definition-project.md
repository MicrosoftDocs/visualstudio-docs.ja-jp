---
title: 'チュートリアル: 基本サイト定義プロジェクトを作成する | Microsoft Docs'
description: この SharePoint チュートリアルでは、複数のコントロールを備えた視覚的 Web パーツを含む基本サイト定義を作成する方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a505ff059b347c6adbef15a8fe8bcfe7b274eaa4
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218023"
---
# <a name="walkthrough-create-a-basic-site-definition-project"></a>チュートリアル: 基本サイト定義プロジェクトを作成する
  このチュートリアルでは、複数のコントロールを備えた視覚的 Web パーツを含む基本サイト定義を作成する方法について説明します。 わかりやすくするため、作成する視覚的 Web パーツには少数のコントロールしかありません。 ただし、より多くの機能を含むより高度な SharePoint サイト定義を作成できます。

 このチュートリアルでは、次のタスクについて説明します。

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] プロジェクト テンプレートを使用してサイト定義を作成する。

- SharePoint でサイト定義を使用して SharePoint サイトを作成する。

- 視覚的 Web パーツをソリューションに追加する。

- 新しい視覚的 Web パーツを追加して、サイトの default.aspx ページをカスタマイズする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。 詳細については、「SharePoint ソリューションの開発要件」を参照してください。

- 見ることができます。

## <a name="create-a-site-definition-solution"></a>サイト定義ソリューションを作成する
 まず、サイト定義プロジェクトを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] に作成します。

#### <a name="to-create-a-site-definition-project"></a>サイト定義プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、メニュー バーで **[ファイル]**  >  **[新しいプロジェクト]** の順に選択します。

    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[SharePoint]** ノードを展開して、 **[2010]** ノードをクリックします。

3. **[テンプレート]** ボックスの一覧で、 **[SharePoint 2010 プロジェクト]** テンプレートを選択します。

4. **[名前]** ボックスに「**TestSiteDef**」と入力した後、 **[OK]** をクリックします。

    **SharePoint カスタマイズ ウィザード** が表示されます。

5. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、サイト定義をデバッグする SharePoint サイトの URL を入力するか、既定の場所 (http://<em>システム名</em>/) を使用します。

6. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[ファーム ソリューションとして配置する]** オプション ボタンをクリックします。

    すべてのサイト定義プロジェクトは、ファーム ソリューションとして配置する必要があります。 サンドボックス ソリューションとファーム ソリューションの比較の詳細については、「[サンド ボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[完了]** をクリックします。

    **ソリューション エクスプローラー** にプロジェクトが表示されます。

8. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。次に、メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択します。

9. **[Visual C#]** または **[Visual Basic]** で **[SharePoint]** ノードを展開し、 **[2010]** ノードをクリックします。

10. **[テンプレート]** ペインで、 **[サイト定義]** テンプレートを選択し、 **[名前]** は **SiteDefinition1** のままにして、 **[追加]** をクリックします。

## <a name="create-a-visual-web-part"></a>視覚的 Web パーツを作成する
 次に、サイト定義のメイン ページに表示する視覚的 Web パーツを作成します。

#### <a name="to-create-a-visual-web-part"></a>視覚的 Web パーツを作成するには

1. **ソリューション エクスプローラー** で、 **[すべてのファイルを表示]** をクリックします。

2. **[SiteDefinition1]** プロジェクト ノードを選択し、次に、メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

3. **[Visual C#]** ノードまたは **[Visual Basic]** ノードを展開し、 **[SharePoint]** ノードを展開して、 **[2010]** ノードをクリックします。

4. テンプレートの一覧で、 **[視覚的 Web パーツ]** テンプレートを選択し、既定の名前の VisualWebPart1 のままにして、 **[追加]** をクリックします。

     *VisualWebPart1.ascx* ファイルが開きます。

5. *VisualWebPart1.ascx* の下部で、次のマークアップを追加して、テキスト ボックス、ボタン、ラベルの 3 つのコントロールをフォームに追加します。

    ```aspx-csharp
    <table>
      <tr>
        <td>
          <asp:TextBox runat="server" ID="tbName"></asp:TextBox>
        </td>
        <td>
          <asp:Button runat="server" ID="btnSubmit" Text = "Change Label Text" OnClick="btnSubmit_Click"></asp:Button>
        </td>
        <td>
          <asp:Label runat="server" ID="lblName"></asp:Label>
        </td>
      </tr>
    </table>
    ```

6. *VisualWebPart1.ascx* の下で、*VisualWebPart1.ascx.cs* ファイル ([!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] の場合) または *VisualWebPart1.ascx.vb* ファイル ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] の場合) を開き、次のコードを追加します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/testsitedefvb/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/testsitedef/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet1":::

     このコードにより、Web パーツのボタン クリックの機能が追加されます。

## <a name="add-the-visual-web-part-to-the-default-aspx-page"></a>既定の ASPX ページに視覚的 Web パーツを追加する
 次に、視覚的 Web パーツをサイト定義の既定の ASPX ページに追加します。

#### <a name="to-add-a-visual-web-part-to-the-default-aspx-page"></a>既定の ASPX ページに視覚的 Web パーツを追加するには

1. default.aspx ページを開き、`WebPartPages` タグの下に次の行を追加します。

    ```aspx-csharp
    <%@ Register Tagprefix="MyWebPartControls" Namespace="TestSiteDef.VisualWebPart1" Assembly="$SharePoint.Project.AssemblyFullName$" %>
    ```

     この行によって、MyWebPartControls という名前が Web パーツとそのコードに関連付けられます。 *Namespace* パラメーターは、*VisualWebPart1.ascx* コード ファイルで使用されている名前空間と一致します。

2. `</asp:Content>` 要素の後に、`ContentPlaceHolderId="PlaceHolderMain"` セクション全体とその内容を次のコードに置き換えます。

    ```aspx-csharp
    <asp:Content ID="Content1" ContentPlaceHolderId="PlaceHolderMain" runat="server">
        <MyWebPartControls:VisualWebPart1 runat="server" />
    </asp:Content>
    ```

     このコードによって、前に作成した視覚的 Web パーツへの参照が作成されます。

3. **ソリューション エクスプローラー** で、 **[SiteDefinition1]** ノードのショートカット メニューを開き、 **[スタートアップ アイテムとして設定]** を選択します。

## <a name="deploy-and-run-the-site-definition-solution"></a>サイト定義ソリューションを配置して実行する
 次に、プロジェクトを SharePoint に配置してから、プロジェクトを実行します。

#### <a name="to-deploy-and-run-the-site-definition"></a>サイト定義を配置して実行するには

- メニュー バーで **[ビルド]**  >  **[TestSiteDef の配置]** の順に選択します。

- **F5** キーを押します。

     Visual Studio により、コードがコンパイルされ、その機能が追加され、すべてのファイルが SharePoint ソリューション (WSP) ファイルにパッケージ化され、WSP ファイルが SharePoint サーバーに配置されます。 その後、SharePoint によってファイルがインストールされ、機能がアクティブ化されます。

## <a name="create-a-site-based-on-the-site-definition"></a>サイト定義に基づいてサイトを作成する
 次に、新しいサイト定義を使用してサイトを作成します。

#### <a name="to-create-a-site-by-using-the-site-definition"></a>サイト定義を使用してサイトを作成するには

1. SharePoint サイトで、[新しい SharePoint サイト] ページが表示されます。

2. **[タイトルと説明]** セクションで、サイトのタイトルと説明に「**My New Site**」(新しいマイ サイト) と入力します。

3. **[Web サイト アドレス]** セクションで、 **[URL 名]** ボックスに「**mynewsite**」と入力します。

4. **[テンプレート]** セクションで、 **[SharePoint のカスタマイズ]** タブを選択します。

5. **[テンプレートの選択]** ボックスの一覧で **[SiteDefinition1]** を選択します。

6. その他の設定はそれぞれの既定値のままにして、 **[作成]** をクリックします。

     新しいサイトが表示されます。

## <a name="test-the-new-site"></a>新しいサイトをテストする
 次に、新しいサイトをテストして、正常に動作するかどうかを確認します。

#### <a name="to-test-the-new-site"></a>新しいサイトをテストするには

- 既定の ASPX ページで、テキストを入力し、テキスト ボックスの横にある **[ラベル テキストの変更]** をクリックします。

     テキストは、ボタンの右側のラベルに表示されます。

## <a name="see-also"></a>関連項目
- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
