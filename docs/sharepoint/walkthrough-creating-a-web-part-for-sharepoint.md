---
title: 'チュートリアル: SharePoint の Web パーツを作成する | Microsoft Docs'
description: SharePoint の Web パーツを作成します。 Web パーツを使用すると、ブラウザーから SharePoint サイト ページのコンテンツ、外観、および動作を直接変更できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], developing
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3e018085bd9900a9ee04f838b7c802afd2acc4fe
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217711"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint"></a>チュートリアル: SharePoint の Web パーツの作成

Web パーツを使用すると、ブラウザーから SharePoint サイト ページのコンテンツ、外観、および動作を直接変更できます。 このチュートリアルでは、Visual Studio 2010 の **Web パーツ** 項目テンプレートを使用して、Web パーツを作成する方法について説明します。

この Web パーツのデータ グリッドには従業員が表示されます。 従業員データを格納するファイルの場所を指定します。 また、マネージャーである従業員のみが一覧に表示されるように、データ グリッドにフィルターをかけることもできます。

このチュートリアルでは、次の作業について説明します。

- Visual Studio **Web パーツ** 項目テンプレートを使用して Web パーツを作成する。

- Web パーツのユーザーが設定できるプロパティを作成する。 このプロパティでは、従業員データ ファイルの場所を指定します。

- コントロールを Web パーツ コントロール コレクションに追加することで Web パーツにコンテンツをレンダリングする。

- レンダリングされた Web パーツの動詞メニューに表示される、"*動詞*" という新しいメニュー項目を作成する。 動詞を使用すると、Web パーツに表示されるデータを変更できます。

- SharePoint の Web パーツをテストする。

    > [!NOTE]
    > 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- サポート対象エディションの Microsoft Windows および SharePoint。

- Visual Studio 2017 または Azure DevOps Services。

## <a name="create-an-empty-sharepoint-project"></a>空の SharePoint プロジェクトを作成する

まず、空の SharePoint プロジェクトを作成します。 後で、**Web パーツ** 項目テンプレートを使用してプロジェクトに Web パーツを追加します。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を、 **[管理者として実行]** オプションを使用して起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。

3. **[新しいプロジェクト]** ダイアログ ボックスで、使用する言語の **[SharePoint]** ノードを展開して、 **[2010]** ノードをクリックします。

4. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** を選択し、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。 このウィザードを使用すると、プロジェクトのデバッグに使用するサイトや、ソリューションの信頼レベルを選択できます。

5. **[ファーム ソリューションとして配置する]** オプション ボタンをクリックしてから、 **[完了]** をクリックして、ローカル SharePoint サイトの構成を既定値のままにします。

## <a name="add-a-web-part-to-the-project"></a>プロジェクトに Web パーツを追加する

プロジェクトに **[Web パーツ]** 項目を追加します。 **[Web パーツ]** 項目によって Web パーツ コード ファイルが追加されます。 後で、Web パーツ コード ファイルにコードを追加して、Web パーツのコンテンツをレンダリングします。

1. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

2. **[新しい項目の追加]** ダイアログ ボックスの **[インストールされたテンプレート]** ペインで、 **[SharePoint]** ノードを展開し、 **[2010]** ノードをクリックします。

3. SharePoint テンプレートの一覧で **[Web パーツ]** テンプレートを選択し、 **[追加]** をクリックします。

     **ソリューション エクスプローラー** に **[Web パーツ]** 項目が表示されます。

## <a name="rendering-content-in-the-web-part"></a>Web パーツのコンテンツのレンダリング

Web パーツに表示するコントロールを指定するには、Web パーツ クラスのコントロール コレクションにコントロールを追加します。

1. **ソリューション エクスプローラー** で、*WebPart1.vb* (Visual Basic の場合) または *WebPart1.cs* (C# の場合) を開きます。

     コード エディターで Web パーツ コード ファイルが開きます。

2. 次のディレクティブを Web パーツ コード ファイルの先頭に追加します。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet1":::

3. 次のコードを `WebPart1` クラスに追加します。 このコードは、次のフィールドを宣言します。

   - Web パーツに従業員を表示するデータ グリッド。

   - データ グリッドのフィルターに使用するコントロール上に表示するテキスト。

   - データ グリッドでデータを表示できない場合、エラーを表示するラベル。

   - 従業員データ ファイルのパスを含む文字列。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet2":::

4. 次のコードを `WebPart1` クラスに追加します。 このコードで、`DataFilePath` というカスタム プロパティが Web パーツに追加されます。 カスタム プロパティとは、ユーザーが SharePoint で設定できるプロパティです。 このプロパティでは、データ グリッドの設定に使用される XML データ ファイルの場所を取得および設定します。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet3":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet3":::

5. `CreateChildControls` メソッドを次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - 前の手順で宣言したデータ グリッドとラベルを追加します。

   - 従業員データを格納する XML ファイルにデータ グリッドをバインドします。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet4":::

6. `WebPart1` クラスに次のメソッドを追加します。 このコードは、以下のタスクを実行します。

   - レンダリングされた Web パーツの Web パーツ動詞メニューに表示する動詞を作成します。

   - 動詞メニューの動詞を選択すると発生するイベントを処理します。 このコードでは、データ グリッドに表示される従業員一覧にフィルターをかけます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/spext_webpart/webpart1/webpart1.cs" id="Snippet5":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/spext_webpart/webpart1/webpart1.vb" id="Snippet5":::

## <a name="test-the-web-part"></a>Web パーツをテストする

プロジェクトを実行すると、SharePoint サイトが開きます。 Web パーツは SharePoint の Web パーツ ギャラリーに自動的に追加されます。 Web パーツは任意の Web パーツ ページに追加できます。

1. 次の XML をメモ帳ファイルに貼り付けます。 この XML ファイルには、Web パーツに表示されるサンプル データが含まれます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
        <employees xmlns="http://schemas.microsoft.com/vsto/samples">
           <employee>
               <name>David Hamilton</name>
               <hireDate>2001-05-11</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Karina Leal</name>
               <hireDate>1999-04-01</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Nancy Davolio</name>
               <hireDate>1992-05-01</hireDate>
               <title>Sales Associate</title>
           </employee>
           <employee>
               <name>Steven Buchanan</name>
               <hireDate>1955-03-04</hireDate>
               <title>Manager</title>
           </employee>
           <employee>
               <name>Suyama Michael</name>
               <hireDate>1963-07-02</hireDate>
               <title>Sales Associate</title>
           </employee>
        </employees>
    ```

2. メモ帳のメニュー バーで、 **[ファイル]**  >  **[上書き保存]** の順に選択します。

3. **[名前を付けて保存]** ダイアログ ボックスで、 **[ファイルの種類]** ボックスの一覧から **[すべてのファイル]** を選択します。

4. **[ファイル名]** ボックスに「**data.xml**」と入力します。

5. **[フォルダーの参照]** ボタンを使用してフォルダーを選択し、 **[保存]** をクリックします。

6. Visual Studio で **F5** キーを押します。

     SharePoint サイトが開きます。

7. **[サイトの操作]** メニューの **[その他のオプション]** をクリックします。

8. **[作成]** ページで、種類として **[Web パーツ ページ]** を選択し、 **[作成]** をクリックします。

9. **[新しい Web パーツ ページ]** ページで、ページに **SampleWebPartPage.aspx** という名前を付け、 **[作成]** をクリックします。

     [Web パーツ] ページが表示されます。

10. [Web パーツ] ページ上のゾーンを選択します。

11. ページの上部にある **[挿入]** タブをクリックし、 **[Web パーツ]** をクリックします。

12. **[カテゴリ]** ペインで、 **[カスタム]** フォルダーを選択し、 **[WebPart1]** Web パーツを選択して **[追加]** をクリックします。

     ページに Web パーツが表示されます。

## <a name="test-the-custom-property"></a>カスタム プロパティをテストする

Web パーツに表示するデータ グリッドを設定するには、各従業員に関するデータが格納された XML ファイルのパスを指定します。

1. Web パーツの右側に表示される矢印をクリックし、表示されるメニューで **[Web パーツの編集]** を選択します。

     Web パーツのプロパティを含むペインがページの右側に表示されます。

2. ペインの **[その他]** ノードを展開し、上記の手順で作成した XML ファイルのパスを入力して **[適用]** をクリックし、 **[OK]** をクリックします。

     Web パーツに従業員一覧が表示されることを確認します。

## <a name="test-the-web-part-verb"></a>Web パーツの動詞をテストする

Web パーツ動詞メニューに表示される項目を選択すると、マネージャーではない従業員の表示と非表示が切り替わります。

1. Web パーツの右側に表示される矢印をクリックし、表示されるメニューで **[マネージャーのみを表示]** を選択します。

     Web パーツにマネージャーである従業員のみが表示されます。

2. 矢印をもう一度クリックし、表示されるメニューで **[すべての従業員を表示]** を選択します。

     Web パーツにすべての従業員が表示されます。

## <a name="see-also"></a>関連項目

[SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
[方法: SharePoint の Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)
[方法: デザイナーを使用して SharePoint の Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
[チュートリアル: デザイナーを使用して SharePoint の Web パーツを作成する](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)
