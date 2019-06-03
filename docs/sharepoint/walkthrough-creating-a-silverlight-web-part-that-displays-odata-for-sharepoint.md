---
title: SharePoint の OData を表示する Silverlight web パーツを作成します。
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f248ce4403e771d9ab8b6d13fe55fd5ca1c960d4
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401126"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>チュートリアル: SharePoint の OData を表示する Silverlight web パーツを作成します。
  SharePoint 2010 では、OData を使用してそのリストのデータを公開します。 SharePoint では、OData サービスは、RESTful サービス ListData.svc によって実装されます。 このチュートリアルでは、Silverlight アプリケーションをホストする SharePoint web パーツを作成する方法を示します。 Silverlight アプリケーションでは、ListData.svc を使用して SharePoint のお知らせリストの情報が表示されます。 詳細については、次を参照してください。 [SharePoint Foundation REST インターフェイス](http://go.microsoft.com/fwlink/?LinkId=225999)と[Open Data Protocol](http://go.microsoft.com/fwlink/?LinkId=226000)します。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]。

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>Silverlight アプリケーションと Silverlight web パーツを作成します。
 最初に、Visual Studio で Silverlight アプリケーションを作成します。 Silverlight アプリケーションは、SharePoint のお知らせリストから、ListData.svc サービスを使用してデータを取得します。

> [!NOTE]
> Silverlight 4.0 より前に、のバージョンは、SharePoint リストのデータを参照するため、必要なインターフェイスをサポートありません。

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>Silverlight アプリケーションと Silverlight web パーツを作成するには

1. メニュー バーで、**ファイル** > **新規** > **プロジェクト**を表示する、**新しいプロジェクト** ダイアログ ボックス。

2. **Visual C#** または **Visual Basic** 下の **SharePoint** ノードを展開し、 **2010** ノードを選択します。

3. [テンプレート] ペインで選択、 **SharePoint 2010 Silverlight Web パーツ**テンプレート。

4. **名前**ボックスに、入力**SLWebPartTest**選択し、 **OK**ボタン。

    **SharePoint カスタマイズ ウィザード** ダイアログ ボックスが表示されます。

5. **デバッグのサイトとセキュリティのレベルを指定**ページで、サイト定義をデバッグする SharePoint サーバー サイトの URL を入力するか、既定の場所を使用して (http://<em>システム名</em>/).

6. **この SharePoint ソリューションの信頼レベルとは何ですか?** セクションで、選択、**ファーム ソリューションとして配置**オプション ボタンをクリックします。

    この例では、ファーム ソリューションでは、Silverlight web パーツ プロジェクトは、ファームまたはサンド ボックス ソリューションとしてデプロイできます。 サンド ボックス ソリューションとファーム ソリューションの詳細については、次を参照してください。[サンド ボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)します。

7. **Silverlight Web パーツを関連付ける方法**のセクション、 **Silverlight 構成情報の指定**ページで、選択、**新しい Silverlight プロジェクトを作成し、web パーツに関連付ける**オプション ボタンをクリックします。

8. 変更、**名前**に**SLApplication**設定**言語**いずれかに**Visual Basic**または**Visual c#** 、設定**Silverlight バージョン**に**Silverlight 4.0**します。

9. 選択、**完了**ボタンをクリックします。 プロジェクトが表示される**ソリューション エクスプ ローラー**します。

     2 つのプロジェクトがソリューションに含まれています。 Silverlight アプリケーションと Silverlight web パーツ。 Silverlight アプリケーションを取得し、SharePoint からリスト データを表示し、Silverlight web パーツが SharePoint で表示できるように、Silverlight アプリケーションをホストします。

## <a name="customize-the-silverlight-application"></a>Silverlight アプリケーションをカスタマイズします。
 Silverlight アプリケーションにコードと設計の要素を追加します。

#### <a name="to-customize-the-silverlight-application"></a>Silverlight アプリケーションをカスタマイズするには

1. Silverlight アプリケーションで System.Windows.Data にアセンブリ参照を追加します。 詳細については、「[方法 :追加または参照の追加 ダイアログ ボックスを使用して参照を削除する](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)します。

2. **ソリューション エクスプ ローラー**、ショートカット メニューを開き**参照**を選び、**サービス参照の追加**します。

    > [!NOTE]
    > 選択する必要がある Visual Basic を使用している場合、 **すべてのファイル**の上部にあるアイコン**ソリューション エクスプ ローラー**を表示する、**参照**ノード。

3. アドレス ボックスで、**サービス参照の追加** ダイアログ ボックスで、SharePoint サイトの URL を入力します。 **http://MySPSite** 、選択し、**移動**ボタン。

     Silverlight では、SharePoint の OData サービス ListData.svc を検索、フルテキスト サービスの URL を使用して、アドレスが置き換えられます。 この例では、 http://myserver なります http://myserver/_vti_bin/ListData.svc します。

4. 選択、 **OK**サービス参照をプロジェクトに追加するボタンをクリックし、既定のサービス名、[servicereference1] を使用します。

5. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

6. SharePoint サービスに基づくプロジェクトに新しいデータ ソースを追加します。 メニュー バーで、次のように選択します。**ビュー** > **その他の Windows** > **データソース**します。

     **データソース**ウィンドウには、すべてのタスク、お知らせ、予定表など、使用可能な SharePoint リスト データが表示されます。

7. お知らせリストのデータを Silverlight アプリケーションに追加します。 「お知らせ」からドラッグすることができます、**データソース**Silverlight デザイナーにウィンドウ。

     これは、SharePoint サイトのお知らせリストにバインドされたグリッド コントロールを作成します。

8. Silverlight ページに合わせて、グリッド コントロールのサイズを変更します。

9. MainPage.xaml のコード ファイル内 (*MainPage.xaml.cs* Visual c# または*MainPage.xaml.vb* Visual basic の場合)、次の名前空間参照を追加します。

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using statements.
    using SLApplication.ServiceReference1;
    using System.Windows.Data;
    using System.Data.Services.Client;
    ```

10. クラスの上部にある次の変数宣言を追加します。

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

11. 置換、`UserControl_Loaded`を次の手順。

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

     必ずに置き換えて、 *ServerName*プレース ホルダーを SharePoint を実行しているサーバーの名前。

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

## <a name="modify-the-silverlight-web-part"></a>Silverlight web パーツを変更します。
 Silverlight デバッグを有効にする Silverlight web パーツ プロジェクトのプロパティを変更します。

#### <a name="to-modify-the-silverlight-web-part"></a>Silverlight web パーツを変更するには

1. Silverlight web パーツのプロジェクトのショートカット メニューを開き (**SLWebPartTest**) を選び、**プロパティ**します。

2. **プロパティ**ウィンドウで、選択、 **SharePoint**タブ。

3. 選択されていない場合は、選択、**を有効にする Silverlight のデバッグ (スクリプトのデバッグ) ではなく**チェック ボックスをオンします。

4. プロジェクトを保存します。

## <a name="test-the-silverlight-web-part"></a>Silverlight web パーツをテストします。
 SharePoint リストのデータが正しく表示されることを確認するように SharePoint では、新しい Silverlight web パーツをテストします。

#### <a name="to-test-the-silverlight-web-part"></a>Silverlight web パーツをテストするには

1. 選択、 **F5**キーをビルドして、SharePoint ソリューションを実行します。

2. SharePoint では、上、**サイトの操作**] メニューの [選択**新しいページ**します。

3. **新しいページ**ダイアログ ボックスなどのタイトルを入力します**SL Web パーツのテスト**、選択し、**作成**ボタンをクリックします。

4. ページ デザイナーで、**編集ツール** タブで、選択**挿入**します。

5. タブ ストリップで**Web パーツ**します。

6. **カテゴリ**ボックスで、選択、**カスタム**フォルダー。

7. **Web パーツ**ボックスの一覧で、Silverlight web パーツを選択し、選択、**追加**web パーツをデザイナーに追加するボタンをクリックします。

8. Web ページをすべて追加機能の作成後を選択、**ページ**、タブをクリックして、**保存して閉じる**ツール バー ボタンをクリックします。

     Silverlight web パーツは、ここで、SharePoint サイトからお知らせのデータを表示している必要があります。 既定では、ページは、SharePoint のサイト ページのリストに格納されます。

    > [!NOTE]
    > Silverlight のドメイン間でのデータにアクセスするときに Silverlight web アプリケーションを攻撃に使用できるセキュリティの脆弱性を防止します。 Silverlight でのリモート データにアクセスするときに問題が発生した場合は、次を参照してください。[使用可能なドメインの境界を越えてサービスを行う](http://go.microsoft.com/fwlink/?LinkId=223276)します。

## <a name="see-also"></a>関連項目
- [For SharePoint の web パーツを作成します。](../sharepoint/creating-web-parts-for-sharepoint.md)
- [配置、発行、および SharePoint ソリューション パッケージのアップグレード](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)
