---
title: ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成 |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data binding, user controls
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6a1393f45c46709e4085d7e170265b92c6e00266
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219485"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成します。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Windows フォームでデータを表示する場合から既存のコントロールを選択することができます、**ツールボックス**、またはアプリケーションには、標準のコントロールで使用できない機能が必要な場合は、カスタム コントロールを作成できます。 このチュートリアルでは、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールには、データにバインドできるプロパティを 3 つ含めることができます。 このようなコントロールは、<xref:System.Windows.Forms.ComboBox> に似ています。  
  
 コントロールの作成の詳細については、[デザイン時に Windows フォーム コントロールの開発](http://msdn.microsoft.com/library/e5a8e088-7ec8-4fd9-bcb3-9078fd134829)を参照してください。  
  
 データ バインディングのシナリオで使用するためのコントロールを作成するときに、次のデータ バインディング属性のいずれかを実装する必要があります。  
  
|データ バインディング属性の使用方法|  
|-----------------------------------|  
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 詳細については、[単純データ バインディングをサポートする Windows フォーム ユーザー コントロール作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)を参照してください。|  
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 詳細については、[複合データ バインディングをサポートする Windows フォーム ユーザー コントロール作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)を参照してください。|  
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|  
  
 このチュートリアルでは、2 つのテーブルのデータにバインドする検索コントロールを作成します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。 この検索コントロールは `CustomerID` テーブルの `Orders` フィールドにバインドされます。 コントロールは、この値を使用して `CompanyName` テーブルの `Customers` を検索します。  
  
 このチュートリアルでは、次の作業を行う方法について説明します。  
  
-   新規作成**Windows アプリケーション**します。  
  
-   新しい追加**ユーザー コントロール**をプロジェクトにします。  
  
-   ユーザー コントロールをビジュアルに設計します。  
  
-   `LookupBindingProperty` 属性を実装します。  
  
-   使用してデータセットを作成、**データ ソースの構成**ウィザード。  
  
-   設定、 **CustomerID**列に、**注文**テーブル、**データ ソース**ウィンドウで、新しいコントロールを使用します。  
  
-   フォームを作成して、新しいコントロールにデータを表示します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを完了するための要件は次のとおりです。  
  
-   Northwind サンプル データベースにアクセスします。  
  
## <a name="create-a-windows-application"></a>Windows アプリケーションを作成します。  
 作成するには、まず、 **Windows アプリケーション**します。  
  
#### <a name="to-create-the-new-windows-project"></a>新しい Windows プロジェクトを作成するには  
  
1.  Visual Studio から、**ファイル**] メニューの [新規作成**プロジェクト**します。  
  
2.  プロジェクトに名前を**LookupControlWalkthrough**します。  
  
3.  選択**Windows フォーム アプリケーション**、 をクリック**OK**します。  
  
     **LookupControlWalkthrough**プロジェクトを作成するとに追加**ソリューション エクスプ ローラー**します。  
  
## <a name="add-a-user-control-to-the-project"></a>ユーザー コントロールをプロジェクトに追加します。  
 このチュートリアルからルックアップ コントロールを作成、**ユーザー コントロール**、ため、追加、**ユーザー コントロール**項目を**LookupControlWalkthrough**プロジェクト。  
  
#### <a name="to-add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加するには  
  
1.  **プロジェクト**メニューの **ユーザー コントロールの追加**します。  
  
2.  型`LookupBox`で、**名前**領域、およびクリック**追加**します。  
  
     **LookupBox**コントロールに追加されます**ソリューション エクスプ ローラー**、され、デザイナーが開きます。  
  
## <a name="design-the-lookupbox-control"></a>LookupBox コントロールをデザインします。  
  
#### <a name="to-design-the-lookupbox-control"></a>LookupBox コントロールを設計するには  
  
-   ドラッグ、<xref:System.Windows.Forms.ComboBox>から、**ツールボックス**ユーザー コントロールのデザイン サーフェイスにします。  
  
## <a name="add-the-required-data-binding-attribute"></a>必要なデータ バインディング属性を追加します。  
 データ バインディングをサポートする検索コントロールには、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装できます。  
  
#### <a name="to-implement-the-lookupbindingproperties-attribute"></a>LookupBindingProperties 属性を実装するには  
  
1.  スイッチ、 **LookupBox**コントロールをコード ビューにします。 (上、**ビュー** ] メニューの [選択**コード**)。  
  
2.  `LookupBox` のコードを次のコードで置き換えます。  
  
     [!code-csharp[VbRaddataDisplaying#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/LookupBox.cs#5)]
     [!code-vb[VbRaddataDisplaying#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/LookupBox.vb#5)]  
  
3.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
## <a name="create-a-data-source-from-your-database"></a>データベースからデータ ソースを作成します。  
 この手順を使用してデータ ソースを作成し、**データ ソースの構成**に基づいてウィザード、`Customers`と`Orders`Northwind サンプル データベース内のテーブル。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプル データベースのセットアップについては、[サンプル データベースの SQL Server のインストール](../data-tools/install-sql-server-sample-databases.md)を参照してください。  
  
#### <a name="to-create-the-data-source"></a>データ ソースを作成するには  
  
1.  **[データ]** メニューの **[データ ソースの表示]** をクリックします。  
  
2.  **データソース**ウィンドウで、**新しいデータ ソースの追加**を開始する、**データ ソースの構成**ウィザード。  
  
3.  **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **データ接続の選択**ページは、次のいずれか。  
  
    -   Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。  
  
    -   選択**新しい接続**を起動する、**接続の追加/変更** ダイアログ ボックス。  
  
5.  データベースにパスワードが必要な場合をクリックして、機密データを含めるオプションを選択**次**します。  
  
6.  **接続文字列をアプリケーション構成ファイルに保存**] ページで [**次**します。  
  
7.  **データベース オブジェクトの選択** ページで、展開、**テーブル**ノード。  
  
8.  選択、`Customers`と`Orders`テーブル、およびクリック**完了**します。  
  
     **NorthwindDataSet**がプロジェクトに追加、`Customers`と`Orders`に表示されるテーブル、**データ ソース**ウィンドウ。  
  
## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>LookupBox コントロールを使用して、Orders テーブルの CustomerID 列を設定します。  
 内で、**データソース**ウィンドウで、フォームに項目をドラッグする前に作成するコントロールを設定することができます。  
  
#### <a name="to-set-the-customerid-column-to-bind-to-the-lookupbox-control"></a>[CustomerID] 列を LookupBox コントロールにバインドするように設定するには  
  
1.  開いている**Form1**デザイナー。  
  
2.  展開、**顧客**内のノード、**データソース**ウィンドウ。  
  
3.  展開、**注文**ノード (で 1 つ、**顧客**ノードの下、 **Fax**列)。  
  
4.  ドロップダウン矢印をクリックして、**注文**ノード選択**詳細**コントロール リストから。  
  
5.  ドロップダウン矢印をクリックして、 **CustomerID**列 (で、**注文**ノード)、選択**カスタマイズ**します。  
  
6.  選択、 **LookupBox**の一覧から**関連付けられたコントロール**で、**データ UI カスタマイズ オプション** ダイアログ ボックス。  
  
7.  **[OK]** をクリックします。  
  
8.  ドロップダウン矢印をクリックして、 **CustomerID**列選択**LookupBox**します。  
  
## <a name="addcontrols-to-the-form"></a>フォームに Addcontrols  
 項目をドラッグして、データ バインド コントロールを作成することができます、**データソース**ウィンドウ**Form1**します。  
  
#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>Windows フォームにデータ バインディング コントロールを作成するには  
  
-   ドラッグ、**注文**ノードから、**データ ソース**ウィンドウから Windows フォームにことを確認します、 **LookupBox**コントロールを使用すると、データを表示、 `CustomerID`列です。  
  
## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>Customers テーブルから CompanyName を検索するコントロールをバインドします。  
  
#### <a name="to-setup-the-lookup-bindings"></a>検索バインドをセットアップするには  
  
-   メインの選択**顧客**内のノード、**データ ソース**ウィンドウとに、コンボ ボックスにドラッグ、 **CustomerIDLookupBox**で**Form1**.  
  
     これを表示するデータ バインディングが設定、`CompanyName`から、`Customers`を維持しながら、テーブル、`CustomerID`値から、`Orders`テーブル。  
  
## <a name="running-the-application"></a>アプリケーションの実行  
  
#### <a name="to-run-the-application"></a>アプリケーションを実行するには  
  
-   F5 キーを押してアプリケーションを実行します。  
  
-   一部のレコード間を移動し、いることを確認、`CompanyName`に表示されます、`LookupBox`コントロール。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

