---
title: 'チュートリアル: サイトのカスタム ワークフロー アクティビティの作成 | Microsoft Docs'
description: このチュートリアルでは、Visual Studio を使用してサイト レベルの SharePoint ワークフローのカスタム アクティビティを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, custom workflow activities
- site workflows [SharePoint development in Visual Studio]
- workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, site workflows
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29a3cd6fe37ec824a3db3a2c83aad7434d0018cb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218049"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>チュートリアル: サイトのカスタム ワークフロー アクティビティの作成
  このチュートリアルでは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用してサイト レベルのワークフローのカスタム アクティビティを作成する方法について説明します。 (サイト レベルのワークフローは、サイトのリストだけでなく、サイト全体に適用されます)。このカスタム アクティビティでは、バックアップのお知らせリストを作成し、お知らせリストの内容をそこにコピーします。

 このチュートリアルでは、次のタスクについて説明します。

- サイト レベルのワークフローの作成。

- カスタム ワークフロー アクティビティの作成。

- SharePoint リストの作成と削除。

- リスト間での項目のコピー。

- クイック起動バーでのリストの表示。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポートされているエディションの [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] と SharePoint。

- 見ることができます。

## <a name="create-a-site-workflow-custom-activity-project"></a>サイト ワークフローのカスタム アクティビティ プロジェクトを作成する
 まず、カスタム ワークフロー アクティビティを保持してテストするプロジェクトを作成します。

#### <a name="to-create-a-site-workflow-custom-activity-project"></a>サイト ワークフローのカスタム アクティビティ プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。

2. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** テンプレートを選択します。

4. **[名前]** ボックスに「**AnnouncementBackup**」と入力し、 **[OK]** ボタンを選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

5. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、 **[ファーム ソリューションとして配置する]** オプション ボタンを選択してから、 **[完了]** ボタンを選択して信頼レベルと既定のサイトをそのまま使用します。

     このステップでは、ソリューションの信頼レベルをファーム ソリューション (ワークフロー プロジェクトで使用できる唯一のオプション) として設定します。

6. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。次に、メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択します。

7. **[Visual C#]** または **[Visual Basic]** で **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

8. **[テンプレート]** ペインで、 **[シーケンシャル ワークフロー (ファーム ソリューションのみ)]** テンプレートを選択し、 **[追加]** ボタンを選択します。

     **SharePoint カスタマイズ ウィザード** が表示されます。

9. **[デバッグのワークフロー名の指定]** ページでは、既定の名前 (AnnouncementBackup - Workflow1) をそのまま使用します。 ワークフロー テンプレートの種類を **[サイト ワークフロー]** に変更し、 **[次へ]** ボタンを選択します。

10. **[完了]** ボタンを選択して、残りの既定の設定をそのまま使用します。

## <a name="add-a-custom-workflow-activity-class"></a>カスタム ワークフロー アクティビティのクラスを追加する
 次に、カスタム ワークフロー アクティビティのコードを保持するクラスをプロジェクトに追加します。

#### <a name="to-add-a-custom-workflow-activity-class"></a>カスタム ワークフロー アクティビティのクラスを追加するには

1. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** を選択して、 **[新しい項目の追加]** ダイアログ ボックスを表示します。

2. **[インストールされたテンプレート]** ツリービューで、 **[コード]** ノードを選択し、プロジェクト項目テンプレートの一覧で **[クラス]** テンプレートを選択します。 既定の名前 Class1 を使用します。 **[追加]** ボタンを選びます。

3. Class1 内のすべてのコードを次のものに置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb" id="Snippet1":::

4. プロジェクトを保存してから、メニュー バーで **[ビルド]**  >  **[ソリューションのビルド]** を選択します。

     **[ツールボックス]** の **[AnnouncementBackup コンポーネント]** タブに Class1 がカスタム アクションとして表示されます。

## <a name="add-the-custom-activity-to-the-site-workflow"></a>サイト ワークフローにカスタム アクティビティを追加する
 次に、カスタム コードを含むアクティビティをワークフローに追加します。

#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>サイト ワークフローにカスタム アクティビティを追加するには

1. ワークフロー デザイナーのデザイン ビューで Workflow1 を開きます。

2. **[ツールボックス]** から Class1 をドラッグして `onWorkflowActivated1` アクティビティの下に表示されるようにします。または、Class1 のショートカット メニューを開き、 **[コピー]** を選択し、`onWorkflowActivated1` アクティビティの下にある行のショートカット メニューを開いて、 **[貼り付け]** を選択します。

3. プロジェクトを保存します。

## <a name="test-the-site-workflow-custom-activity"></a>サイト ワークフローのカスタム アクティビティをテストする
 次に、プロジェクトを実行し、サイト ワークフローを開始します。 このカスタム アクティビティでは、バックアップのお知らせリストを作成し、現在のお知らせリストの内容をそこにコピーします。 また、このコードでは、作成の前に、バックアップリストが既に存在しているかどうかの確認も行います。 バックアップ リストが既に存在する場合は、それを削除します。 また、このコードでは、SharePoint サイトのクイック起動バーに新しいリストへのリンクを追加します。

#### <a name="to-test-the-site-workflow-custom-activity"></a>サイト ワークフローのカスタム アクティビティをテストするには

1. **F5** キーを押し、プロジェクトを実行して SharePoint に配置します。

2. クイック起動バーの **[リスト]** リンクを選択して、SharePoint サイトで使用できるすべてのリストを表示します。 **お知らせ** という名前のお知らせリストが 1 つだけあります。

3. SharePoint Web ページの上部にある **[サイト ワークフロー]** リンクを選択します。

4. [新しいワークフローの開始] セクションで、**AnnouncementBackup - Workflow1** リンクを選択します。 これにより、サイト ワークフローが開始され、カスタム アクションのコードが実行されます。

5. クイック起動バーの **Announcements Backup** リンクを選択します。 **[お知らせ]** リストに含まれているすべてのお知らせが、この新しいリストにコピーされていることに注目してください。

## <a name="see-also"></a>関連項目
- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
