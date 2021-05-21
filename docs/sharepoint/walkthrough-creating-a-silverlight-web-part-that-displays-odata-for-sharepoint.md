---
title: SharePoint の OData を表示する Silverlight Web パーツを作成する
titleSuffix: ''
description: SharePoint の OData を表示する Silverlight Web パーツを作成します。 Silverlight アプリケーションをカスタマイズし、Silverlight Web パーツを変更してテストします。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ee35ecc9cfa49f445e93677df9d2917150bc1e74
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847831"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>チュートリアル: SharePoint の OData を表示する Silverlight Web パーツを作成する
  SharePoint 2010 では、リスト データの公開に OData が使用されています。 SharePoint での OData サービスは、RESTful サービス ListData.svc によって実装されています。 このチュートリアルでは、Silverlight アプリケーションをホストする SharePoint Web パーツを作成する方法について説明します。 Silverlight アプリケーションで SharePoint のお知らせリストの情報を表示するには、ListData.svc を使用します。 詳細については、「[SharePoint Foundation REST インターフェイス](/previous-versions/office/developer/sharepoint-2010/ff521587(v=office.14))」および [Open Data Protocol](https://www.odata.org/) に関するページを参照してください。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>Silverlight アプリケーションと Silverlight Web パーツを作成する
 まず、Visual Studio で Silverlight アプリケーションを作成します。 Silverlight アプリケーションで ListData.svc サービスを使用して SharePoint のお知らせリストからデータを取得します。

> [!NOTE]
> 4\.0 より前のバージョンの Silverlight では、SharePoint のリスト データを参照するために必要なインターフェイスがサポートされていません。

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>Silverlight アプリケーションと Silverlight Web パーツを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。

2. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. テンプレート ペインで、 **[SharePoint 2010 Silverlight Web パーツ]** テンプレートを選択します。

4. **[名前]** ボックスに「**SLWebPartTest**」と入力し、 **[OK]** ボタンを選択します。

    **[SharePoint カスタマイズ ウィザード]** ダイアログ ボックスが表示されます。

5. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、サイト定義をデバッグする SharePoint サーバー サイトの URL を入力するか、既定の場所 (http://<<em>システム名</em>>/) を使用します。

6. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[ファーム ソリューションとして配置する]** オプション ボタンを選択します。

    この例ではファーム ソリューションを使用しますが、Silverlight Web パーツ プロジェクトは、ファーム ソリューションまたはサンドボックス ソリューションとして配置できます。 サンドボックス ソリューションとファーム ソリューションの詳細については、「[サンド ボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[Silverlight 構成情報の指定]** ページの **[Silverlight Web パーツを関連付ける方法]** セクションで、 **[新しい Silverlight プロジェクトを作成して Web パーツと関連付ける]** オプション ボタンを選択します。

8. **[名前]** を **SLApplication** に変更し、 **[言語]** を **[Visual Basic]** または **[Visual C#]** のいずれかに設定して、 **[Silverlight バージョン]** を **Silverlight 4.0** に設定します。

9. **[完了]** をクリックします。 **ソリューション エクスプローラー** にプロジェクトが表示されます。

     ソリューションには、Silverlight アプリケーションと Silverlight Web パーツという 2 つのプロジェクトが含まれています。 Silverlight アプリケーションによって、SharePoint からリスト データが取得されて表示されます。Silverlight Web パーツによって、Silverlight アプリケーションがホストされ、SharePoint で表示できるようになります。

## <a name="customize-the-silverlight-application"></a>Silverlight アプリケーションをカスタマイズする
 Silverlight アプリケーションにコードとデザイン要素を追加します。

#### <a name="to-customize-the-silverlight-application"></a>Silverlight アプリケーションをカスタマイズするには

1. Silverlight アプリケーションで System.Windows.Data へのアセンブリ参照を追加します。 詳しくは、「[方法: [参照の追加] ダイアログ ボックスを使用して参照を追加または削除する](/previous-versions/wkze6zky(v=vs.140))」を参照してください。

2. **ソリューション エクスプローラー** で、 **[参照]** のショートカット メニューを開き、 **[サービス参照の追加]** を選択します。

    > [!NOTE]
    > Visual Basic を使用している場合は、**ソリューション エクスプローラー** の上部にある **[すべてのファイルを表示]** アイコンを選択して、 **[参照]** ノードを表示する必要があります。

3. **[サービス参照の追加]** ダイアログ ボックスの [アドレス] ボックスに SharePoint サイトの URL ( **http://MySPSite** など) を入力して、 **[実行]** ボタンを選択します。

     Silverlight によって SharePoint OData サービスの ListData.svc が検索され、アドレスがサービスの完全な URL に置き換えられます。 この例では、 http://myserver が http://myserver/_vti_bin/ListData.svc になります。

4. **[OK]** を選択してサービス参照をプロジェクトに追加し、既定のサービス名 ServiceReference1 を使用します。

5. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

6. SharePoint サービスに基づいて新しいデータ ソースをプロジェクトに追加します。 そのためには、メニュー バーで **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** を選択します。

     **[データ ソース]** ウィンドウには、タスク、お知らせ、カレンダーなど、SharePoint の利用可能なすべてのリスト データが表示されます。

7. Silverlight アプリケーションにお知らせリスト データを追加します。 **[データ ソース]** ウィンドウから Silverlight デザイナーに "お知らせ" をドラッグできます。

     これにより、SharePoint サイトのお知らせリストにバインドされたグリッド コントロールが作成されます。

8. Silverlight ページに合わせてグリッド コントロールのサイズを変更します。

9. MainPage.xaml コード ファイル (Visual C# の場合は *MainPage.xaml.cs*、Visual Basic の場合は *MainPage.xaml.vb*) で、次の名前空間参照を追加します。

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using directives.
    using SLApplication.ServiceReference1;
    using System.Windows.Data;
    using System.Data.Services.Client;
    ```

10. クラスの先頭に、次の変数宣言を追加します。

    ```vb
    Private context As TeamSiteDataContext
    Private myCollectionViewSource As CollectionViewSource
    Private announcements As New DataServiceCollection(Of AnnouncementsItem)()
    ```

    ```csharp
    private TeamSiteDataContext context;
    private CollectionViewSource myCollectionViewSource;
    DataServiceCollection<AnnouncementsItem> announcements = new DataServiceCollection<AnnouncementsItem>();
    ```

11. `UserControl_Loaded` プロシージャを次のように置き換えます。

    ```vb
    Private Sub UserControl_Loaded_1(sender As Object, e As RoutedEventArgs)
        ' The URL for the OData service.
        ' Replace <server name> in the next line with the name of your SharePoint server.
        context = New TeamSiteDataContext(New Uri("http://<server name>/_vti_bin/ListData.svc"))

        ' Do not load your data at design time.
        If Not System.ComponentModel.DesignerProperties.GetIsInDesignMode(Me) Then
            'Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource =   DirectCast(Me.Resources("announcementsViewSource"), System.Windows.Data.CollectionViewSource)
            announcements.LoadCompleted += New EventHandler(Of LoadCompletedEventArgs)(AddressOf announcements_LoadCompleted)
            announcements.LoadAsync(context.Announcements)
        End If
    End Sub
    ```

    ```csharp
    private void UserControl_Loaded_1(object sender, RoutedEventArgs e)
    {
        // The URL for the OData service.
        // Replace <server name> in the next line with the name of your
        // SharePoint server.
        context = new TeamSiteDataContext(new Uri("http://ServerName>/_vti_bin/ListData.svc"));

        // Do not load your data at design time.
        if (!System.ComponentModel.DesignerProperties.GetIsInDesignMode(this))
        {
            //Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource = (System.Windows.Data.CollectionViewSource)this.Resources["announcementsViewSource"];
            announcements.LoadCompleted += new EventHandler<LoadCompletedEventArgs>(announcements_LoadCompleted);
            announcements.LoadAsync(context.Announcements);
        }
    }
    ```

     *ServerName* プレースホルダーは、SharePoint が実行されているサーバーの名前に必ず置き換えてください。

12. 次のエラー処理プロシージャを追加します。

    ```vb
    Private Sub announcements_LoadCompleted(sender As Object, e As LoadCompletedEventArgs)
        ' Handle any errors.
        If e.[Error] Is Nothing Then
            myCollectionViewSource.Source = announcements
        Else
            MessageBox.Show(String.Format("ERROR: {0}", e.[Error].Message))
        End If
    End Sub

    ```

    ```csharp
    void announcements_LoadCompleted(object sender, LoadCompletedEventArgs e)
    {
        // Handle any errors.
        if (e.Error == null)
        {
            myCollectionViewSource.Source = announcements;
        }
        else
        {
            MessageBox.Show(string.Format("ERROR: {0}", e.Error.Message));
        }
    }
    ```

## <a name="modify-the-silverlight-web-part"></a>Silverlight Web パーツを変更する
 Silverlight Web パーツ プロジェクトのプロパティを変更して、Silverlight のデバッグを有効にします。

#### <a name="to-modify-the-silverlight-web-part"></a>Silverlight Web パーツを変更するには

1. Silverlight Web パーツ プロジェクト (**SLWebPartTest**) のショートカット メニューを開き、 **[プロパティ]** を選択します。

2. **[プロパティ]** ウィンドウで、 **[SharePoint]** タブを選択します。

3. まだ選択されていない場合は、 **[Script デバッグの代わりに Silverlight デバッグを有効にする]** チェック ボックスをオンにします。

4. プロジェクトを保存します。

## <a name="test-the-silverlight-web-part"></a>Silverlight Web パーツをテストする
 SharePoint で新しい Silverlight Web パーツをテストして、SharePoint のリスト データが正しく表示されることを確認します。

#### <a name="to-test-the-silverlight-web-part"></a>Silverlight Web パーツをテストするには

1. **F5** キーを押し、SharePoint ソリューションをビルドして実行します。

2. SharePoint の **[サイトの操作]** メニューで、 **[新しいページ]** を選択します。

3. **[新しいページ]** ダイアログで、「**SL Web パーツ テスト**」といったタイトルを入力し、 **[作成]** ボタンを選択します。

4. ページ デザイナーの **[編集ツール]** タブで、 **[挿入]** を選択します。

5. タブ ストリップで、 **[Web パーツ]** を選択します。

6. **[カテゴリ]** ボックスで、 **[カスタム]** フォルダーを選択します。

7. **[Web パーツ]** の一覧で Silverlight Web パーツを選択し、 **[追加]** ボタンを選択して、Web パーツをデザイナーに追加します。

8. Web ページに必要なものをすべて追加した後、 **[ページ]** タブを選択して、ツール バーの **[保存して閉じる]** ボタンを選択します。

     Silverlight Web パーツに、SharePoint サイトからのお知らせデータが表示されるようになるはずです。 既定では、ページは SharePoint のサイト ページ リストに格納されます。

    > [!NOTE]
    > 異なるドメインから Silverlight のデータにアクセスすると、Web アプリケーションの悪用に使用できるセキュリティの脆弱性が Silverlight によって防がれます。 Silverlight でリモート データにアクセスするときに問題が発生する場合は、「[ドメインの境界を越えてサービスを利用できるようにする](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc197955(v=vs.95))」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [SharePoint ソリューション パッケージの配置、発行、アップグレード](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)