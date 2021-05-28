---
title: WPF と Entity Framework を使用した WCF Data Service を作成する
description: ASP.NET Web アプリケーションでホストされている WPF と Entity Framework を使用して WCF Data Service を作成し、Windows フォーム アプリケーションからアクセスします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data services in Visual Studio
- WCF Data Services, Visual Studio
- ADO.NET Data Services, Visual Studio
- WCF data services in Visual Studio
ms.assetid: da66ad1b-a25d-485c-af13-2d18f0422e3d
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f519d8e3bfe01fc3e4a1e4cfe82f4f8502c84821
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215696"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>チュートリアル: WPF と Entity Framework を使用した WCF データ サービスの作成
このチュートリアルでは、[!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] Web アプリケーションでホストされる簡単な [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] を作成して、Windows フォーム アプリケーションからアクセスする方法について説明します。

このチュートリアルでは、次の作業を行います。

- [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] をホストする Web アプリケーションを作成します。

- Northwind データベースの `Customers` テーブルを表す [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] を作成します。

- [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] を作成します。

- クライアント アプリケーションを作成し、[!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] への参照を追加します。

- サービスへのデータ バインディングを有効にし、ユーザー インターフェイスを生成します。

- 必要に応じて、アプリケーションにフィルター処理機能を追加します。

## <a name="prerequisites"></a>前提条件
このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** では、**データ ストレージとデータ処理** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (**SQL Server オブジェクト エクスプローラー** は、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="creating-the-service"></a>サービスの作成
[!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] を作成するには、Web プロジェクトを追加し、[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] を作成した後、そのモデルからサービスを作成します。

最初に、サービスをホストする Web プロジェクトを追加します。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-the-web-project"></a>Web プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Basic]** または **[Visual C#]** ノードを展開して、**[Web]** ノードをクリックし、**[ASP.NET Web アプリケーション]** テンプレートをクリックします。

3. **[名前]** ボックスに「**NorthwindWeb**」と入力し、**[OK]** をクリックします。

4. **[新しい ASP.NET プロジェクト]** ダイアログ ボックスの **[テンプレートの選択]** リストで **[なし]** を選択し、**[OK]** ボタンをクリックします。

次の手順では、Northwind データベースの `Customers` テーブルを表す [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] を作成します。

### <a name="to-create-the-entity-data-model"></a>Entity Data Model を作成するには

1. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで **[データ]** ノードを選択し、**[ADO.NET エンティティ データ モデル]** 項目を選択します。

3. **[名前]** ボックスに「`NorthwindModel`」と入力して、 **[追加]** を選択します。

     Entity Data Model ウィザードが表示されます。

4. エンティティ データ モデル ウィザードの **[モデルのコンテンツの選択]** ページで、**[データベースから EF デザイナー]** 項目を選択してから **[次へ]** ボタンを選択します。

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

    - Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

         または

    - **[新しい接続]** を選択して、新しいデータ接続を構成します。 詳細については、「[新しい接続を追加する](../data-tools/add-new-connections.md)」を参照してください。

6. データベースにパスワードが必要な場合は、**[はい、重要情報を接続文字列に含めます。]** を選択し、**[次へ]** をクリックします。

    > [!NOTE]
    > ダイアログ ボックスが表示された場合は、**[はい]** をクリックしてファイルをプロジェクトに保存します。

7. **[バージョンの選択]** ページで **[Entity Framework 5.0]** オプション ボタンを選択し、**[次へ]** をクリックします。

    > [!NOTE]
    > WCF サービスで Entity Framework 6 の最新バージョンを使用するには、WCF Data Services Entity Framework Provider NuGet パッケージのインストールが必要になります。 「[WCF Data Services 5.6.0 と Entity Framework 6+ の使用](https://devblogs.microsoft.com/odata/using-wcf-data-services-5-6-0-with-entity-framework-6/)」を参照してください。

8. **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開し、**[Customers]** チェック ボックスをオンにして **[完了]** をクリックします。

     エンティティ モデル ダイアグラムが表示され、プロジェクトに *NorthwindModel.edmx* ファイルが追加されます。

次の手順では、データ サービスを作成してテストします。

### <a name="to-create-the-data-service"></a>データ サービスを作成するには

1. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで **[Web]** ノードを選択し、**[WCF Data Service 5.6]** 項目を選択します。

3. **[名前]** ボックスに「`NorthwindCustomers`」と入力して、 **[追加]** を選択します。

     **NorthwindCustomers.svc** ファイルが **コード エディター** に表示されます。

4. **コード エディター** で、最初の `TODO:` コメントを探して、コードを次のコードに置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs" id="Snippet1":::

5. `InitializeService` イベント ハンドラーのコメントを次のコードに置き換えます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs" id="Snippet2":::


6. メニュー バーで **[デバッグ]**  >  **[デバッグなしで開始]** の順にクリックして、プロジェクトを実行します。 ブラウザー ウィンドウが開き、そのサービスの XML スキーマが表示されます。

7. **[アドレス]** バーの **NorthwindCustomers.svc** の URL の末尾に「`Customers`」と入力し、**Enter** キーを押します。

     `Customers` テーブル内のデータの XML 表現が表示されます。

    > [!NOTE]
    > Internet Explorer がデータを誤って RSS フィードとして解釈する場合があります。 RSS フィードを表示するオプションが無効になっていることを確認してください。 詳細については、「[サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md)」を参照してください。

8. ブラウザー ウィンドウを閉じます。

次の手順では、サービスを使用する Windows フォーム クライアント アプリケーションを作成します。

## <a name="creating-the-client-application"></a>クライアント アプリケーションの作成
クライアント アプリケーションを作成するには、2 つ目のプロジェクトを追加し、そのプロジェクトにサービス参照を追加します。そして、データ ソースを構成し、サービスから取得したデータを表示するユーザー インターフェイスを作成します。

最初に、Windows フォーム プロジェクトをソリューションに追加し、スタートアップ プロジェクトに設定します。

### <a name="to-create-the-client-application"></a>クライアント アプリケーションを作成するには

1. メニュー バーで [ファイル]、 **[追加]**  >  **[新しいプロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual Basic]** ノードまたは **[Visual C#]** ノードを展開し、 **[Windows]** をクリックして **[Windows フォーム アプリケーション]** をクリックします。

3. **[名前]** ボックスに「`NorthwindClient`」と入力して、 **[OK]** を選択します。

4. **ソリューション エクスプローラー** で、**[NorthwindClient]** プロジェクト ノードをクリックします。

5. メニュー バーで、**[プロジェクト]**、**[スタートアップ プロジェクトに設定]** の順に選択します。

次の手順では、Web プロジェクト内の [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] へのサービス参照を追加します。

### <a name="to-add-a-service-reference"></a>サービス参照を追加するには

1. メニュー バーで、 **[プロジェクト]**  >  **[サービス参照の追加]** の順に選択します。

2. **[サービス参照の追加]** ダイアログ ボックスで、**[探索]** をクリックします。

     NorthwindCustomers サービスの URL が **[アドレス]** フィールドに表示されます。

3. **[OK]** をクリックして、サービス参照を追加します。

次の手順では、データ ソースを構成して、サービスへのデータ バインディングを有効にします。

### <a name="to-enable-data-binding-to-the-service"></a>サービスへのデータ バインディングを有効にするには

1. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[データ ソース]** を選択します。

   **[データ ソース]** ウィンドウが開きます。

2. **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックします。

3. **データ ソースの構成ウィザード** の **[データ ソースの種類を選択]** ページで、**[オブジェクト]** をクリックし、**[次へ]** をクリックします。

4. **[データ オブジェクトの選択]** ページで、**NorthwindClient** ノードを展開し、さらに **NorthwindClient.ServiceReference1** ノードを展開します。

5. **[Customer]** チェック ボックスをオンにし、**[完了]** をクリックします。

次の手順では、サービスから取得したデータを表示するユーザー インターフェイスを作成します。

### <a name="to-create-the-user-interface"></a>ユーザー インターフェイスを作成するには

1. **[データ ソース]** ウィンドウで、**[Customers]** ノードのショートカット メニューを開き、**[コピー]** をクリックします。

2. **[Form1.vb]** または **[Form1.cs]** フォーム デザイナーで、ショートカット メニューを開き、**[貼り付け]** をクリックします。

    <xref:System.Windows.Forms.DataGridView> コントロール、<xref:System.Windows.Forms.BindingSource> コンポーネント、および <xref:System.Windows.Forms.BindingNavigator> コンポーネントがフォームに追加されます。

3. **[CustomersDataGridView]** コントロールを選択してから、**[プロパティ]** ウィンドウで **[Dock]** プロパティを **[Fill]** に設定します。

4. **ソリューション エクスプローラー** で、 **[Form1]** ノードのショートカット メニューを開き、 **[コードの表示]** を選択してコード エディターを開き、次の `Imports` または `Using` ステートメントをファイルの先頭に追加します。

   ```vb
   Imports NorthwindClient.ServiceReference1
   ```

   ```csharp
   using NorthwindClient.ServiceReference1;
   ```

5. `Form1_Load` イベント ハンドラーに次のコードを追加します。

   ```vb
   Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
           Dim proxy As New NorthwindEntities _
   (New Uri("http://localhost:53161/NorthwindCustomers.svc/"))
           Me.CustomersBindingSource.DataSource = proxy.Customers
       End Sub
   ```

   ```csharp
   private void Form1_Load(object sender, EventArgs e)
   {
   NorthwindEntities proxy = new NorthwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc/"));
   this.CustomersBindingSource.DataSource = proxy.Customers;
   }
   ```

6. **ソリューション エクスプローラー** で、**NorthwindCustomers.svc** ファイルのショートカット メニューを開き、**[ブラウザーで表示]** をクリックします。 Internet Explorer が開き、そのサービスの XML スキーマが表示されます。

7. Internet Explorer のアドレス バーから URL をコピーします。

8. 手順 4. で追加したコードの「`http://localhost:53161/NorthwindCustomers.svc/`」を選択し、コピーした URL に置き換えます。

9. メニュー バーで、 **[デバッグ]**  >  **[デバッグ開始]** の順に選択してアプリケーションを実行します。 顧客情報が表示されます。

   この時点で、NorthwindCustomers サービスから取得した顧客の一覧を表示するアプリケーションが作成されました。 このサービスを使用して他のデータも公開する場合は、[!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)]を変更して、Northwind データベースの他のテーブルを含めます。

次の省略可能な手順では、サービスによって返されたデータをフィルター処理する方法について説明します。

## <a name="adding-filtering-capabilities"></a>フィルター処理機能の追加
この手順では、アプリケーションをカスタマイズして、都市で顧客データをフィルター処理します。

### <a name="to-add-filtering-by-city"></a>都市によるフィルター処理を追加するには

1. **ソリューション エクスプローラー** で、**[Form1.vb]** または **[Form1.cs]** ノードのショートカット メニューを開き、**[開く]** をクリックします。

2. **[ツールボックス]** から、<xref:System.Windows.Forms.TextBox> コントロールと <xref:System.Windows.Forms.Button> コントロールをフォームに追加します。

3. <xref:System.Windows.Forms.Button> コントロールのショートカット メニューを開き、 **[コードの表示]** をクリックして、`Button1_Click` イベント ハンドラーに次のコードを追加します。

    ```vb
    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
            Dim proxy As New northwindEntities _
    (New Uri("http://localhost:53161/NorthwindCustomers.svc"))
            Dim city As String = TextBox1.Text

            If city <> "" Then
                Me.CustomersBindingSource.DataSource = From c In _
             proxy.Customers Where c.City = city
            End If

        End Sub
    ```

    ```csharp
    private void Button1_Click(object sender, EventArgs e)
    {
    ServiceReference1.northwindModel.northwindEntities proxy = new northwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc"));
    string city = TextBox1.Text;

    if (!string.IsNullOrEmpty(city)) {
    this.CustomersBindingSource.DataSource = from c in proxy.Customers where c.City == city;
    }

    }
    ```

4. このコードの `http://localhost:53161/NorthwindCustomers.svc` を `Form1_Load` イベント ハンドラーの URL に置き換えます。

5. メニュー バーで、 **[デバッグ]**  >  **[デバッグ開始]** の順に選択してアプリケーションを実行します。

6. テキスト ボックスに「**London**」と入力し、ボタンをクリックします。 ロンドンの顧客だけが表示されます。

## <a name="see-also"></a>こちらもご覧ください

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
- [方法: WCF データ サービス参照を追加、更新、または削除する](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)
