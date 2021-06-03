---
title: 'チュートリアル: 既存の SharePoint サイトからのアイテムのインポート | Microsoft Docs'
titleSuffix: ''
description: このチュートリアルでは、既存の SharePoint サイトから Visual Studio SharePoint プロジェクトに項目をインポートします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 861b6ff20f9ceb73c279e54fa89ee513389b6b91
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900951"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>チュートリアル: 既存の SharePoint サイトからのアイテムのインポート
  このチュートリアルでは、既存の SharePoint サイトから [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトに項目をインポートする方法を実演します。

 このチュートリアルでは、次のタスクについて説明します。

- カスタム サイト列 (*フィールド* とも呼ばれます) を追加して SharePoint サイトをカスタマイズする。

- SharePoint サイトを .wsp ファイルにエクスポートする。

- .wsp インポートプロジェクトを使用して、.wsp ファイルを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint にインポートする。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポートされているエディションの [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] と SharePoint。

- 見ることができます。

## <a name="customize-a-sharepoint-site"></a>SharePoint サイトをカスタマイズする
 この例では、SharePoint サブサイトに新しいサイト列を追加し、後で使用するために別のサブサイトを作成することによって、SharePoint サブサイトを作成およびカスタマイズします。 後で、最初のサブサイトを .wsp ファイルにエクスポートし、その後 .wsp インポート プロジェクトを使用して、2 番目のサブサイトにカスタム サイト列をインポートします。

### <a name="to-create-and-customize-a-sharepoint-site"></a>SharePoint サイトを作成およびカスタマイズする方法

1. http://<em>system name</em>/SitePages/Home.aspx など、Web ブラウザーを使用して SharePoint サイトを開きます。

2. メインの SharePoint サイトからサブサイトを作成するには、 **[サイトの操作]** メニューを開き、 **[新しいサイト]** を選択します。

3. サイトの **[作成]** ダイアログ ボックスで、 **[空のサイト]** タイプを選択します。

4. **[タイトル]** ボックスに「**Site Column Test 1**」と入力します。 **[URL 名]** ボックスに、「**columntest1**」と入力します。その他の設定は既定値のままにしておきます。次に、 **[作成]** ボタンをクリックします。

5. サイトが作成されたら、ブラウザーでメイン サイト http://<em>system name</em>/SitePages/Home.aspx に移動し戻ります。

6. ここでも、メインの SharePoint サイトから空のサブサイトを作成します。そのためには、 **[サイトの操作]** メニューを開き、 **[新しいサイト]** を選択して、 **[空のサイト]** タイプを選択します。

7. **[タイトル]** ボックスに「**Site Column Test 2**」と入力します。 **[URL 名]** ボックスに、「**columntest2**」と入力します。その他の設定は既定値のままにしておきます。次に、 **[作成]** ボタンをクリックします。

8. 最初のサブサイト、 http://<em>SystemName</em>/columntest1/default.aspx に移動し戻ります。

9. **[サイトの操作]** メニューの **[サイトの設定]** をクリックして、[サイトの設定] ページを表示します。

10. **[ギャラリー]** セクションで、 **[サイト列]** リンクを選択します。

11. **[サイト列ギャラリー]** ページの上部にある **[作成]** ボタンをクリックします。

12. **[列名]** ボックスに「**Test Column**」と入力し、その他の既定値はそのままにして、 **[OK]** をクリックします。

13. **[Test Column]** 列は、サイト列ギャラリーの [カスタム列] 見出しの下に表示されます。

## <a name="exporting-the-sharepoint-site"></a>SharePoint サイトのエクスポート
 次に、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトにインポートする SharePoint アイテムと要素を含む SharePoint セットアップ (.wsp) ファイルを取得します。 .wsp ファイルがまだない場合は、既存の SharePoint サイトから作成する必要があります。 この例では、既定の SharePoint サイトを .wsp ファイルにエクスポートします。

> [!IMPORTANT]
> 次の手順を実行する際にランタイムエラーが発生した場合は、SharePoint サイトにアクセスできるシステムでこの手順を実行する必要があります。

### <a name="to-export-an-existing-sharepoint-site"></a>既存の SharePoint サイトをエクスポートする方法

1. SharePoint サイトで、 **[サイトの操作]** タブの **[サイトの設定]** を選択し、[サイトの設定] ページを表示します。

2. [サイトの設定] ページの **[サイトの操作]** セクションで、 **[サイトをテンプレートとして保存]** リンクを選択します。

3. **[ファイル名]** ボックスに「**ExampleSite**」と入力し、 **[テンプレート名]** ボックスに「**Example Site**」と入力します。

4. この例では、 **[コンテンツを含める]** チェック ボックスをオフのままにします。

     このボックスを選択すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によりすべてのリストとドキュメント ライブラリおよびその内容が .wsp ファイルに保存されます。 これは、状況によっては役に立ちますが、この例では必要ではありません。

5. 操作が正常に完了したら、 **[ソリューション ギャラリー]** リンクをクリックして、.wsp ファイルを表示します。

     後で [ソリューション ギャラリー] ページを表示するには、 **[サイトの操作]** メニューを開き、 **[サイトの設定]** を選択します。次に、 **[サイト コレクションの管理]** セクションの **[最上位レベルのサイト設定にアクセス]** リンクを選択し、 **[ギャラリー]** セクションの **[ソリューション]** リンクを選択します。

6. ソリューション ギャラリーで、**ExampleSite** のリンクを選択します。

7. **[ファイルのダウンロード]** ダイアログ ボックスで、 **[保存]** をクリックして、ローカル システムにファイルを保存します。既定はダウンロード フォルダーです。

## <a name="import-the-wsp-file"></a>.wsp ファイルをインポートする
 再利用する項目 (カスタム サイト列の Test Column) を含む *.wsp* ファイルがあるので、それにアクセスするために *.wsp* ファイルをインポートします。

### <a name="to-import-a-wsp-file"></a>.wsp ファイルをインポートする方法

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のメニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、メニュー バーで **[ファイル]**  >  **[新しいプロジェクト]** の順に選択します。

2. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. **[テンプレート]** ペインで **[SharePoint 2010 ソリューション パッケージのインポート]** テンプレートを選択し、プロジェクトの名前を WspImportProject1 のままにして、 **[OK]** をクリックします。

    **SharePoint カスタマイズ ウィザード** が表示されます。

4. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、前に作成した 2 番目の SharePoint サブサイトの [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] を入力します。 新しいカスタム フィールド項目である http://<em>system name</em>/columntest2 をそのサブサイトに追加します。

5. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[サンドボックス ソリューションとして配置する]** を選択したままにします。

6. **[新しいプロジェクト ソースの指定]** ページで、前に *.wsp* ファイルを保存したシステム上の場所を参照し、 **[次へ]** を選択します。

   > [!NOTE]
   > このページの **[完了]** ボタンを選択すると、 *.wsp* ファイル内の使用可能なすべての項目がインポートされます。

7. **[インポートする項目の選択]** ボックスで、**Test Column** 以外の一覧のすべてのチェック ボックスをオフにし、 **[完了]** を選択します。

    一覧には多くの項目が含まれているので、 **Ctrl**+**A** キーを押して一覧内のすべての項目を選択し、Space キーを押してすべてのチェック ボックスをオフにして、**Test Column** 項目の横のチェック ボックスのみをオンにします。

    インポート操作が完了すると、**WspImportProject1** という名前の新しいプロジェクトが作成されます。これには、**Fields** という名前のフォルダーが含まれています。 このフォルダーには、カスタムサイト列の **Test Column** とその定義ファイル *Elements.xml* があります。

## <a name="deploy-the-project"></a>プロジェクトをデプロイする
 最後に、カスタム サイト列を表示するために、前に作成した 2 つ目の SharePoint サブサイトに **WspImportProject1** を配置します。

### <a name="to-deploy-the-project"></a>プロジェクトを展開するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、**F5** キーを 押して、 *.wsp* インポート プロジェクトを配置して実行します。

2. SharePoint サイトで、 **[サイトの操作]** メニューを開き、次に **[サイトの設定]** を選択肢して [サイトの設定] ページを表示します。

3. **[ギャラリー]** セクションで、 **[サイト列]** リンクを選択します。

4. **[カスタム列]** セクションまで下へスクロールします。

     最初の SharePoint サイトからインポートしたカスタム サイト列が一覧に表示されることに注意してください。

## <a name="see-also"></a>関連項目
- [既存の SharePoint サイトからの項目のインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
