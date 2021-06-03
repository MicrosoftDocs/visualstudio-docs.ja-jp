---
title: 'チュートリアル: SharePoint アプリケーションのプロファイリング | Microsoft Docs'
description: このチュートリアルでは、Visual Studio のプロファイル ツールを使用して、SharePoint アプリケーションのパフォーマンスを最適化します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 796c41ae50a33f00f72e0286d5e9680f9016cf58
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952565"
---
# <a name="walkthrough-profile-a-sharepoint-application"></a>チュートリアル: SharePoint アプリケーションのプロファイリング
  このチュートリアルでは、Visual Studio のプロファイル ツールを使用し、SharePoint アプリケーションのパフォーマンスを最適化する方法について説明します。 アプリケーション例は SharePoint フィーチャー イベント レシーバーで、これにはフィーチャー イベント レシーバーのパフォーマンスを低下させるアイドル ループが含まれています。 Visual Studio プロファイラーを使用すると、"*ホット パス*" とも呼ばれるプロジェクトの最も負荷のかかる (実行速度が最も遅い) 部分を特定し、取り除くことができます。

 このチュートリアルでは、次のタスクについて説明します。

- [機能とフィーチャー イベント レシーバーを追加します](#add-a-feature-and-feature-event-receiver)。

- [SharePoint アプリケーションを構成し、配置します](#configure-and-deploy-the-sharepoint-application)。

- [SharePoint アプリケーションを実行します](#run-the-sharepoint-application)。

- [プロファイル結果を表示し、解釈します](#view-and-interpret-the-profile-results)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-sharepoint-project"></a>SharePoint プロジェクトを作成する
 まずは、SharePoint プロジェクトを作成します。

### <a name="to-create-a-sharepoint-project"></a>SharePoint プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択して、 **[新しいプロジェクト]** ダイアログ ボックスを表示します。

2. **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. [テンプレート] ウィンドウで、 **[SharePoint 2010 プロジェクト]** テンプレートを選択します。

4. **[名前]** ボックスに「**ProfileTest**」と入力し、 **[OK]** ボタンを選択します。

    **SharePoint カスタマイズ ウィザード** が表示されます。

5. **[デバッグのサイトとセキュリティ レベルの指定]** ページで、サイト定義をデバッグする SharePoint サーバー サイトの URL を入力するか、既定の場所 (http://<<em>システム名</em>>/) を使用します。

6. **[この SharePoint ソリューションの信頼レベル]** セクションで、 **[ファーム ソリューションとして配置する]** オプション ボタンを選択します。

    現時点では、ファーム ソリューションのプロファイルのみを実行できます。 サンドボックス ソリューションとファーム ソリューションの比較の詳細については、「[サンド ボックス ソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[完了]** をクリックします。 **ソリューション エクスプローラー** にプロジェクトが表示されます。

## <a name="add-a-feature-and-feature-event-receiver"></a>フィーチャーとフィーチャー イベント レシーバーを追加する
 次に、フィーチャーを、そのイベント レシーバーと共にプロジェクトに追加します。 このイベント レシーバーには、プロファイル対象のコードが含まれます。

### <a name="to-add-a-feature-and-feature-event-receiver"></a>機能とフィーチャー イベント レシーバーを追加するには

1. **ソリューション エクスプローラー** で **[フィーチャー]** ノードのショートカット メニューを開き、 **[フィーチャーの追加]** を選択します。名前は既定値の **[Feature1]** のままにします。

2. **ソリューション エクスプローラー** で **[Feature1]** のショートカット メニューを開き、 **[イベント レシーバーの追加]** を選択します。

     これにより、いくつかのコメント アウトされたイベント ハンドラーを持つコード ファイルが機能に追加され、編集のためにファイルが開かれます。

3. イベント レシーバー クラスに、次の変数宣言を追加します。

    ```vb
    ' SharePoint site/subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site/subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

4. `FeatureActivated` プロシージャを次のコードに置き換えます。

    ```vb
    Public Overrides Sub FeatureActivated(properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add a new announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    ' Waste some time.
                    TimeCounter()
                    ' Update the list.
                    listItem.Update()
                End Using
            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try
    End Sub
    ```

    ```csharp
    public override void FeatureActivated(SPFeatureReceiverProperties properties)
    {
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList announcementsList = web.Lists["Announcements"];

                    // Add a new announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " +
    DateTime.Now.ToString();
                    // Waste some time.
                    TimeCounter();
                    // Update the list.
                    listItem.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

5. 次のプロシージャを `FeatureActivated` プロシージャの下に追加します。

    ```vb

    Public Sub TimeCounter()
        Dim result As Integer
        For i As Integer = 0 To 99999
            For j As Integer = 0 To 9999
                result = i * j
            Next j
        Next i
    End Sub
    ```

    ```csharp
    public void TimeCounter()
    {
        for (int i = 0; i < 100000; i++)
        {
            for (int j = 0; j < 10000; j++)
            {
                int result = i * j;
            }
        }
    }
    ```

6. **ソリューション エクスプローラー** で、プロジェクト (**ProfileTest**) のショートカット メニューを開き、 **[プロパティ]** を選択します。

7. **[プロパティ]** ダイアログ ボックスで、 **[SharePoint]** タブを選択します。

8. **[アクティブな配置構成]** ボックスの一覧の **[アクティブ化なし]** を選択します。

     この配置構成を選択することにより、後で SharePoint 内から手動で機能をアクティブ化できます。

9. プロジェクトを保存します。

## <a name="configure-and-deploy-the-sharepoint-application"></a>SharePoint アプリケーションを構成し、配置する
 SharePoint プロジェクトの準備ができたので、それを構成し、SharePoint サーバーに配置します。

### <a name="to-configure-and-deploy-the-sharepoint-application"></a>SharePoint アプリケーションを構成し、配置するには

1. **[分析]** メニューの **[パフォーマンス ウィザードの起動]** を選択します。

2. **パフォーマンス ウィザード** の最初のページで、プロファイル方法を **[CPU サンプリング]** のままにし、 **[次へ]** を選択します。

     他のプロファイル方法は、より高度なプロファイルを行う場合に使用できます。 詳細については、「[パフォーマンス収集方法について](../profiling/understanding-performance-collection-methods.md)」を参照してください。

3. **パフォーマンス ウィザード** の 2 ページ目で、プロファイルのターゲットを **[ProfileTest]** のままにし、 **[次へ]** を選択します。

     ソリューションに複数のプロジェクトがある場合は、この一覧に表示されます。

4. **パフォーマンス ウィザード** の 3 ページ目で、 **[階層の相互作用のプロファイルを有効にする]** チェック ボックスをオフにし、 **[次へ]** を選択します。

     階層の相互作用のプロファイル (TIP) 機能は、データベースを照会するアプリケーションのパフォーマンスの測定や、Web ページが要求された回数の表示に便利です。 そのようなデータはこの例では不要なため、この機能は有効にしません。

5. **パフォーマンス ウィザード** の 4 ページ目で、 **[ウィザードの完了後にプロファイルを起動する]** チェック ボックスをオンのままにし、 **[完了]** を選択します。

     ウィザードによって、サーバーでのアプリケーションのプロファイルが有効になり、 **[パフォーマンス エクスプローラー]** ウィンドウが表示され、SharePoint アプリケーションのビルド、配置、および実行が行われます。

## <a name="run-the-sharepoint-application"></a>SharePoint アプリケーションを実行する
 `FeatureActivation` イベント コードの実行をトリガーし、SharePoint 内のフューチャーをアクティブ化します。

### <a name="to-run-the-sharepoint-application"></a>SharePoint アプリケーションを実行するには

1. SharePoint で、 **[サイトの操作]** メニューを開き、 **[サイトの設定]** を選択します。

2. **[サイトの操作]** ボックスの一覧の **[サイト機能の管理]** リンクを選択します。

3. **[機能]** の一覧で、**ProfileTest Feature1** の横にある **[アクティブ化]** を選択します。

     この操作を実行すると、`FeatureActivated` 関数内でアイドル ループが呼び出されることによって一時停止が発生します。

4. **[クイック起動]** バーの **[リスト]** を選択し、 **[リスト]** ボックスの一覧の **[お知らせ]** を選択します。

     機能がアクティブになったことを示す新しいお知らせが一覧に追加されていることを確認します。

5. SharePoint サイトを閉じます。

     SharePoint を閉じると、プロファイラーによってサンプル プロファイル レポートが作成されて表示され、.vsp ファイルとして **ProfileTest** プロジェクトのフォルダーに保存されます。

## <a name="view-and-interpret-the-profile-results"></a>プロファイル結果を表示し、解釈する
 SharePoint アプリケーションを実行してプロファイルを行ったので、次はテスト結果を表示します。

### <a name="to-view-and-interpret-the-profile-results"></a>プロファイル結果を表示し、解釈するには

1. サンプル プロファイル レポートの **[最も頻繁に個別の作業を実行している関数]** セクションでは、`TimeCounter` が一覧の最上部近くにあります。

     この場所は、`TimeCounter` がサンプル数の最も多い関数の 1 つ、つまり、アプリケーション内で最大のパフォーマンス ボトルネックの 1 つであることを示しています。 ただし、これは驚くような状況はではありません。デモンストレーションのために、意図してこのようにデザインされたものであるからです。

2. **[最も頻繁に個別の作業を実行している関数]** セクションで `ProcessRequest` リンクをクリックし、`ProcessRequest` 関数のコスト配分を表示します。

     `ProcessRequest` の **[呼び出される関数]** セクションに、**FeatureActiviated** 関数が最も負荷の高い、呼び出される関数として表示されます。

3. **[呼び出される関数]** セクションで、 **[FeatureActivated]** を選択します。

     **FeatureActivated** の **[呼び出される関数]** セクションに、`TimeCounter` 関数が最も負荷の高い、呼び出される関数として表示されます。 **[関数コード ビュー]** ウィンドウの強調表示されたコード (`TimeCounter`) はホットスポットであり、修正が必要な場所を示しています。

4. サンプル プロファイル レポートを閉じます。

     レポートは、 **[パフォーマンス エクスプローラー]** ウィンドウの .vsp ファイルを開くと、いつでも再確認できます。

## <a name="fix-the-code-and-reprofile-the-application"></a>コードを修正し、アプリケーションを再プロファイルする
 SharePoint アプリケーション内のホットスポット関数を特定したので、次はこれを修正します。

### <a name="to-fix-the-code-and-reprofile-the-application"></a>コードを修正し、アプリケーションを再プロファイルするには

1. フィーチャー イベント レシーバーのコード内で、`FeatureActivated` の `TimeCounter` メソッドの呼び出しをコメント アウトし、これが呼び出されないようにします。

2. プロジェクトを保存します。

3. **パフォーマンス エクスプローラー** で [ターゲット] フォルダーを開き、 **[ProfileTest]** ノードをクリックします。

4. **[アクション]** タブの **[パフォーマンス エクスプローラー]** ツール バーで、 **[プロファイルの開始]** をクリックします。

     アプリケーションの再プロファイル前にいずれかのプロファイル プロパティを変更する場合は、代わりに **[パフォーマンス ウィザードの起動]** をクリックします。

5. このトピックで前述した「**SharePoint アプリケーションを実行する**」セクションの手順に従います。

     これで、アイドル ループへの呼び出しが削除されたため、機能のアクティブ化がより高速になりました。 このことは、サンプル プロファイル レポートに反映されます。

## <a name="see-also"></a>関連項目
- [パフォーマンス セッションの概要](../profiling/performance-session-overview.md)
- [パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-performance-profiling.md)
- [Visual Studio プロファイラーでアプリケーションのボトルネックを見つける](/archive/msdn-magazine/2008/march/find-application-bottlenecks-with-visual-studio-profiler)