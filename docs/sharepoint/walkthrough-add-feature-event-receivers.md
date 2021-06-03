---
title: 'チュートリアル: フィーチャー イベント レシーバーを追加する | Microsoft Docs'
description: このチュートリアルでは、フィーチャー イベント レシーバーを追加します。フィーチャー イベント レシーバーとは、SharePoint フィーチャーがインストールされたとき、アクティブ化されたとき、非アクティブ化されたとき、削除されたときなどに実行されるメソッドです。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, advanced packaging tools
- SharePoint development in Visual Studio, event receivers
- SharePoint development in Visual Studio, feature event receivers
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 305220a8206cc84e55ed7319b5ce6ce1c8058b3c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217035"
---
# <a name="walkthrough-add-feature-event-receivers"></a>チュートリアル: フィーチャー イベント レシーバーを追加する
フィーチャー イベント レシーバーは、SharePoint で次のフィーチャー関連のイベントのいずれかが発生したときに実行されるメソッドです。

- フィーチャーがインストールされた。

- フィーチャーがアクティブ化された。

- フィーチャーが非アクティブ化された。

- フィーチャーが削除された。

このチュートリアルでは、SharePoint プロジェクトのフィーチャーにイベント レシーバーを追加する方法について説明します。 次のタスクについて説明します。

- フィーチャー イベント レシーバーを使用して空のプロジェクトを作成する。

- **FeatureDeactivating** メソッドを操作する。

- SharePoint プロジェクト オブジェクト モデルを使用して、お知らせリストにアナウンスを追加する。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- 見ることができます。

## <a name="create-a-feature-event-receiver-project"></a>フィーチャー イベント レシーバー プロジェクトを作成する
 まず、フィーチャー イベント レシーバーを含むプロジェクトを作成します。

#### <a name="to-create-a-project-with-a-feature-event-receiver"></a>フィーチャー イベント レシーバーを含むプロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。

2. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. **[テンプレート]** ペインで、 **[SharePoint 2010 プロジェクト]** テンプレートを選択します。

     フィーチャー イベント レシーバーには、プロジェクト テンプレートがないため、このプロジェクトの種類を使用します。

4. **[名前]** ボックスに「**FeatureEvtTest**」と入力し、 **[OK]** をクリックして **SharePoint カスタマイズ ウィザード** を表示します。

5. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、新しいカスタム フィールド項目を追加する SharePoint サーバー サイトの URL を入力するか、既定の場所 (http://\<*system name*>/) を使用します。

6. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[ファーム ソリューションとして配置する]** オプション ボタンをクリックします。

     サンドボックス ソリューションとファーム ソリューションの比較の詳細については、「[サンド ボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[完了]** をクリックし、Feature1 という名前のフィーチャーが **[フィーチャー]** ノードの下に表示されることを確認します。

## <a name="add-an-event-receiver-to-the-feature"></a>イベント レシーバーをフィーチャーに追加する
 次に、フィーチャーにイベント レシーバーを追加し、フィーチャーが非アクティブになったときに実行されるコードを追加します。

#### <a name="to-add-an-event-receiver-to-the-feature"></a>イベント レシーバーをフィーチャーに追加するには

1. [フィーチャー] ノードのショートカット メニューを開き、 **[フィーチャーの追加]** を選択してフィーチャーを作成します。

2. **[フィーチャー]** ノードで **Feature1** のショートカット メニューを開き、 **[イベント レシーバーの追加]** を選択して、このフィーチャーにイベント レシーバーを追加します。

     これにより、Feature1 の下にコード ファイルが追加されます。 この場合、プロジェクトの開発言語に応じて、*Feature1.EventReceiver.cs* または *Feature1.EventReceiver.vb* のいずれかの名前が付けられます。

3. プロジェクトが [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] に記述されている場合は、イベント レシーバーの先頭に次のコードを追加します (まだ存在していない場合)。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs" id="Snippet1":::

4. イベント レシーバー クラスには、イベントとして機能するいくつかのコメントアウトされたメソッドが含まれています。 **FeatureDeactivating** メソッドを以下に置き換えます。

     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/featureevt2vb/features/feature1/feature1.eventreceiver.vb" id="Snippet2":::
     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs" id="Snippet2":::

## <a name="test-the-feature-event-receiver"></a>フィーチャー イベント レシーバーをテストする
 次に、フィーチャーを非アクティブ化して、**FeatureDeactivating** メソッドにより SharePoint お知らせリストにアナウンスが出力されるかどうかをテストします。

#### <a name="to-test-the-feature-event-receiver"></a>フィーチャー イベント レシーバーをテストするには

1. プロジェクトの "**アクティブな配置構成**" プロパティの値を **[アクティブ化なし]** に設定します。

     このプロパティを設定すると、SharePoint でフィーチャーをアクティブ化できなくなり、フィーチャー イベント レシーバーをデバッグできるようになります。 詳細については、[SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)に関するページを参照してください。

2. **F5** キーを押し、プロジェクトを実行して SharePoint に配置します。

3. SharePoint Web ページの上部にある **[サイトの操作]** メニューを開き、 **[サイトの設定]** を選択します。

4. **[サイトの設定]** ページの **[サイトの操作]** セクションで、 **[サイト機能の管理]** リンクを選択します。

5. **[フィーチャー]** ページで、**FeatureEvtTest Feature1** フィーチャーの横にある **[アクティブ化]** をクリックします。

6. **[フィーチャー]** ページで、**FeatureEvtTest Feature1** フィーチャーの横にある **[非アクティブ化]** をクリックし、 **[この機能を非アクティブ化]** 確認リンクを選択してフィーチャーを非アクティブ化します。

7. **[ホーム]** をクリックします。

     フィーチャーが非アクティブ化されると、**お知らせ** リストにアナウンスが表示されます。

## <a name="see-also"></a>関連項目

- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)