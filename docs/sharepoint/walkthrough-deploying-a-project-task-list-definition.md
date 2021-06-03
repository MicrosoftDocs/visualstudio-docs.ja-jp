---
title: 'チュートリアル: プロジェクト タスク一覧定義の配置 | Microsoft Docs'
description: このチュートリアルでは、Visual Studio を使用して、プロジェクト タスクを追跡する SharePoint リストを作成、カスタマイズ、デバッグ、配置します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b0692b676ec701b40edd12d1634ab9cdf419f85f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217724"
---
# <a name="walkthrough-deploy-a-project-task-list-definition"></a>チュートリアル: プロジェクト タスク リスト定義を配置する

このチュートリアルでは、[!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] を使用して、プロジェクト タスクを追跡する SharePoint リストを作成、カスタマイズ、デバッグ、配置する方法を説明します。

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント

- サポート対象エディションの Microsoft Windows および SharePoint。

- Visual Studio 2017 または Azure DevOps Services。

## <a name="create-a-sharepoint-list"></a>SharePoint リストを作成する

SharePoint リスト プロジェクトを作成し、リスト定義をタスクに関連付けます。

1. **[新しいプロジェクト]** ダイアログ ボックスを開き、 **[SharePoint]** ノードを展開して、 **[2010]** ノードをクリックします。

2. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** テンプレートを選択し、プロジェクトに **ProjectTaskList** という名前を付け、 **[OK]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。

3. デバッグに使用するローカル SharePoint サイトを指定し、 **[ファーム ソリューションとして配置する]** オプション ボタンをクリックして、 **[完了]** をクリックします。

4. プロジェクトのショートカット メニューを開き、 **[追加]**  >  **[新しい項目]** の順に選択します。

5. **[テンプレート]** ペインで、 **[リスト]** テンプレートを選択し、 **[追加]** をクリックします。

     **SharePoint カスタマイズ ウィザード** が表示されます。

6. **[リストの表示名]** ボックスに、「**Project Task List**」(プロジェクト タスク一覧) と入力します。

7. **[既存のリストの種類に基づくカスタマイズできないリストを作成]** オプション ボタンをクリックし、一覧で **[タスク]** を選択し、 **[完了]** をクリックします。

     一覧、フィーチャー、パッケージが、**ソリューション エクスプローラー** に表示されます。

## <a name="add-an-event-receiver"></a>イベント レシーバーを追加する

タスク一覧で、タスクの期限と説明を自動的に設定するイベント レシーバーを追加できます。 次の手順では、イベント レシーバーとしてリスト インスタンスに単純なイベント ハンドラーを追加します。

1. プロジェクト ノードのショートカット メニューを開き、 **[追加]** を選択し、 **[新しい項目]** をクリックします。

2. SharePoint テンプレートの一覧で、 **[イベント レシーバー]** テンプレートを選択し、**ProjectTaskListEventReceiver** という名前を付けます。

     **SharePoint カスタマイズ ウィザード** が表示されます。

3. **[イベント レシーバー設定の選択]** ページの **[使用するイベント レシーバーの種類]** ボックスの一覧で、イベント レシーバーの種類として **[リスト項目イベント]** を選択します。

4. **[イベント ソースとなる項目]** ボックスの一覧で、 **[タスク]** を選択します。

5. 処理するイベントの一覧で、 **[項目が追加されました]** の横にあるチェック ボックスをオンにして、 **[完了]** をクリックします。

     新しいイベント レシーバー ノードが、**ProjectTaskListEventReceiver** という名前のコード ファイルと共にプロジェクトに追加されます。

6. **ProjectTaskListEventReceiver** コード ファイル内の `ItemAdded` メソッドにコードを追加します。 新しいタスクが追加されるたびに、既定の期限と説明がタスクに追加されます。 既定の期限は 2009 年 7 月 1 日です。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb" id="Snippet1":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs" id="Snippet1":::

## <a name="customize-the-project-task-list-feature"></a>プロジェクト タスク リスト フィーチャーをカスタマイズする

SharePoint ソリューションを作成すると、Visual Studio によって、既定のプロジェクト項目のフィーチャーが自動的に作成されます。 フィーチャー デザイナーを使用して、SharePoint サイトのプロジェクト タスク リスト設定をカスタマイズできます。

1. **ソリューション エクスプローラー** で、 **[フィーチャー]** を展開します。

2. **Feature1** のショートカット メニューを開き、 **[ビュー デザイナー]** を選択します。

3. **[タイトル]** ボックスに「**Project Task List Feature**」(プロジェクト タスク一覧フィーチャー) と入力します。

4. **[スコープ]** ボックスの一覧で、 **[Web]** を選択します。

5. **[プロパティ]** ウィンドウで、**Version** プロパティの値として「**1.0.0.0**」を入力します。

## <a name="customize-the-project-task-list-package"></a>プロジェクト タスク リスト パッケージをカスタマイズする

SharePoint プロジェクトを作成すると、Visual Studio により、既定のプロジェクト項目を含むフィーチャーがパッケージに自動的に追加されます。 パッケージ デザイナーを使用して、SharePoint サイトのプロジェクト タスク リスト設定をカスタマイズできます。

1. **ソリューション エクスプローラー** で、 **[パッケージ]** のショートカット メニューを開き、 **[ビュー デザイナー]** を選択します。

2. **[名前]** ボックスに、「**ProjectTaskListPackage**」と入力します。

3. **[Web サーバーのリセット]** チェック ボックスをオンにします。

## <a name="build-and-test-the-project-task-list"></a>プロジェクト タスク リストをビルドしテストする

プロジェクトを実行すると、SharePoint サイトが開きます。 ただし、タスクの一覧の場所には手動で移動する必要があります。

1. **F5** キーを押して、プロジェクト タスクの一覧をビルドおよび配置します。

     SharePoint サイトが開きます。

2. **[ホーム]** タブを選択します。

3. 左側のサイドバーで、 **[プロジェクト タスク一覧]** リンクを選択します。

     [プロジェクト タスク一覧] ページが表示されます。

4. **[リスト ツール]** タブで、 **[項目]** タブを選択します。

5. **[項目]** グループで、 **[新しい項目]** をクリックします。

6. **[タイトル]** テキスト ボックスに「**Task1**」と入力します。

7. **[保存]** をクリックします。

     サイトが更新されると、**Task1** タスクが 2009 年 7 月 1 日の期限で表示されます。

8. **[Task1]** を選択します。

     タスクの詳細ビューが表示され、"This is a critical task"(これはクリティカル タスクです) という説明が表示されます。

## <a name="deploy-the-project-task-list"></a>プロジェクト タスク リストを配置する

プロジェクト タスク リストをビルドおよびテストした後、"*ローカル システム*" または "*リモート システム*" にそれを配置できます。 ローカル システムは、ソリューションを開発したコンピューターと同じですが、リモート システムは別のコンピューターです。

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>ローカル システムにプロジェクト タスク リストを配置するには

Visual Studio メニュー バーで、 **[ビルド]**  >  **[ソリューションの配置]** の順に選択します。

Visual Studio では IIS アプリケーション プールをリサイクルし、ソリューションの既存のバージョンを取り消し、ソリューション パッケージ ( *.wsp*) ファイルを SharePoint にコピーして、そのフィーチャーをアクティブ化します。 これで、SharePoint でソリューションを使用できるようになります。 配置構成手順に関する詳細については、「[方法: SharePoint の配置構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」を参照してください。

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>リモート システムにプロジェクト タスク リストを配置するには

1. Visual Studio のメニュー バーで、 **[ビルド]**  >  **[発行]** の順に選択します。

2. **[発行]** ダイアログ ボックスで、 **[ファイル システムに発行する]** オプション ボタンをクリックします。

     **[発行]** ダイアログ ボックスで目的の場所を変更するには、省略記号ボタン (![省略記号アイコン](../sharepoint/media/ellipsisicon.gif "省略記号アイコン")) をクリックし、別の場所に移動します。

3. **[発行]** をクリックします。

     ソリューションの *.wsp* ファイルが作成されます。

4. *.wsp* ファイルをリモートの SharePoint システムにコピーします。

5. PowerShell `Add-SPUserSolution` コマンドを使用して、リモートの SharePoint インストールにパッケージをインストールします。 (ファーム ソリューションの場合は、`Add-SPSolution` コマンドを使用します)。

     たとえば、「 `Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp` 」のように入力します。

6. PowerShell `Install-SPUserSolution` コマンドを使用して、ソリューションを配置します。 (ファーム ソリューションの場合は、`Install-SPSolution` コマンドを使用します)。

     たとえば、「 `Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName` 」のように入力します。

     リモート配置の詳細については、「[ソリューションの使用](/previous-versions/office/developer/sharepoint-2010/ee534972(v=office.14))」と [SharePoint 2010 の PowerShell を使用したソリューションの追加と配置](http://www.dotnetmafia.com/blogs/dotnettipoftheday/archive/2009/12/02/adding-and-deploying-solutions-with-powershell-in-sharepoint-2010.aspx)に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

SharePoint ソリューションをカスタマイズおよび配置する方法の詳細については、次のトピックを参照してください。

- [チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)

- [SharePoint Server 2010 用 Windows PowerShell](/powershell/module/sharepoint-server)

## <a name="see-also"></a>関連項目
[SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
