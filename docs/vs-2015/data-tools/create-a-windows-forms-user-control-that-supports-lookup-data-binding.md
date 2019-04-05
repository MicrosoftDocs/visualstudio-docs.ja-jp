---
title: ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールの作成 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
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
manager: jillfra
ms.openlocfilehash: 786895d045b4ee43d9fbb8cb519fdd47d76b057a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58976895"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>ルックアップ データ バインディングをサポートする Windows フォーム ユーザー コントロールを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
フォームにデータを表示する場合は、**ツールボックス**から既存のコントロールを選択するか、またはアプリケーションが標準コントロールでは提供できない機能を必要とする場合は、カスタム コントロールを記述できます。 このチュートリアルでは、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールを作成する方法を示します。 <xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装するコントロールには、データにバインドできるプロパティを 3 つ含めることができます。 このようなコントロールは、<xref:System.Windows.Forms.ComboBox> に似ています。  
  
 コントロールの作成の詳細については、次を参照してください。[デザイン時に Windows フォーム コントロールの開発](http://msdn.microsoft.com/library/e5a8e088-7ec8-4fd9-bcb3-9078fd134829)します。  
  
 データ バインディングのシナリオで使用するためのコントロールを作成するときは、次のいずれかのデータ バインディング属性を実装する必要があります。  
  
|データ バインディング属性の使用方法|  
|-----------------------------------|  
|単一のデータ列またはプロパティを表示する <xref:System.ComponentModel.DefaultBindingPropertyAttribute> のような <xref:System.Windows.Forms.TextBox> を簡単なコントロールに実装します。 詳細については、次を参照してください。[単純データ バインディングをサポートする Windows フォーム ユーザー コントロール作成](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)です。|  
|データの一覧またはテーブルを表示する <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> のような <xref:System.Windows.Forms.DataGridView> をコントロールに実装します。 詳細については、次を参照してください。[複合データ バインディングをサポートする Windows フォーム ユーザー コントロール作成](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)です。|  
|データの一覧またはテーブルを表示しますが、単一の列またはプロパティを表示する必要もある <xref:System.ComponentModel.LookupBindingPropertiesAttribute> のような <xref:System.Windows.Forms.ComboBox> をコントロールに実装します。 このチュートリアルでは、このプロセスについて説明します。|  
  
 このチュートリアルでは、2 つのテーブルのデータにバインドする検索コントロールを作成します。 この例では、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルを使用します。 この検索コントロールは `CustomerID` テーブルの `Orders` フィールドにバインドされます。 コントロールは、この値を使用して `CompanyName` テーブルの `Customers` を検索します。  
  
 このチュートリアルでは、次の作業を行う方法について説明します。  
  
-   新規作成**Windows アプリケーション**します。  
  
-   新しい**ユーザー コントロール**をプロジェクトに追加します。  
  
-   ユーザー コントロールをビジュアルに設計します。  
  
-   `LookupBindingProperty` 属性を実装します。  
  
-   使用してデータセットを作成、**データ ソースの構成**ウィザード。  
  
-   **[データ ソース]** ウィンドウで **Orders** テーブルの **[CustomerID]** 列が新しいコントロールを使用するように設定します。  
  
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
  
     **LookupControlWalkthrough** プロジェクトが作成されて**ソリューション エクスプローラー**に追加されます。  
  
## <a name="add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加する  
 このチュートリアルでは**ユーザー コントロール**から検索コントロールを作成するので、**ユーザー コントロール**の項目を **LookupControlWalkthrough** プロジェクトに追加します。  
  
#### <a name="to-add-a-user-control-to-the-project"></a>プロジェクトにユーザー コントロールを追加するには  
  
1.  **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。  
  
2.  型`LookupBox`で、**名前**領域、およびクリック**追加**します。  
  
     **LookupBox** コントロールが **ソリューション エクスプローラー**に追加され、デザイナーが開きます。  
  
## <a name="design-the-lookupbox-control"></a>LookupBox コントロールをデザインします。  
  
#### <a name="to-design-the-lookupbox-control"></a>LookupBox コントロールを設計するには  
  
-   **ツールボックス**からユーザー コントロールのデザイン サーフェイスに <xref:System.Windows.Forms.ComboBox> をドラッグします。  
  
## <a name="add-the-required-data-binding-attribute"></a>必要なデータ バインディング属性を追加します。  
 データ バインディングをサポートする検索コントロールには、<xref:System.ComponentModel.LookupBindingPropertiesAttribute> を実装できます。  
  
#### <a name="to-implement-the-lookupbindingproperties-attribute"></a>LookupBindingProperties 属性を実装するには  
  
1.  **LookupBox** コントロールをコード ビューに切り替えます。 (**[表示]** メニューの **[コード]** を選択します。)  
  
2.  `LookupBox` のコードを次のコードで置き換えます。  
  
     [!code-csharp[VbRaddataDisplaying#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/LookupBox.cs#5)]
     [!code-vb[VbRaddataDisplaying#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/LookupBox.vb#5)]  
  
3.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
## <a name="create-a-data-source-from-your-database"></a>データベースからデータ ソースを作成します。  
 この手順では、**データ ソース構成**ウィザードを使用して、Northwind サンプル データベースの `Customers` テーブルと `Orders` テーブルに基づいてデータ ソースを作成します。 接続を作成するには、Northwind サンプル データベースへのアクセス権を持っている必要があります。 Northwind サンプル データベースのセットアップについては、次を参照してください。[サンプル データベースの SQL Server のインストール](../data-tools/install-sql-server-sample-databases.md)します。  
  
#### <a name="to-create-the-data-source"></a>データ ソースを作成するには  
  
1.  **[データ]** メニューの **[データ ソースの表示]** をクリックします。  
  
2.  **[データ ソース]** ウィンドウで、**[新しいデータ ソースの追加]** をクリックして**データ ソース構成**ウィザードを起動します。  
  
3.  **[データソースの種類を選択]** ページで、 **[データベース]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[データ接続の選択]** ページで、次のいずれかの操作を行います。  
  
    -   Northwind サンプル データベースへのデータ接続がドロップダウン リストに表示されている場合は選択します。  
  
    -   **[新しい接続]** を選択して **[接続の追加] または [接続の変更]** ダイアログ ボックスを表示します。  
  
5.  データベースにパスワードが必要な場合は、該当するオプションを選択して重要情報を含め、**[次へ]** をクリックします。  
  
6.  **[アプリケーション構成ファイルに接続文字列を保存]** ページで、**[次へ]** をクリックします。  
  
7.  **[データベース オブジェクトの選択]** ページで、**[テーブル]** ノードを展開します。  
  
8.  `Customers` テーブルと `Orders` テーブルを選択し、**[完了]** をクリックします。  
  
     プロジェクトに **NorthwindDataSet** が追加され、**[データ ソース]** ウィンドウに `Customers` テーブルと `Orders` テーブルが表示されます。  
  
## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>LookupBox コントロールを使用して、Orders テーブルの CustomerID 列を設定します。  
 **[データ ソース]** ウィンドウでは、フォームにコントロールをドラッグする前に作成するコントロールを設定できます。  
  
#### <a name="to-set-the-customerid-column-to-bind-to-the-lookupbox-control"></a>[CustomerID] 列を LookupBox コントロールにバインドするように設定するには  
  
1.  デザイナーで **Form1** を開きます。  
  
2.  **[データ ソース]** ウィンドウの **[Customers]** ノードを展開します。  
  
3.  **[Fax]** 列の下の **[Customers]** 列にある **[Orders]** ノードを展開します。  
  
4.  **[Orders]** ノードのドロップダウン矢印をクリックし、コントロール一覧の **[Details]** を選択します。  
  
5.  **[Orders]** ノードの **[CustomerID]** 列のドロップダウン矢印をクリックし、**[Customize]** をクリックします。  
  
6.  **[データ UI カスタマイズ オプション]** ダイアログ ボックスの **[関連付けられたコントロール]** の一覧の **[LookupBox]** を選択します。  
  
7.  **[OK]** をクリックします。  
  
8.  **[CustomerID]** 列のドロップダウン矢印をクリックし、**[LookupBox]** をクリックします。  
  
## <a name="addcontrols-to-the-form"></a>フォームに Addcontrols  
 **[データ ソース]** ウィンドウから **Form1** に項目をドラッグして、データ バインディング コントロールを作成します。  
  
#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>Windows フォームにデータ バインディング コントロールを作成するには  
  
-   ドラッグ、**注文**ノードから、**データ ソース**ウィンドウから Windows フォームにことを確認します、 **LookupBox**コントロールを使用すると、データを表示、 `CustomerID`列です。  
  
## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>Customers テーブルから CompanyName を検索するコントロールをバインドします。  
  
#### <a name="to-setup-the-lookup-bindings"></a>検索バインドをセットアップするには  
  
-   メインの選択**顧客**内のノード、**データ ソース**ウィンドウとに、コンボ ボックスにドラッグ、 **CustomerIDLookupBox**で**Form1**.  
  
     これによって、`Orders` テーブルの `CustomerID` 値を維持しながら、`Customers` テーブルの `CompanyName` を表示するためのデータ バインディングがセットアップされます。  
  
## <a name="running-the-application"></a>アプリケーションの実行  
  
#### <a name="to-run-the-application"></a>アプリケーションを実行するには  
  
-   F5 キーを押してアプリケーションを実行します。  
  
-   レコード間を移動し、`LookupBox` コントロールに `CompanyName` が表示されることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
