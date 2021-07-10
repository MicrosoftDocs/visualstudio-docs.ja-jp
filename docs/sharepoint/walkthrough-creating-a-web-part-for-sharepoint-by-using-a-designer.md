---
title: デザイナーを使用して SharePoint の Web パーツを作成する
description: このチュートリアルでは、Visual Studio に用意されている SharePoint の視覚的 Web パーツ プロジェクト テンプレートを使用して、Web パーツを視覚的に作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 55f69875b06428c9bbe179e73dd6ea9b4ef40b8e
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112442"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>チュートリアル: デザイナーを使用した SharePoint の Web パーツの作成

SharePoint サイトの Web パーツを作成すれば、ユーザーはブラウザーを使用して、そのサイトを構成するページのコンテンツ、外観、動作を直接変更できます。 このチュートリアルでは、Visual Studio に用意されている SharePoint の **視覚的 Web パーツ** プロジェクト テンプレートを使用して、Web パーツを視覚的に作成する方法を説明します。

ここで作成する Web パーツには、月間カレンダー ビューと、サイトで使用する各カレンダー リストのチェック ボックスが表示されます。 ユーザーがチェック ボックスをオンにすると、それに対応するカレンダー リストが月間カレンダー ビューに追加されます。

このチュートリアルでは、次の作業について説明します。

- **視覚的 Web パーツ** プロジェクト テンプレートを使用して Web パーツを作成する
- Visual Studio の Visual Web Developer デザイナーを使用して Web パーツをデザインする
- Web パーツに配置したコントロールのイベントを処理するコードを追加する
- SharePoint で Web パーツをテストする

    > [!NOTE]
    > このチュートリアルに記載されている Visual Studio ユーザー インターフェイスの一部の要素は、お使いのコンピューターに実際に表示される名前や場所と異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Windows と SharePoint

## <a name="create-a-web-part-project"></a>Web パーツ プロジェクトを作成する

まず、**視覚的 Web パーツ** プロジェクト テンプレートを使用して Web パーツ プロジェクトを作成します。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を、 **[管理者として実行]** オプションを使用して起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。
::: moniker range="=vs-2017"

3. **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** の **[Office/SharePoint]** を展開し、 **[SharePoint ソリューション]** カテゴリを選択します。

4. テンプレートの一覧で **[SharePoint 2013 視覚的 Web パーツ]** テンプレートを選択し、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。 このウィザードでは、プロジェクトのデバッグ時に使用するサイトやソリューションの信頼レベルを指定できます。
::: moniker-end
::: moniker range=">=vs-2019"
3. **[新しいプロジェクトの作成]** ダイアログで、インストールした SharePoint の特定のバージョンに対応する *SharePoint の空のプロジェクト** を選択します。 たとえば、SharePoint 2019 がインストールされている場合は、 **[SharePoint 2019 - 空のプロジェクト]** テンプレートを選択します。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

4. **[名前]** ボックスに「**TestProject1**」と入力した後、 **[作成]** ボタンを選択します。

::: moniker-end
5. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[ファーム ソリューションとして配置する]** オプション ボタンをクリックします。

6. **[完了]** をクリックして、既定のローカル SharePoint サイトを作成します。

## <a name="designing-the-web-part"></a>Web パーツをデザインする

**ツールボックス** にあるコントロールを Visual Web Developer デザイナーのサーフェイスへ追加して、Web パーツをデザインします。

1. Visual Web Developer デザイナーで、 **[デザイン]** タブを選択してデザイン ビューに切り替えます。

2. メニュー バーで **[表示]** 、 **[ツールボックス]** の順にクリックします。

3. **ツールボックス** の **[標準]** ノードで **[CheckBoxList]** コントロールを選択し、次のいずれかの手順に従います。

    - **[CheckBoxList]** コントロールのショートカット メニューを開き、 **[コピー]** を選択します。デザイナーで最初の行のショートカット メニューを開き、 **[貼り付け]** を選択します。

    - **ツールボックス** から **[CheckBoxList]** コントロールをドラッグし、デザイナーの最初の行に接続します。

4. 前の手順を繰り返します。ただし、ここでは、デザイナーの次の行へボタンを移動します。

5. デザイナーで **[Button1]** をクリックします。

6. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

     **[プロパティ]** ウィンドウが開きます。

7. ボタンの "**テキスト**" プロパティに「**更新**」と入力します。

## <a name="handling-the-events-of-controls-on-the-web-part"></a>Web パーツ上のコントロールのイベントを処理する

ユーザーがマスター カレンダー ビューにカレンダーを追加できるようにするコードを追加します。

1. 次のいずれかの操作を実行します。

   - デザイナーで、 **[更新]** ボタンをダブルクリックします。

   - **[更新]** ボタンの **[プロパティ]** ウィンドウで、 **[イベント]** をクリックします。 **Click** プロパティに「**Button1_Click**」と入力し、Enter キーを押します。

     ユーザー コントロール コード ファイルがコード エディターで開き、`Button1_Click` イベント ハンドラーが表示されます。 後で、このイベント ハンドラーにコードを追加します。

2. ユーザー コントロール コード ファイルの先頭に次のステートメントを追加します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet1":::

3. `VisualWebPart1` クラスに次のコード行を追加します。 このコードでは、月間カレンダー ビュー コントロールを宣言します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet2":::

4. `Page_Load` クラスの `VisualWebPart1` メソッドを次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - 月間カレンダー ビューをユーザー コントロールに追加します。

   - サイト上の各カレンダー リストにチェック ボックスを追加します。

   - カレンダー ビューに表示される項目の種類ごとにテンプレートを指定します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet3":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet3":::

5. `Button1_Click` クラスの `VisualWebPart1` メソッドを次のコードに置き換えます。 このコードでは、選択したカレンダーの項目をマスター カレンダー ビューに追加します。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb" id="Snippet4":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs" id="Snippet4":::

## <a name="test-the-web-part"></a>Web パーツをテストする

プロジェクトを実行すると、SharePoint サイトが開きます。 SharePoint の Web パーツ ギャラリーに Web パーツが自動的に追加されます。 このプロジェクトをテストするには、次のタスクを実行します。

- 2 つのカレンダー リストそれぞれにイベントを追加します。
- Web パーツを Web パーツ ページに追加します。
- 月間カレンダー ビューに含めるリストを指定します。

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>サイト上のカレンダー リストにイベントを追加するには

1. Visual Studio で **F5** キーを押します。

     SharePoint サイトが開き、ページ上に [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] クイック起動バーが表示されます。

2. クイック起動バーの **[リスト]** にある **[カレンダー]** リンクを選択します。

     **[カレンダー]** ページが表示されます。

     クイック起動バーにカレンダー リンクが表示されない場合は、 **[サイト コンテンツ]** リンクを選択します。 [サイト コンテンツ] ページに **[カレンダー]** 項目が表示されない場合は、カレンダーを作成します。

3. カレンダー ページで、日を選択し、選択した日の **[追加]** リンクを選択してイベントを追加します。

4. **[タイトル]** ボックスに「**Event in the default calendar**」(既定のカレンダーのイベント) と入力し、 **[保存]** をクリックします。

5. **[サイト コンテンツ]** リンクを選択し、 **[アプリの追加]** タイルを選択します。

6. **[作成]** ページで、種類として **[カレンダー]** を選択し、カレンダーの名前を入力して、 **[作成]** をクリックします。

7. 新しいカレンダーにイベントを追加し、イベントに「**Event in the custom calendar**」(カスタム カレンダーのイベント) という名前を付け、 **[保存]** をクリックします。

### <a name="to-add-the-web-part-to-a-web-part-page"></a>Web パーツを Web パーツ ページに追加するには

1. **[サイト コンテンツ]** ページで **[サイトのページ]** フォルダーを開きます。

2. リボンで **[ファイル]** タブを選択します。 **[新しいドキュメント]** メニューを開き、 **[Web パーツ ページ]** コマンドをクリックします。

3. **[新しい Web パーツ ページ]** で、ページに「**SampleWebPartPage.aspx**」と名前を付け、 **[作成]** をクリックします。

     Web パーツ ページが表示されます。

4. Web パーツ ページの上部にある **[挿入]** タブをクリックし、 **[Web パーツ]** をクリックします。

5. **[カスタム]** フォルダーを選択します。さらに **[VisualWebPart1]** Web パーツを選択し、 **[追加]** をクリックします。

     ページに Web パーツが表示されます。 Web パーツに次のコントロールが表示されます。

    - 月間カレンダー ビュー

    - **[更新]** ボタン

    - **[カレンダー]** チェック ボックス

    - **[カスタム カレンダー]** チェック ボックス

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>月間カレンダー ビューに追加するリストを指定するには

Web パーツで、月間カレンダー ビューに追加するカレンダーを選択し、 **[更新]** をクリックします。

指定したすべてのカレンダーのイベントが月間カレンダー ビューに表示されます。

## <a name="see-also"></a>関連項目

[SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
[方法: SharePoint の Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)
[チュートリアル: SharePoint の Web パーツを作成する](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
