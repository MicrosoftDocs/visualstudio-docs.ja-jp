---
title: ビジネス データを使用して SharePoint に外部リストを作成する
description: ビジネス データベース内の連絡先に関する情報を返す BDC サービスのモデルを作成し、その後、このモデルを使用して SharePoint に外部リストを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], external list
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], external list
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0811b029bf7e4705bc0c3689eff73f38280c3b3d
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217685"
---
# <a name="walkthrough-create-an-external-list-in-sharepoint-by-using-business-data"></a>チュートリアル: ビジネス データを使用して SharePoint で外部リストを作成する

ビジネス データ接続 (BDC) サービスを使用すると、SharePoint で、バックエンド サーバー アプリケーション、Web サービス、データベースのビジネス データを表示できます。

このチュートリアルでは、サンプル データベースに含まれる連絡先に関する情報を返すという、BDC サービスのモデルを作成する方法について説明します。 次に、このモデルを使用して、SharePoint に外部リストを作成します。

このチュートリアルでは、次の作業について説明します。

- プロジェクトの作成。
- モデルへのエンティティの追加。
- Finder メソッドの追加。
- SpecificFinder メソッドの追加。
- プロジェクトのテスト。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Windows と SharePoint

- AdventureWorks サンプル データベースにアクセスします。 AdventureWorks データベースをインストールする方法の詳細については、[SQL Server サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)に関するページを参照してください。

## <a name="create-a-project-that-contains-a-bdc-model"></a>BDC モデルを含むプロジェクトを作成する

1. Visual Studio のメニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **[Visual C#]** または **[Visual Basic]** のどちらかで、 **[SharePoint]** ノードを展開し、 **[2010]** 項目を選択します。

3. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** を選択し、プロジェクトに **AdventureWorksTest** という名前を付けて、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。 このウィザードでは、プロジェクトのデバッグ時に使用するサイトやソリューションの信頼レベルを設定できます。

4. **[ファーム ソリューションとして配置する]** オプションボタンをクリックして、信頼レベルを設定します。

5. **[完了]** をクリックして、既定のローカル SharePoint サイトを作成します。

6. **ソリューション エクスプローラー** で、[SharePoint] プロジェクト ノードをクリックします。

7. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが開きます。

8. **[テンプレート]** ペインで、 **[ビジネス データ接続モデル (ファーム ソリューションのみ)]** を選択し、プロジェクトに **AdventureWorksContacts** という名前を付けて、 **[追加]** をクリックします。

## <a name="add-data-access-classes-to-the-project"></a>プロジェクトにデータ アクセス クラスを追加する

1. メニュー バーで、 **[ツール]**  >  **[データベースへの接続]** の順に選択します。

     **[接続の追加]** ダイアログ ボックスが表示されます。

2. SQL Server AdventureWorks サンプル データベースへの接続を追加します。

     詳細については、「[接続の追加/変更 (Microsoft SQL Server)](/previous-versions/dxb6fxah(v=vs.140))」を参照してください。

3. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

4. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

5. **[インストールされたテンプレート]** ペインで、 **[データ]** ノードを選択します。

6. **[テンプレート]** ペインで、 **[LINQ to SQL クラス]** を選択します。

7. **[名前]** ボックスで「**AdventureWorks**」と指定してから、 **[追加]** を選択します。

     .dbml ファイルがプロジェクトに追加され、オブジェクト リレーショナル デザイナー (O/R デザイナー) が開きます。

8. メニュー バーで、 **[表示]**  >  **[サーバー エクスプローラー]** を選択します。

9. **サーバー エクスプローラー** で、AdventureWorks サンプル データベースを表すノードを展開し、 **[テーブル]** ノードを展開します。

10. O/R デザイナーに **[連絡担当者]** テーブルを追加します。

     エンティティ クラスが作成され、デザイン サーフェイスに表示されます。 このエンティティ クラスには、[連絡担当者] テーブルの列にマップされるプロパティが含まれています。

## <a name="remove-the-default-entity-from-the-bdc-model"></a>BDC モデルから既定のエンティティを削除する

**ビジネス データ接続モデル** プロジェクトによって、Entity1 という名前の既定のエンティティがモデルに追加されます。 このエンティティを削除します。 後で、新しいエンティティを追加します。 空のモデルから開始すると、このチュートリアルを行うために必要な手順の数が減ります。

1. **ソリューション エクスプローラー** で、 **[BdcModel1]** ノードを展開し、*BdcModel1.bdcm* ファイルを開きます。

2. ビジネス データ接続モデル ファイルが BDC デザイナーで開きます。

3. デザイナーで、**Entity1** のショートカット メニューを開き、 **[削除]** を選択します。

4. **ソリューション エクスプローラー** で、*Entity1.vb* (Visual Basic の場合) または *Entity1.cs* (C# の場合) のショートカット メニューを開き、 **[削除]** を選択します。

5. *Entity1Service.vb* (Visual Basic の場合) または *Entity1Service.cs* (C# の場合) のショートカット メニューを開き、 **[削除]** を選択します。

## <a name="add-an-entity-to-the-model"></a>モデルにエンティティを追加する

モデルにエンティティを追加します。 エンティティは、Visual Studio の **ツールボックス** から BDC デザイナーに追加できます。

1. メニュー バーで **[表示]** 、 **[ツールボックス]** の順にクリックします。

2. **ツールボックス** の **[BusinessDataConnectivity]** タブで、BDC デザイナーに **エンティティ** を追加します。

     新しいエンティティがデザイナーに表示されます。 Visual Studio によって、*EntityService.vb* (Visual Basic の場合) または *EntityService.cs* (C# の場合) という名前のファイルがプロジェクトに追加されます。

3. メニュー バーで **[表示]**  >  **[プロパティ]**  >  **[ウィンドウ]** の順に選択します。

4. **[プロパティ]** ウィンドウで、 **[名前]** プロパティ値を「**Contact**」に設定します。

5. デザイナーで、エンティティのショートカット メニューを開き、 **[追加]** を選択してから、 **[識別子]** を選択します。

     新しい識別子がエンティティに表示されます。

6. **[プロパティ]** ウィンドウで、識別子の名前を **ContactID** に変更します。

7. **[型名]** ボックスの一覧で、 **[System.Int32]** を選択します。

## <a name="add-a-specific-finder-method"></a>SpecificFinder メソッドを追加する

BDC サービスで特定の連絡先を表示できるようにするには、SpecificFinder メソッドを追加する必要があります。 ユーザーが一覧の項目を選択し、リボンの **[項目の表示]** をクリックすると、BDC サービスにより SpecificFinder メソッドが呼び出されます。

**[BDC メソッドの詳細]** ウィンドウを使用して、SpecificFinder メソッドを Contact エンティティに追加します。 SpecificFinder を返すには、コードをメソッドに追加します。

1. BDC デザイナーで、**Contact** エンティティを選択します。

2. メニュー バーで、 **[表示]**  >  **[その他のウィンドウ]**  >  **[BDC メソッドの詳細]** の順に選択します。

     [BDC メソッドの詳細] ウィンドウが開きます。

3. **[メソッドの追加]** 一覧で、 **[Specific Finder メソッドの作成]** を選択します。

     Visual Studio により、次の要素がモデルに追加されます。 これらの要素は、 **[BDC メソッドの詳細]** ウィンドウに表示されます。

    - ReadItem という名前のメソッド。

    - メソッドの入力パラメーター。

    - メソッドの戻り値パラメーター。

    - 各パラメーターの型記述子。

    - メソッドのメソッド インスタンス。

4. **[BDC メソッドの詳細]** ウィンドウで、**Contact** 型記述子に対して表示される一覧を開き、 **[編集]** を選択します。

     **BDC エクスプローラー** が開き、モデルの階層ビューが表示されます。

5. **[プロパティ]** ウィンドウで、**TypeName** プロパティの横にある一覧を開き、 **[現在のプロジェクト]** タブを選択し、**Contact** プロパティを選択します。

6. **BDC エクスプローラー** で、**Contact** のショートカット メニューを開き、 **[型記述子の追加]** をクリックします。

     **TypeDescriptor1** という名前の新しい型記述子が、**BDC エクスプローラー** に表示されます。

7. **[プロパティ]** ウィンドウで、 **[名前]** プロパティの値を「**ContactID**」に設定します。

8. **TypeName** プロパティの横にある一覧を開き、 **[Int32]** を選択します。

9. **Identifier** プロパティの横にある一覧を開き、 **[ContactID]** を選択します。

10. 手順 6 を繰り返して、次の各フィールドの型記述子を作成します。

    |名前|種類名|
    |----------|---------------|
    |FirstName|System.String|
    |LastName|System.String|
    |Phone|System.String|
    |EmailAddress|System.String|
    |EmailPromotion|System.Int32|
    |NameStyle|System.Boolean|
    |PasswordHash|System.String|
    |PasswordSalt|System.String|

11. BDC デザイナーの **Contact** エンティティで、**ReadItem** メソッドを開きます。

     コード エディターで Contact サービス コード ファイルが開きます。

12. `ContactService` クラスで、`ReadItem` メソッドを次のコードに置き換えます。 このコードは、以下のタスクを実行します。

    - AdventureWorks データベースの Contact テーブルからレコードを取得します。

    - Contact エンティティが BDC サービスに返されます。

    > [!NOTE]
    > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet3":::

## <a name="add-a-finder-method"></a>Finder メソッドを追加する

BDC サービスで一覧に連絡先を表示できるようにするには、Finder メソッドを追加する必要があります。 **[BDC メソッドの詳細]** ウィンドウを使用して、Finder メソッドを Contact エンティティに追加します。 BDC サービスにエンティティのコレクションを返すには、メソッドにコードを追加します。

1. BDC デザイナーで、**Contact** エンティティを選択します。

2. **[BDC メソッドの詳細]** ウィンドウで **[ReadItem]** ノードを折りたたみます。

3. **ReadList** メソッドの下にある **[メソッドの追加]** ボックスの一覧で、 **[Finder メソッドの作成]** を選択します。

     Visual Studio によって、メソッド、戻り値パラメーター、型記述子が追加されます。

4. BDC デザイナーの **Contact** エンティティで、**ReadList** メソッドを開きます。

     連絡先サービスのコード ファイルがコード エディターで開きます。

5. `ContactService` クラスで、`ReadList` メソッドを次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - AdventureWorks データベースの Contacts テーブルからデータを取得します。

   - BDC サービスに Contact エンティティの一覧を返します。

     > [!NOTE]
     > `ServerName` フィールドの値をサーバーの名前に置き換えてください。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb" id="Snippet2":::

## <a name="test-the-project"></a>プロジェクトをテストする

プロジェクトを実行すると、SharePoint サイトが開き、Visual Studio によってビジネス データ接続サービスにモデルが追加されます。 Contact エンティティを参照する外部リストを SharePoint に作成します。 AdventureWorks データベースにおける連絡先のデータが一覧に表示されます。

> [!NOTE]
> ソリューションをデバッグする前に、SharePoint のセキュリティ設定を変更することが必要になる場合があります。 詳細については、[ビジネス データ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)に関するページを参照してください。

1. **F5** キーを押します。

     SharePoint サイトが開きます。

2. **[サイトの操作]** メニューで **[その他のオプション]** コマンドをクリックします。

3. **[作成]** ページで、 **[外部リスト]** テンプレートを選択し、 **[作成]** をクリックします。

4. カスタム リストに **Contacts** という名前を付けます。

5. **[外部コンテンツ タイプ]** フィールドの横にある参照ボタンをクリックします。

6. **[外部コンテンツタイプの選択]** ダイアログ ボックスで、 **[AdventureWorksContacts.BdcModel1.Contact]** 項目を選択し、 **[作成]** をクリックします。

     SharePoint では、AdventureWorks サンプル データベースの連絡先を含む外部リストが作成されます。

7. SpecificFinder メソッドをテストするには、一覧で連絡先を選択します。

8. リボンで **[項目]** タブを選択してから、 **[項目の表示]** コマンドを選択します。

     選択した連絡先の詳細がフォームに表示されます。

## <a name="next-steps"></a>次のステップ

SharePoint で BDC サービスのモデルを設計する方法の詳細については、次のトピックを参照してください。

- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)。
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)。
- [方法: Deleter メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)。

## <a name="see-also"></a>関連項目

[ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md) 
 [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md) 
 [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md) 
 [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)