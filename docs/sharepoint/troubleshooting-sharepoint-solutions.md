---
title: SharePoint ソリューションのトラブルシューティング | Microsoft Docs
description: Visual Studio デバッガーを使用して SharePoint ソリューションをデバッグするときに発生する可能性がある問題または警告について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Tools.SharePoint.Errors.Debugging
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, troubleshooting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c6b0e031e96d2543ae0bb109f243824125f431a3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892295"
---
# <a name="troubleshoot-sharepoint-solutions"></a>SharePoint ソリューションのトラブルシューティング
  以下の問題または警告は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを使用して SharePoint ソリューションをデバッグするときに発生することがあります。 詳細については、[SharePoint 2007 ワークフロー ソリューションのデバッグ](/previous-versions/bb386166(v=vs.100))に関する記事を参照してください。

## <a name="token-restrictions-in-sandboxed-visual-web-parts"></a>サンドボックス視覚的 Web パーツでのトークンの制約
 サンドボックス ソリューションの視覚的 Web パーツは、SharePoint ランタイムでサポートされる $SPUrl などの標準トークンを処理できません。 そのため、URL は解決されず、次の例のように、スクリプト要素でこのトークンを直接参照する場合、視覚的 Web パーツ デザイナーのデザイン ビューでコンテンツをプレビューできません。

```xml
<script src="<% $SPUrl:~site/SiteAssets/ListOperations.js %>"></script>
```

 この制限を回避し、トークンを解決するには、次のようにリテラルを使用してトークンを参照します。

```xml
<asp:literal ID="Literal1" runat="server" Text="<script src='" />
<asp:literal ID="Literal2" runat="server" Text="<% $SPUrl:~site/SiteAssets/ListOperations.js %>" />
<asp:literal ID="Literal3" runat="server" Text="' type='text/javascript' ></script>" />
```

## <a name="character-restrictions-in-names-of-projects-and-project-items"></a>プロジェクトとプロジェクト アイテムの名前の文字制限
 プロジェクトとプロジェクト アイテムの名前には、SharePoint 2010 の配置パスで有効な文字だけを使用できます。 他の文字は使用できません。

### <a name="error-message"></a>エラー メッセージ
 "無効な文字" エラー メッセージ。

### <a name="resolution"></a>解決方法
 SharePoint のプロジェクトとプロジェクト アイテムの名前では、次の文字だけを使用してください。

- ASCII 英数字

- Space

- ピリオド (.)

- コンマ (,)

- アンダースコア (_)

- ダッシュ (-)

- 円記号 (\\)

  プロジェクトがパッケージされるとき、検証規則により、配置される各ファイルの配置パス プロパティに有効な文字だけが含まれていることが確認されます。

## <a name="errors-when-creating-custom-fields"></a>カスタム フィールド作成時のエラー
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、カスタム フィールドは、XML で定義されます。 フィールドが特定の形式で定義または参照されていない場合、エラーが発生する可能性があります。

### <a name="error-message"></a>エラー メッセージ
 パッケージ実行時の "無効な文字" エラー メッセージ。

### <a name="resolution"></a>解決方法
 フィールド定義の ID には、次の例のように、中かっこで囲まれた GUID を指定する必要があります。

```xml
<Field ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Type="Note"
    Name="PatientName"
    DisplayName="Patient Name"
    Group="A Custom Group">
</Field>.
```

 次の例に示すように、コンテンツ タイプ内のフィールド参照は、開始と終了要素 (\<FieldRef>\</FieldRef>) ではなく、空の要素の形式 (\<FieldRef />) で定義する必要があります。

```xml
<FieldRef ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Name="PatientName"
    DisplayName="Patient Name"
    Required="TRUE"/>
```

 フィールドのソース XML の形式が間違っている場合、有効な XML ファイルでない場合、またはその他の問題がある場合、"ファイルを解析できません" エラーが発生します。

## <a name="new-non-english-site-definitions-do-not-appear-in-site-creation-page-after-deployment"></a>英語以外の新しいサイト定義が配置後にサイトの作成ページに表示されない
 英語以外のバージョン (ロケール [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] が 1033 以外のバージョン) の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用してサイト定義を作成して配置した後に、 **[テンプレートの選択]** ボックスに **[SharePoint のカスタマイズ]** タブが表示されず、 **[新しい SharePoint サイト]** ページに新しいサイト テンプレートが表示されません。

### <a name="error-message"></a>エラー メッセージ
 [なし] :

### <a name="resolution"></a>解決方法
 この問題は、webtemp サイト定義構成ファイル (*webtemp_SiteDefinitionProject1.xml* など) の **[パス]** プロパティの値が正しくないために発生します。 webtemp ファイルの **[パス]** プロパティ ( **[配置場所]** の下にあります) で、1033 を適切なロケール [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] に変更します。 たとえば、日本語のロケールを使用する場合は値を 1041 に変更します。 詳細については、「 [Microsoft によって割り当てられているロケール ID](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)」を参照してください。

## <a name="error-appears-when-a-workflow-project-is-deployed-on-a-clean-system"></a>ワークフロー プロジェクトをクリーン システムに配置するとエラーが表示される
 この問題は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] のワークフロー プロジェクトをクリーン システムに配置した場合に発生します。 クリーン システムとは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] と SharePoint の新しいインストールが含まれているが、ワークフロー プロジェクトは配置されていないコンピューターです。

### <a name="error-message"></a>エラー メッセージ
 SharePoint リストが見つかりません: ワークフローの履歴。

### <a name="resolution"></a>解決方法
 このエラーが発生するのは、ワークフローの履歴リストがないからです。 開発環境がクリーン システムの場合、ワークフローが配置されていないため、ワークフローの履歴リストはまだ存在しません。 この問題を解決するには、ワークフロー ウィザードをもう一度開きます。これにより、ワークフローの履歴リストが作成されます。

##### <a name="to-reenter-the-workflow-wizard"></a>ワークフロー ウィザードを再実行するには

1. **ソリューション エクスプローラー** でワークフロー ノードを選択します。

2. **[プロパティ]** ウィンドウで、省略記号 [...] ボタンが付いている任意のプロパティの省略記号ボタンを選択します。

## <a name="user-must-refresh-application-page-in-browser-while-debugging-to-view-updated-image"></a>デバッグ中に更新されたイメージを表示するにはブラウザーでアプリケーション ページを更新する必要がある
 デバッグしている SharePoint ソリューションに、イメージを表示するコントロール ([!INCLUDE[TLA2#tla_html](../sharepoint/includes/tla2sharptla-html-md.md)] Image コントロールなど) を含むアプリケーション ページが含まれている場合に、そのイメージに対して行われた変更を表示するには、ブラウザーでページを更新する必要があります。

## <a name="error-the-site-location-is-not-valid"></a>エラー: サイトの場所が有効ではありません
 この問題は、[!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] がインストールされていない場合に発生することがあります。 また、**SharePoint カスタマイズ ウィザード** で指定した SharePoint Web サイトに対する管理者の権限がない場合にも発生する可能性があります。

### <a name="error-message"></a>エラー メッセージ

- 入力されている SharePoint サイトの場所が有効ではありません。

### <a name="resolution"></a>解決方法

- [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]をインストールする。

- SharePoint Web サイトに対する管理者の権限があることを確認します。 詳細については、[!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] Online の記事「[SharePoint Server でサービス アプリケーションの管理者を割り当てる、または削除する](/sharepoint/administration/assign-or-remove-administrators-of-service-applications)」を参照してください。

## <a name="site-deletion-web-event-does-not-occur-in-event-receiver-project"></a>イベント レシーバー プロジェクトでサイト削除 Web イベントが発生しない
 イベント レシーバー プロジェクトを作成し、"サイトが削除されています" などの特定の Web イベントを選択すると、イベントは発生しません。

### <a name="error-message"></a>エラー メッセージ
 [なし] :

### <a name="resolution"></a>解決方法
 この問題は、サイト レベルのイベントを処理するにはフィーチャーのスコープが "サイト" である必要があるのに、イベント レシーバー プロジェクトの既定のフィーチャー スコープが "Web" になっているために発生します。 影響を受ける Web イベントは次のとおりです。

- サイトが削除されています (WebDeleting)

- サイトが削除されました (WebDeleted)

- サイトが移動されています (WebMoving)

- サイトが移動されました (WebMoved)

  この問題を修正するには、イベント レシーバーのフィーチャー スコープを次のように変更します。

##### <a name="to-change-the-feature-scope-of-the-event-receiver"></a>イベント レシーバーのフィーチャー スコープを変更するには

1. **ソリューション エクスプローラー** で、イベント レシーバーの *.feature* ファイルを、ダブルクリックするか、そのショートカット メニューを開いて **[開く]** を選択することにより、**フィーチャー デザイナー** で開きます。

2. **[スコープ]** の横にある矢印を選択し、表示される一覧で **[サイト]** を選択します。

## <a name="deployment-error-appears-after-the-name-of-an-identifier-in-a-business-data-connectivity-model-project-is-changed"></a>ビジネス データ接続モデル プロジェクトで識別子の名前を変更すると配置エラーが発生する
 この問題は、ビジネス データ接続 (BDC) モデルでエンティティの識別名を変更した後、ソリューションを配置しようとすると発生します。

### <a name="error-messages"></a>エラー メッセージ

- \<*model name*> には次の外部コンテンツ タイプ アクティブ化エラーがあります...

- 名前 '\<*model name*>' の IMetadataObject は、フィールド '名' の値が重複しています...

### <a name="resolution"></a>解決方法
 この問題を解決するには、モデルを手動で削除した後、ソリューションを再び配置します。  モデルを削除するには、次のどちらかのツールを使用します。

- SharePoint 2010 サーバーの全体管理。 詳細については、Microsoft TechNet Web サイトで [BDC モデルの管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14)#delete-a-bdc-model)に関する記事を参照してください。

- Windows PowerShell。 コマンドプロンプトでコマンド「**Remove-SPBusinessDataCatalogModel**」を入力することで、モデルを削除できます。 詳細については、Microsoft TechNet Web サイトで[コマンドレット全般 (SharePoint Server 2010)](/powershell/module/sharepoint-server) に関する記事を参照してください。

## <a name="an-error-appears-when-you-try-to-view-a-visual-web-part-in-sharepoint"></a>可視 Web パーツを SharePoint で表示しようとするとエラーが表示される
 この問題は、ユーザー コントロールの **[パス]** プロパティが文字列 "CONTROLTEMPLATES\\" で始まっていない場合に発生します。

### <a name="error-messages"></a>エラー メッセージ

- '/_CONTROLTEMPLATES/ *\<project name>* / *\<Web Part name>* / *\<user control name>* .ascx' ファイルが存在しません。

- Server Error in '/' Application.

### <a name="resolution"></a>解決方法

##### <a name="to-resolve-this-issue"></a>この問題を解決するには

1. **ソリューション エクスプローラー** で、ファイル名拡張子が *.ascx* であるユーザー コントロール ファイルを選択します。

2. メニュー バーで、 **[表示]**  >  **[プロパティ ウィンドウ]** の順に選択します。

3. **[プロパティ]** ウィンドウで、 **[配置場所]** ノードを展開します。

4. **[パス]** プロパティの値が、文字列 "CONTROLTEMPLATES\\" で始まっていることを確認します。

## <a name="error-appears-when-an-imported-reusable-workflow-that-contains-a-task-form-field-is-run"></a>インポートしたタスク フォーム フィールドを含む再使用可能なワークフローを実行するとエラーが表示される
 この問題は、フィールドを含むタスク フォームが存在するワークフローをインポートした後、ワークフローのインポート元と同じシステム上で新しいワークフローを実行したときに発生します。

### <a name="error-message"></a>エラー メッセージ
 配置手順 "機能のアクティブ化" でエラーが発生しました。機能 [*Guid*] に定義された ID [*Guid*] が、現在のサイト コレクションまたはサブサイト内で検出されました。

### <a name="resolution"></a>解決方法
 このエラーは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の再利用可能なワークフローのインポート プロジェクトでタスク フォームのフィールド ID が変更されないせいで、フィールド ID の競合が発生した結果です。 インポートしたワークフローを、元のワークフローと同じサーバー上に配置すると、フィールド ID の競合が発生します。

 この問題を解決するには、検索置換機能を使用して、インポートしたすべてのワークフロー ファイル内のフィールド ID 属性の値を変更する必要があります。

## <a name="error-appears-when-a-renamed-imported-list-instance-is-run"></a>インポートして名前を変更したリスト インスタンスを実行するとエラーが表示される
 この問題は、インポートしたリスト インスタンスの名前を変更した後、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で実行した場合に発生します。

### <a name="error-message"></a>エラー メッセージ
 ビルド エラー: 配置手順 '機能のアクティブ化' でエラーが発生しました。Template\Features\\[*import project*<em>feature</em>*name*]\Files\Lists\\[*old*<em>list name</em>]\Schema.xml ファイルが存在しません。

### <a name="resolution"></a>解決方法
 リスト インスタンスをインポートすると、CustomSchema という名前の属性がリスト インスタンスの Elements.xml ファイルに追加されます。 Elements.xml には、リスト インスタンス用のカスタム schema.xml のパスが含まれます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でリスト インスタンスの名前を変更すると、カスタム schema.xml の配置パスは変更されますが、CustomSchema 属性のパス値は更新されません。 この結果、機能がアクティブ化されるときに、リスト インスタンスは、CustomSchema 属性に指定された古いパスでは *schema.xml* ファイルを検出できません。

 この問題を解決するには、CustomSchema 属性の *schema.xml* ファイルの配置場所のパスを更新します。

## <a name="sharepoint-debugging-session-terminated-by-iis"></a>SharePoint デバッグ セッションが IIS によって終了する
 この問題は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ソリューション内にブレークポイントを設定し、**F5** キーを押してソリューションを実行した後、ブレークポイントで 90 秒以上停止した場合に発生します。

### <a name="error-message"></a>エラー メッセージ
 デバッグ対象の Web サーバー プロセスは、インターネット インフォメーション サービス (IIS) によって停止されました。 IIS のアプリケーション プールの ping の設定を構成することによって、この問題を回避できます。 詳細については、ヘルプを参照してください。

### <a name="resolution"></a>解決方法
 既定では、IIS アプリケーション プールは、アプリケーションから応答が返るまで 90 秒間待機した後、アプリケーションを閉じます。 このプロセスは、アプリケーションの "ping" として知られています。 この問題を解決するには、待機時間を増やすか、アプリケーションの ping を完全に無効にします。

##### <a name="to-access-the-iis-app-pool-settings"></a>IIS アプリケーション プールの設定にアクセスするには

1. IIS マネージャーを開きます。

2. **[接続]** ペインで SharePoint サーバー ノードを展開し、 **[アプリケーション プール]** ノードを選択します。

3. **[アプリケーション プール]** ページで、SharePoint アプリケーション プール (通常は "SharePoint - 80") を選択した後、 **[操作]** ペインで **[詳細設定]** リンクを選択します。

4. IIS がタイムアウトするまでの待機時間を長くするには、 **[Ping 最大応答時間 (秒)]** を、90 秒より大きな値に変更します。

5. IIS の ping を無効にするには、 **[Ping の有効化]** を **[False]** に設定します。

## <a name="auto-retract-leaves-orphaned-list-instance-in-sharepoint"></a>自動取り消しで孤立状態のリスト インスタンスが SharePoint に残る
 この問題は、次の手順に従った場合に発生します。

1. リスト インスタンスがあるリスト定義を [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成します。

2. **F5** キーを押してソリューションを実行します。

3. デバッグを停止するか、SharePoint サイトを閉じます。

4. SharePoint サイトを再度開き、リスト インスタンスを開きます。

### <a name="error-message"></a>エラー メッセージ
 Server Error in '/' Application.

### <a name="resolution"></a>解決方法
 このエラーは、SharePoint ソリューションのデバッグ セッションを閉じた後、自動取り消し機能によってソリューションが取り消されたために発生します。 取り消しにより、リスト定義は SharePoint から削除されますが、リスト インスタンスは削除されません。 リスト インスタンスは、基になるリスト定義を必要とします。

 この問題を解決するには、メニュー バーの **[ビルド]**  >  **[配置]** を選択して、ソリューションを配置します。 (**F5** キーを押してソリューションをデバッグしないでください)。次に、SharePoint 内のリスト インスタンスを削除します。

## <a name="original-sharepoint-solution-is-replaced-by-an-exported-version"></a>元の SharePoint ソリューションがエクスポートしたバージョンによって置換される
 エクスポートした SharePoint ソリューションを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] にインポートした後、そのソリューションをエクスポート元のサイトに配置した場合、元の SharePoint ソリューションが置換されます。 この問題は、ソリューションの配置先を元のソリューションがアクティブ化されていないサーバーにすると、発生しません。

### <a name="error-message"></a>エラー メッセージ
 [なし] :

### <a name="resolution"></a>解決方法
 エクスポート元のサイトでソリューションが上書きされないようにするには、ソリューション ID の GUID と [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] プロジェクトにインポートしたすべての機能の機能 ID を変更します。

## <a name="error-appears-when-debugging-starts"></a>デバッグ開始時にエラーが表示される
 Visual Studio で SharePoint ソリューションのデバッグを開始すると、特定のキーがディクショナリに存在しないので Visual Studio で Web.config ファイルを読み込むことができないというエラーが発生します。

### <a name="error-message"></a>エラー メッセージ
 Web.config 構成ファイルを読み込むことができませんでした。 ファイルをチェックして、形式が正しくない XML 要素を修正した後、再試行してください。 次のエラーが発生しています: 特定のキーがディクショナリに存在しません。

### <a name="resolution"></a>解決方法
 この問題を解決するには、Visual Studio 内の SharePoint プロジェクトの [サイト URL] プロパティの値が、Web アプリケーションの代替アクセス マッピング用の既定のゾーンに割り当てられた URL と一致することを確認します。 URL でイントラネットなどの他のゾーンを使用すると、エラーは解消されません。 プロジェクトのサイト URL と既定のゾーンの URL は一致している必要があります。 代替アクセス マッピングにアクセスするには、SharePoint 2010 サーバーの全体管理ユーティリティを開き、 **[アプリケーション構成の管理]** リンクを選択し、 **[Web アプリケーション]** の下の **[代替アクセス マッピングの構成]** リンクを選択します。 詳細については、「[Web アプリケーション用の領域を作成する](/previous-versions/office/sharepoint-2007-products-and-technologies/cc263087(v=office.12))」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [SharePoint のパッケージ化と配置のトラブルシューティング](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Visual Studio でのデバッグ](../debugger/debugger-feature-tour.md)