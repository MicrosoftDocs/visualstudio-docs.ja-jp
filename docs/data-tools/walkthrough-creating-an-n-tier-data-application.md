---
title: 'チュートリアル: n 層データ アプリケーションの作成'
description: このチュートリアルでは、n 層データ アプリケーションを作成します。 n 層データ アプリケーションとは、データにアクセスし、多くの論理レイヤーつまり層に分かれているアプリです。
ms.custom: SEO-VS-2020
ms.date: 09/08/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, creating
- n-tier applications, walkthroughs
ms.assetid: d15e4d31-2839-48d9-9e0e-2e73404d82a2
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: ed395c60ec16eeff6a5aac88a99698193e8bacbd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866152"
---
# <a name="walkthrough-create-an-n-tier-data-application"></a>チュートリアル: n 層データ アプリケーションを作成する
*n 層* データ アプリケーションとは、データにアクセスするアプリケーションの中でも、複数の論理レイヤー、つまり *層* に分離されるアプリケーションです。 アプリケーション コンポーネントをこのように別個の層に分離すると、アプリケーションの保守容易性とスケーラビリティが向上します。 これは、ソリューション全体を再設計しなくても 1 つの層に適用できる、新しい技術を簡単に導入できるようにすることで実現されます。 n 層アーキテクチャには、プレゼンテーション層、中間層、およびデータ層が存在します。 通常、中間層には、データ アクセス層、ビジネス ロジック層、および認証や検証などの共有コンポーネントが含まれます。 データ層には、リレーショナル データベースが含まれます。 通常、n 層アプリケーションでは、機密情報が中間層のデータ アクセス層に格納され、プレゼンテーション層にアクセスするエンド ユーザーから分離されます。 詳細については、「[n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)」を参照してください。

n 層アプリケーションで各層を分離する 1 つの方法は、アプリケーションに組み込む層ごとに別個のプロジェクトを作成することです。 型指定されたデータセットには、生成されたデータセットと `DataSet Project` コードの格納先となるプロジェクトを決定する、`TableAdapter` プロパティが含まれています。

このチュートリアルでは、**データセット デザイナー** を使用して、別個のクラス ライブラリ プロジェクトにデータセットと `TableAdapter` コードを分離する方法を示します。 データセットと TableAdapter のコードを分離した後、[Visual Studio で Windows Communication Foundation サービスと WCF Data Services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) を使用して、データ アクセス層を呼び出すためのサービスを作成します。 最後に、プレゼンテーション層として Windows フォーム アプリケーションを作成します。 この層は、データ サービスからデータにアクセスします。

このチュートリアルでは次の手順を実行します。

- 複数のプロジェクトを含む新しい n 層ソリューションを作成する。

- この n 層ソリューションに 2 つのクラス ライブラリ プロジェクトを追加する。

- **データ ソース構成ウィザード** を実行して、型指定されたデータセットを作成する。

- 生成された [TableAdapters](create-and-configure-tableadapters.md) とデータセットのコードを別々のプロジェクトに分離する。

- データ アクセス層を呼び出す Windows Communication Foundation (WCF) サービスを作成する。

- このサービスに、データ アクセス層からデータを取得する関数を作成する。

- プレゼンテーション層として機能する Windows フォーム アプリケーションを作成する。

- Windows フォーム コントロールを作成し、データ ソースにバインドする。

- データ テーブルにデータを読み込むコードを記述する。

![ビデオへのリンク](../data-tools/media/playvideo.gif)このトピックのビデオ版について、次を参照してください[ビデオ操作方法: n 層データ アプリケーションの作成](/previous-versions/visualstudio/visual-studio-2008/cc178916(v=vs.90))。

## <a name="prerequisites"></a>前提条件
このチュートリアルでは SQL Server Express LocalDB と Northwind サンプル データベースを使用します。

1. SQL Server Express LocalDB がない場合は、[SQL Server Express のダウンロード ページ](https://www.microsoft.com/sql-server/sql-server-editions-express)からインストールするか、**Visual Studio インストーラー** を使用してインストールします。 **Visual Studio インストーラー** で、 **.NET デスクトップ開発** ワークロードの一部として、または個別のコンポーネントとして、SQL Server Express LocalDB をインストールできます。

2. 次の手順に従って、Northwind サンプル データベースをインストールします。

    1. Visual Studio で、 **[SQL Server オブジェクト エクスプローラー]** ウィンドウを開きます。 (**SQL Server オブジェクト エクスプローラー** は、Visual Studio インストーラーの **データ ストレージとデータ処理** ワークロードの一部としてインストールされます)。 **[SQL Server]** ノードを展開します。 LocalDB インスタンスを右クリックし、 **[新しいクエリ]** を選択します。

       クエリ エディター ウィンドウが開きます。

    2. [Northwind Transact-SQL スクリプト](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)をクリップボードにコピーします。 この T-SQL スクリプトを使用すると、Northwind データベースが新規作成され、データが設定されます。

    3. T-SQL スクリプトをクエリ エディターに貼り付け、 **[実行]** ボタンを選択します。

       しばらくすると、クエリの実行が完了し、Northwind データベースが作成されます。

## <a name="create-the-n-tier-solution-and-class-library-to-hold-the-dataset-dataentitytier"></a>n 層ソリューションと、データセットを保持するためのクラス ライブラリ (DataEntityTier) を作成する
このチュートリアルでは、まず、1 つのソリューションと 2 つのクラス ライブラリ プロジェクトを作成します。 最初のクラス ライブラリは、データセット (生成した型指定された `DataSet` クラスと、アプリケーションのデータを保持する DataTables) を保持します。 このプロジェクトは、アプリケーションのデータ エンティティ層として使用され、通常は中間層に配置されます。 データセットにより初期データセットが作成され、コードが自動的に 2 つのクラス ライブラリに分離されます。

> [!NOTE]
> **[OK]** をクリックする前に、必ずプロジェクトとソリューションに適切な名前を付けてください。 これにより、チュートリアルの完了が容易になります。

### <a name="to-create-the-n-tier-solution-and-dataentitytier-class-library"></a>n 層ソリューションと DataEntityTier クラス ライブラリを作成するには

1. Visual Studio の **[ファイル]** メニューで､ **[新規作成]**  >  **[プロジェクト]** を選択します。

2. 左側のペインで **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。

3. 中央のペインで、 **[クラス ライブラリ]** プロジェクトの種類を選択します。

4. プロジェクトに「**DataEntityTier**」という名前を付けます。

5. ソリューションに「**NTierWalkthrough**」という名前を付けて、 **[OK]** を選択します。

     DataEntityTier プロジェクトを含む NTierWalkthrough ソリューションが作成され、**ソリューション エクスプローラー** に追加されます。

## <a name="create-the-class-library-to-hold-the-tableadapters-dataaccesstier"></a>TableAdapter を保持するクラス ライブラリを作成する (DataAccessTier)
DataEntityTier プロジェクトを作成したら、次に、クラス ライブラリ プロジェクトをもう 1 つ作成します。 このプロジェクトは、生成された TableAdapter を保持し、アプリケーションの "*データ アクセス層*" と呼ばれます。 データ アクセス層は、データベースへの接続に必要な情報を格納し、通常、中間層に置かれます。

### <a name="to-create-a-separate-class-library-for-the-tableadapters"></a>TableAdapter 用の別のクラス ライブラリを作成するには

1. **ソリューション エクスプローラー** でソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの中央のペインで、 **[クラス ライブラリ]** を選択します。

3. プロジェクトに「**DataAccessTier**」という名前を付けて、 **[OK]** を選択します。

     DataAccessTier プロジェクトが作成され、NTierWalkthrough ソリューションに追加されます。

## <a name="create-the-dataset"></a>データセットを作成する
次に、型指定されたデータセットを作成します。 型指定されたデータセットは、データセット クラス (`DataTables` クラスを含む) と `TableAdapter` クラスの両方を含む単一のプロジェクトとして作成されます。 (すべてのクラスは 1 つのファイルに生成されます)。データセットと TableAdapter を異なるプロジェクトに分けたら、データセット クラスは他のプロジェクトに移動し、`TableAdapter` クラスは元のプロジェクトのままにします。 このため、最終的に TableAdapter が含まれるプロジェクト (DataAccessTier プロジェクト) にデータセットを作成します。 **データ ソース構成ウィザード** を使用して、データセットを作成します。

> [!NOTE]
> 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプル データベースの設定の詳細については、[サンプル データベースをインストールする方法](../data-tools/installing-database-systems-tools-and-samples.md)に関する記事を参照してください。

### <a name="to-create-the-dataset"></a>データセットを作成するには

1. **ソリューション エクスプローラー** で、**DataAccessTier** を選択します。

2. **[データ]** メニューで、 **[データ ソースの表示]** を選択します。

   **[データ ソース]** ウィンドウが開きます。

3. **[データ ソース]** ウィンドウで、 **[新しいデータ ソースの追加]** をクリックして **データ ソース構成ウィザード** を起動します。

4. **[データ ソースの種類の選択]** ページで **[データベース]** を選択し、 **[次へ]** を選択します。

5. **[データ接続の選択]** ページで、次のいずれかの操作を行います。

     Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。

     または

     **[新しい接続]** を選択して、 **[接続の追加]** ダイアログ ボックスを表示します。

6. データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、 **[次へ]** を選択します。

    > [!NOTE]
    > SQL Server に接続するのではなく、ローカル データベース ファイルを選択した場合は、ファイルをプロジェクトに追加するかどうかをたずねるメッセージが表示されます。 **[はい]** を選択して、データベース ファイルをプロジェクトに追加します。

7. **[アプリケーション構成ファイルに接続文字列を保存]** ページで、 **[次へ]** を選択します。

8. **[データベース オブジェクトの選択]** ページの **[テーブル]** ノードを展開します。

9. **Customers** テーブルと **Orders** テーブルのチェック ボックスをオンにして、 **[完了]** を選択します。

     NorthwindDataSet が DataAccessTier プロジェクトに追加され、**[データ ソース]** ウィンドウに表示されます。

## <a name="separate-the-tableadapters-from-the-dataset"></a>データセットと TableAdapter を分離する
データセットを作成したら、生成されたデータセット クラスを TableAdapter から分離します。 これを行うには、**[DataSet プロジェクト]** プロパティを、分離されたデータセット クラスを格納するプロジェクトの名前に設定します。

### <a name="to-separate-the-tableadapters-from-the-dataset"></a>データセットと TableAdapter を分離するには

1. **ソリューション エクスプローラー** で **NorthwindDataSet.xsd** をダブルクリックし、**データセット デザイナー** でデータセットを開きます。

2. デザイナーの空の領域を選択します。

3. **[プロパティ]** ウィンドウで **[DataSet プロジェクト]** ノードを見つけます。

4. **[DataSet プロジェクト]** ボックスの一覧で、**DataEntityTier** を選択します。

5. **[ビルド]** メニューの **[ソリューションのビルド]** を選択します。

   データセットと TableAdapter が、2 つのクラス ライブラリ プロジェクトに分離されます。 最初にデータセット全体 (`DataAccessTier`) が含まれていたプロジェクトに、現在は TableAdapter しか含まれません。 **[DataSet プロジェクト]** プロパティで指定したプロジェクト (`DataEntityTier`) には、型指定されたデータセット *NorthwindDataSet.Dataset.Designer.vb* (または *NorthwindDataSet.Dataset.Designer.cs*) が含まれます。

> [!NOTE]
> **[DataSet プロジェクト]** プロパティを設定してデータセットと TableAdapter を分離する場合でも、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

## <a name="create-a-new-service-application"></a>新しいサービス アプリケーションを作成する
このチュートリアルでは WCF サービスを使用してデータ アクセス層にアクセスする方法を説明するので、新しい WCF サービス アプリケーションを作成します。

### <a name="to-create-a-new-wcf-service-application"></a>新しい WCF サービス アプリケーションを作成するには

1. **ソリューション エクスプローラー** でソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの左側のペインで、 **[WCF]** を選択します。 中央のペインで、 **[WCF サービス ライブラリ]** を選択します。

3. プロジェクトに「**DataService**」という名前を付け、 **[OK]** を選択します。

     DataService プロジェクトが作成されて NTierWalkthrough ソリューションに追加されます。

## <a name="create-methods-in-the-data-access-tier-to-return-the-customers-and-orders-data"></a>顧客と注文のデータを返すデータ アクセス層のメソッドを作成する
データ サービスでは、データ アクセス層の 2 つのメソッド (`GetCustomers` と `GetOrders`) を呼び出す必要があります。 これらのメソッドからは、Northwind の `Customers` と `Orders` テーブルが返されます。 `DataAccessTier` プロジェクトで `GetCustomers` と `GetOrders` メソッドを作成します。

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-customers-table"></a>Customers テーブルを返すメソッドをデータ アクセス層に作成するには

1. **ソリューション エクスプローラー** で **NorthwindDataset.xsd** をダブルクリックして、データセットを開きます。

2. **CustomersTableAdapter** を右クリックし、 **[クエリの追加]** をクリックします。

3. **[コマンドの種類を選択します]** ページで、**[SQL ステートメントを使用する]** の既定値を受け入れ、**[次へ]** をクリックします。

4. **[クエリの種類の選択]** ページで、**[複数行を返す SELECT]** の既定値を受け入れ、**[次へ]** をクリックします。

5. **[SQL SELECT ステートメントの指定]** ページで、既定のクエリを受け入れ、**[次へ]** をクリックします。

6. **[生成するメソッドの選択]** ページで、**[DataTable を返す]** セクションの **[メソッド名]** に「**GetCustomers**」と入力します。

7. **[完了]** をクリックします。

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-orders-table"></a>Orders テーブルを返すメソッドをデータ アクセス層に作成するには

1. **[OrdersTableAdapter]** を右クリックし、**[クエリの追加]** をクリックします。

2. **[コマンドの種類を選択します]** ページで、**[SQL ステートメントを使用する]** の既定値を受け入れ、**[次へ]** をクリックします。

3. **[クエリの種類の選択]** ページで、**[複数行を返す SELECT]** の既定値を受け入れ、**[次へ]** をクリックします。

4. **[SQL SELECT ステートメントの指定]** ページで、既定のクエリを受け入れ、**[次へ]** をクリックします。

5. **[生成するメソッドの選択]** ページで、**[DataTable を返す]** セクションの **[メソッド名]** に「**GetOrders**」と入力します。

6. **[完了]** をクリックします。

7. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="add-a-reference-to-the-data-entity-and-data-access-tiers-to-the-data-service"></a>データ エンティティ層とデータ アクセス層への参照をデータ サービスに追加する
データ サービスはデータセットと TableAdapter の情報を必要とするため、**DataEntityTier** プロジェクトおよび **DataAccessTier** プロジェクトへの参照を追加します。

### <a name="to-add-references-to-the-data-service"></a>データ サービスに参照を追加するには

1. **ソリューション エクスプローラー** で、**[DataService]** を右クリックし、**[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスの **[プロジェクト]** タブをクリックします。

3. **[DataAccessTier]** プロジェクトと **[DataEntityTier]** プロジェクトの両方を選択します。

4. **[OK]** をクリックします。

## <a name="add-functions-to-the-service-to-call-the-getcustomers-and-getorders-methods-in-the-data-access-tier"></a>データ アクセス層の GetCustomers と GetOrders メソッドを呼び出す関数をサービスに追加する
これで、データを返すメソッドをデータ アクセス層に含めることができました。次に、データ サービスにメソッドを作成して、データ アクセス層のメソッドを呼び出します。

> [!NOTE]
> C# プロジェクトの場合は、次のコードをコンパイルするために `System.Data.DataSetExtensions` アセンブリへの参照を追加する必要があります。

### <a name="to-create-the-getcustomers-and-getorders-functions-in-the-data-service"></a>データ サービスに GetCustomers 関数と GetOrders 関数を作成するには

1. **DataService** プロジェクトで、**IService1.vb** または **IService1.cs** をダブルクリックします。

2. **[Add your service operations here]** というコメントの下に、次のコードを追加します。

    ```vb
    <OperationContract()> _
    Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable

    <OperationContract()> _
    Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable
    ```

    ```csharp
    [OperationContract]
    DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers();

    [OperationContract]
    DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders();
    ```

3. DataService プロジェクトで、**Service1.vb** または **Service1.cs** をダブルクリックします。

4. **Service1** クラスに次のコードを追加します。

    ```vb
    Public Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable Implements IService1.GetCustomers
        Dim CustomersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
        Return CustomersTableAdapter1.GetCustomers()
    End Function

    Public Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable Implements IService1.GetOrders
        Dim OrdersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
        Return OrdersTableAdapter1.GetOrders()
    End Function
    ```

    ```csharp
    public DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
             CustomersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter();
        return CustomersTableAdapter1.GetCustomers();
    }
    public DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
             OrdersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter();
        return OrdersTableAdapter1.GetOrders();
    }
    ```

5. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

## <a name="create-a-presentation-tier-to-display-data-from-the-data-service"></a>データ サービスのデータを表示するプレゼンテーション層を作成する
これで、データ アクセス層を呼び出すメソッドを持つデータ サービスをソリューションに含めることができました。次に、データ サービスを呼び出してデータをユーザーに表示する別のプロジェクトを作成します。 このチュートリアルでは、Windows フォーム アプリケーションを作成します。これは n 層アプリケーションのプレゼンテーション層です。

### <a name="to-create-the-presentation-tier-project"></a>プレゼンテーション層プロジェクトを作成するには

1. **ソリューション エクスプローラー** でソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** を選択します。

2. **[新しいプロジェクト]** ダイアログ ボックスの左側のペインで、 **[Windows デスクトップ]** を選択します。 中央のペインで、 **[Windows フォーム アプリ]** を選択します。

3. プロジェクトに「**PresentationTier**」という名前を付け、**[OK]** をクリックします。

    PresentationTier プロジェクトが作成され、NTierWalkthrough ソリューションに追加されます。

## <a name="set-the-presentationtier-project-as-the-startup-project"></a>スタートアップ プロジェクトとして PresentationTier プロジェクトを設定する
**PresentationTier** プロジェクトをソリューションのスタートアップ プロジェクトとして設定します。これは、データを表示して操作する実際のクライアント アプリケーションであるためです。

### <a name="to-set-the-new-presentation-tier-project-as-the-startup-project"></a>新しいプレゼンテーション層プロジェクトをスタートアップ プロジェクトとして設定するには

- **ソリューション エクスプローラー** で、**[PresentationTier]** を右クリックし、**[スタートアップ プロジェクトに設定]** をクリックします。

## <a name="add-references-to-the-presentation-tier"></a>プレゼンテーション層への参照を追加する
クライアント アプリケーションである PresentationTier には、サービスのメソッドにアクセスできるように、データ サービスへのサービス参照が必要です。 また、WCF サービスによる型の共有を有効にするために、データセットへの参照も必要です。 データセット部分クラスに追加したコードは、データ サービスを介した型の共有を有効にするまで、プレゼンテーション層で使用することはできません。 通常は、データ テーブルの行と列の変更イベントに検証コードなどのコードを追加するため、クライアントからこのコードにアクセスすることが必要になります。

### <a name="to-add-a-reference-to-the-presentation-tier"></a>プレゼンテーション層に参照を追加するには

1. **ソリューション エクスプローラー** で、**PresentationTier** を右クリックして、 **[参照の追加]** を選択します。

2. **[参照の追加]** ダイアログ ボックスで、 **[プロジェクト]** タブを選択します。

3. **DataEntityTier** を選択し、 **[OK]** を選択します。

### <a name="to-add-a-service-reference-to-the-presentation-tier"></a>プレゼンテーション層にサービス参照を追加するには

1. **ソリューション エクスプローラー** で、**PresentationTier** を右クリックし、 **[サービス参照の追加]** を選択します。

2. **[サービス参照の追加]** ダイアログ ボックスで **[探索]** を選択します。

3. **Service1** を選択し、 **[OK]** を選択します。

    > [!NOTE]
    > 現在のコンピューターに複数のサービスがある場合は、このチュートリアルで以前に作成したサービス (`GetCustomers` および `GetOrders` メソッドを含むサービス) を選択します。

## <a name="add-datagridviews-to-the-form-to-display-the-data-returned-by-the-data-service"></a>データ サービスから返されたデータを表示するための DataGridView をフォームに追加する
データ サービスへのサービス参照を追加すると、サービスによって返されたデータが **[データ ソース]** ウィンドウに自動的に読み込まれます。

### <a name="to-add-two-data-bound-datagridviews-to-the-form"></a>フォームに 2 つのデータ バインド DataGridView を追加するには

1. **ソリューション エクスプローラー** で、**PresentationTier** プロジェクトを選択します。

2. **[データ ソース]** ウィンドウの **[NorthwindDataSet]** を展開し、**[Customers]** ノードを見つけます。

3. **[Customers]** ノードを Form1 にドラッグします。

4. **[データ ソース]** ウィンドウの **[Customers]** ノードを展開し、関連する **[Orders]** ノード (**[Customers]** ノードに入れ子になっている **[Orders]** ノード) を見つけます。

5. 関連する **[Orders]** ノードを Form1 にドラッグします。

6. フォームの空の領域をダブルクリックして、`Form1_Load` イベント ハンドラーを作成します。

7. `Form1_Load` イベント ハンドラーに次のコードを追加します。

    ```vb
    Dim DataSvc As New ServiceReference1.Service1Client
    NorthwindDataSet.Customers.Merge(DataSvc.GetCustomers)
    NorthwindDataSet.Orders.Merge(DataSvc.GetOrders)
    ```

    ```csharp
    ServiceReference1.Service1Client DataSvc =
        new ServiceReference1.Service1Client();
    northwindDataSet.Customers.Merge(DataSvc.GetCustomers());
    northwindDataSet.Orders.Merge(DataSvc.GetOrders());
    ```

## <a name="increase-the-maximum-message-size-allowed-by-the-service"></a>サービスで許可されるメッセージの最大サイズを増やす
`maxReceivedMessageSize` の既定値は、`Customers` および `Orders` テーブルから取得したデータを保持するのに十分な大きさではありません。 次の手順では、その値を 6,553,600 に増やします。 クライアントで値を変更すると、サービス参照が自動的に更新されます。

> [!NOTE]
> 既定のサイズが低く設定されているのは、サービス拒否 (DoS) 攻撃を受けるリスクを低減するためです。 詳細については、「<xref:System.ServiceModel.WSHttpBindingBase.MaxReceivedMessageSize%2A>」を参照してください。

### <a name="to-increase-the-maxreceivedmessagesize-value"></a>maxReceivedMessageSize 値を増やすには

1. **ソリューション エクスプローラー** で、**PresentationTier** プロジェクトの **app.config** ファイルをダブルクリックします。

2. **maxReceivedMessage** サイズ属性を見つけ、値を「`6553600`」に変更します。

## <a name="test-the-application"></a>アプリケーションをテストする
**F5** キーを押してアプリケーションを実行します。 `Customers` および `Orders` テーブルのデータがデータ サービスから取得され、フォームに表示されます。

## <a name="next-steps"></a>次のステップ
Windows ベース アプリケーションに関連データを保存した後で、アプリケーションの要件によってはさらに操作を追加する必要があります。 たとえば、このアプリケーションに対して次のような拡張を行うことができます。

- データセットへの検証の追加。

- サービスへの、データを更新してデータベースに戻す追加メソッドの追加。

## <a name="see-also"></a>こちらもご覧ください

- [n 層アプリケーションでのデータセットの操作](../data-tools/work-with-datasets-in-n-tier-applications.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
