---
title: 'チュートリアル: 実行時にリボンのコントロールを更新する'
description: Office アプリケーションにリボンを読み込んだ後に、リボン オブジェクト モデルを使用してリボン上のコントロールを更新する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- updating Ribbon controls
- Ribbon [Office development in Visual Studio], dynamic menu
- dynamic menus [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], updating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7cf9bbe73bd43fa01aec8e7d0dec42fd8301ff30
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827527"
---
# <a name="walkthrough-update-the-controls-on-a-ribbon-at-run-time"></a>チュートリアル: 実行時にリボンのコントロールを更新する

このチュートリアルでは、Office アプリケーションにリボンを読み込んだ後に、リボン オブジェクト モデルを使用してリボン上のコントロールを更新する方法について説明します。

[!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

この例では、Northwind サンプル データベースからデータを取得し、Microsoft Office Outlook のコンボ ボックスとメニューに読み込みます。 これらのコントロールで選択した項目は、電子メール メッセージの **[宛先]** や **[件名]** などのフィールドに自動的に読み込まれます。

このチュートリアルでは、次の作業について説明します。

- 新しい Outlook VSTO アドイン プロジェクトを作成します。

- カスタム リボン グループをデザインします。

- 組み込みタブにカスタム グループを追加します。

- 実行時にリボン上のコントロールを更新します。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Outlook

## <a name="create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成する

まず、Outlook VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、**Ribbon_Update_At_Runtime** という名前の Outlook VSTO アドイン プロジェクトを作成します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。

3. プロジェクトを既定のプロジェクト ディレクトリに保存します。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

## <a name="design-a-custom-ribbon-group"></a>カスタム リボン グループをデザインする

この例のリボンは、ユーザーが新しいメール メッセージを作成するときに表示されます。 リボンのカスタム グループを作成するには、最初にプロジェクトにリボン項目を追加し、次にリボン デザイナーでグループをデザインします。 このカスタム グループを使用して、データベースから名前と注文履歴をプルし、顧客へのフォローアップ電子メール メッセージを生成できます。

### <a name="to-design-a-custom-group"></a>カスタム グループをデザインするには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (ビジュアル デザイナー)]** をクリックします。

3. 新しいリボンの名前を「**CustomerRibbon**」に変更し、 **[追加]** をクリックします。

     リボン デザイナーで *CustomerRibbon.cs* または *CustomerRibbon.vb* ファイルが開き、既定のタブとグループが表示されます。

4. リボン デザイナーをクリックして選択します。

5. **[プロパティ]** ウィンドウで、 **[RibbonType]** プロパティの隣のドロップダウン矢印をクリックし、 **[Microsoft.Outlook.Mail.Compose]** をクリックします。

     これにより、ユーザーが Outlook で新しいメール メッセージを作成するときにリボンを表示できます。

6. リボン デザイナーで、 **[Group1]** をクリックして選択します。

7. **[プロパティ]** ウィンドウで、 **[ラベル]** を「**顧客の購入**」に設定します。

8. **[ツールボックス]** の **[Office リボン コントロール]** タブから **[コンボ ボックス]** を **[顧客の購入]** グループにドラッグします。

9. **[ComboBox1]** をクリックして選択します。

10. **[プロパティ]** ウィンドウで、 **[ラベル]** を **[顧客]** に設定します。

11. **[ツールボックス]** の **[Office リボン コントロール]** タブから **[メニュー]** を **[顧客の購入]** グループにドラッグします。

12. **[プロパティ]** ウィンドウで、 **[ラベル]** を「**購入した製品**」に設定します。

13. **[ダイナミック]** を **true** に設定します。

     これにより、リボンが Office アプリケーションに読み込まれた後に、実行時にメニュー上のコントロールを追加および削除できます。

## <a name="add-the-custom-group-to-a-built-in-tab"></a>組み込みタブにカスタム グループを追加する

組み込みタブは、Outlook エクスプローラーまたはインスペクターのリボンに始めから含まれているタブです。 この手順では、組み込みタブにカスタム グループを追加し、タブ上のカスタム グループの位置を指定します。

### <a name="to-add-the-custom-group-to-a-built-in-tab"></a>組み込みタブにカスタム グループを追加するには

1. **[TabAddins (ビルトイン)]** タブをクリックして選択します。

2. **[プロパティ]** ウィンドウで、 **[ControlId]** プロパティを展開し、 **[OfficeId]** を **[TabNewMailMessage]** に設定します。

     これにより、 **[顧客の購入]** グループが、新しいメール メッセージ内に表示されるリボンの **[メッセージ]** タブに追加されます。

3. **[顧客の購入]** グループをクリックして選択します。

4. **[プロパティ]** ウィンドウで、 **[位置]** プロパティを展開し、 **[PositionType]** プロパティの隣にあるドロップダウン矢印をクリックして **[BeforeOfficeId]** をクリックします。

5. **[OfficeId]** プロパティを **[GroupClipboard]** に設定します。

     これにより、 **[顧客の購入]** グループが **[メッセージ]** タブの **[クリップボード]** グループの前に配置されます。

## <a name="create-the-data-source"></a>データ ソースを作成する

**[データ ソース]** ウィンドウを使用して、型指定されたデータセットをプロジェクトに追加します。

### <a name="to-create-the-data-source"></a>データ ソースを作成するには

1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

     これにより、**データ ソース構成ウィザード** が開始されます。

2. **[データベース]** を選択し、 **[次へ]** をクリックします。

3. **[データセット]** を選択し、 **[次へ]** をクリックします。

4. Microsoft SQL Server Compact 4.0 の Northwind サンプル データベースへのデータ接続を選択するか、または **[新しい接続]** ボタンを使用して新しい接続を追加します。

5. 接続を選択または作成した後で、 **[次へ]** をクリックします。

6. **[次へ]** をクリックして接続文字列を保存します。

7. **[データベース オブジェクトの選択]** ページの **[テーブル]** を展開します。

8. 次の各テーブルの横にあるチェック ボックスをオンにします。

    1. **顧客**

    2. **注文の詳細**

    3. **注文**

    4. **製品**

9. **[完了]** をクリックします。

## <a name="update-controls-in-the-custom-group-at-run-time"></a>実行時にカスタム グループ内のコントロールを更新する

リボン オブジェクト モデルを使用して、以下のタスクを実行します。

- **[顧客]** コンボ ボックスに顧客名を追加します。

- **[購入した製品]** メニューに、販売注文と販売済み製品を表すメニューおよびボタン コントロールを追加します。

- **[顧客]** コンボ ボックスと **[購入した製品]** メニューのデータを使用して、新しいメール メッセージの [宛先]、[件名]、および [本文] フィールドを設定します。

### <a name="to-update-controls-in-the-custom-group-by-using-the-ribbon-object-model"></a>リボン オブジェクト モデルを使用してカスタム グループのコントロールを更新するには

1. **[プロジェクト]** メニューの **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスで、 **[.NET]** タブをクリックし、**System.Data.Linq** アセンブリを選択して **[OK]** をクリックします。

    このアセンブリには、統合言語クエリ (LINQ) を使用するためのクラスが含まれています。 ここでは、LINQ を使用して Northwind データベースから取得したデータをカスタム グループのコントロールに読み込みます。

3. **ソリューション エクスプローラー** で、**CustomerRibbon.cs** または **CustomerRibbon.vb** をクリックして選択します。

4. **[表示]** メニューの **[コード]** をクリックします。

    コード エディターでリボン コード ファイルが開きます。

5. リボン コード ファイルの先頭に次のステートメントを追加します。 これらのステートメントによって、LINQ 名前空間や Outlook プライマリ相互運用機能アセンブリ (PIA) の名前空間に簡単にアクセスできます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet1":::

6. `CustomerRibbon` クラス内に次のコードを追加します。 このコードは、Northwind データベースの Customer、Orders、Order Details、および Product テーブルから取得した情報を格納するために使用するデータ テーブルおよびテーブル アダプターを宣言します。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet2":::

7. `CustomerRibbon` クラスに次のコード ブロックを追加します。 このコードによって、実行時にリボンのコントロールを作成する 3 つのヘルパー メソッドが追加されます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet3":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet3":::

8. `CustomerRibbon_Load` イベント ハンドラー メソッドを次のコードで置き換えます。 このコードは、LINQ クエリを使用して以下のタスクを実行します。

   - Northwind データベース内の 20 件の顧客の ID と名前を使用して **[顧客]** コンボ ボックスを設定します。

   - `PopulateSalesOrderInfo` ヘルパー メソッドを呼び出す。 このメソッドでは、現在選択されている顧客に関連する販売注文番号で **[購入した製品]** メニューを更新します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet4":::

9. 次のコードを `CustomerRibbon` クラスに追加します。 このコードは、LINQ クエリを使用して以下のタスクを実行します。

   - 選択されている顧客に関連する個々の販売注文を示すサブメニューを **[購入した製品]** メニューに追加します。

   - 販売注文に関連する製品を示すボタンを各サブメニューに追加する。

   - 各ボタンにイベントハンドラーを追加する。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet6":::

10. **ソリューション エクスプローラー** でリボン コード ファイルをダブルクリックします。

     リボン デザイナーが開きます。

11. リボン デザイナーで **[顧客]** コンボ ボックスをダブルクリックします。

     リボン コード ファイルがコード エディターで開き、`ComboBox1_TextChanged` イベント ハンドラーが表示されます。

12. `ComboBox1_TextChanged` イベント ハンドラーを次のコードで置き換えます。 このコードは、以下のタスクを実行します。

    - `PopulateSalesOrderInfo` ヘルパー メソッドを呼び出す。 このメソッドでは、選択されている顧客に関連する販売注文で **[購入した製品]** メニューを更新します。

    - `PopulateMailItem` ヘルパー メソッドを呼び出し、現在のテキスト (つまり、選択されている顧客の名前) を渡します。 このメソッドでは、新しいメール メッセージの [宛先]、[件名]、[本文] フィールドを設定します。

      :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet5":::
      :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet5":::

13. 次の `Click` イベント ハンドラーを `CustomerRibbon` クラスに追加します。 このコードでは、選択された製品の名前を新しいメール メッセージの [本文] フィールドに追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet8":::

14. 次のコードを `CustomerRibbon` クラスに追加します。 このコードは、以下のタスクを実行します。

    - 現在選択されている顧客の電子メール アドレスを使用して、新しいメール メッセージの [宛先] 行を設定します。

    - 新しいメール メッセージの [件名] と [本文] フィールドにテキストを追加します。

      :::code language="csharp" source="../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs" id="Snippet7":::
      :::code language="vb" source="../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb" id="Snippet7":::

## <a name="test-the-controls-in-the-custom-group"></a>カスタム グループのコントロールをテストする

Outlook で新しいメール フォームを開くと、リボンの **[メッセージ]** タブに **[顧客の購入]** というカスタム グループが表示されます。

顧客へのフォローアップ電子メール メッセージを作成するには、顧客を選択し、その顧客が購入した製品を選択します。 **[顧客の購入]** グループ内のコントロールが、実行時に Northwind データベースから取得されたデータで更新されます。

### <a name="to-test-the-controls-in-the-custom-group"></a>カスタム グループのコントロールをテストするには

1. **F5** キーを押してプロジェクトを実行します。

     Outlook が起動します。

2. Outlook で、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[メール メッセージ]** をクリックします。

     次のアクションが発生します。

    - 新しいメール メッセージのインスペクター ウィンドウが表示されます。

    - リボンの **[メッセージ]** タブで、 **[クリップボード]** グループの前に **[顧客の購入]** グループが表示されます。

    - そのグループ内の **[顧客]** コンボ ボックスが Northwind データベースに含まれる顧客の名前で更新されます。

3. リボンの **[メッセージ]** タブの **[顧客の購入]** グループで、 **[顧客]** コンボ ボックスから顧客を選択します。

     次のアクションが発生します。

    - **[購入した製品]** メニューが、選択されている顧客の個々の販売注文を示すように更新されます。

    - 個々の販売注文サブメニューが、その注文で購入された商品を示すように更新されます。

    - 選択されている顧客の電子メール アドレスがメール メッセージの **[宛先]** 行に追加され、メール メッセージの件名と本文にテキストが読み込まれます。

4. **[製品購入]** メニューをクリックし、いずれかの販売注文をポイントして、その販売注文に含まれる製品をクリックします。

     製品の名前がメール メッセージの本文に追加されます。

## <a name="next-steps"></a>次のステップ

Office UI をカスタマイズする方法の詳細については、次のトピックで説明します。

- ドキュメント レベルのカスタマイズにコンテキスト ベースの UI を追加する。 詳細については、「[操作ペインの概要](../vsto/actions-pane-overview.md)」を参照してください。

- 標準またはカスタムの Microsoft Office Outlook フォームを拡張する。 詳細については、「[チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)」を参照してください。

- Outlook にカスタム作業ウィンドウを追加する。 詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [統合言語クエリ (LINQ: Language-Integrated Query)](/dotnet/csharp/linq/index)
- [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [チュートリアル: リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)
- [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)
- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)
- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [方法: リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: アドインのユーザー インターフェイス エラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)