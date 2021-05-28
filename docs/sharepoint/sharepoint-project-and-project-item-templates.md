---
title: SharePoint のプロジェクト テンプレートとプロジェクト項目テンプレート | Microsoft Docs
description: SharePoint で使用可能なプロジェクト テンプレートとプロジェクト項目テンプレート、およびそれらの使用方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.FirstWizardPage
- VS.SharePointTools.SPE.ListInstance
- VS.SharePointTools.SPE.ListDefinition
- VS.SharePointTools.SPE.ListDefFromContentType
- VS.SharePointTools.SPE.ContentType
- SPE.Wizard
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, project and project item templates
- SharePoint development in Visual Studio, templates
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8482a6185f670ce1bb340ff40fe277b751a39c06
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892334"
---
# <a name="sharepoint-project-and-project-item-templates"></a>SharePoint のプロジェクト テンプレートとプロジェクト項目テンプレート
  以下のセクションでは、SharePoint プロジェクトとプロジェクト項目の使用可能なテンプレート、およびそれらの使用方法について説明します。

## <a name="project-and-project-item-templates-overview"></a>プロジェクト テンプレートとプロジェクト項目テンプレートの概要
 Visual Studio で新しい SharePoint プロジェクトを作成すると、その種類のプロジェクトに必要なすべてのプロジェクト項目と共にソリューションに追加されます。 たとえば、Silverlight Web パーツ プロジェクトを作成した場合、視覚的 Web パーツ プロジェクト項目と Silverlight アプリケーション プロジェクト項目、およびそれらのプロジェクト項目に必要なすべてのファイルを含むソリューションが作成されます。 プロジェクト項目テンプレートは、既存の SharePoint プロジェクトにプロジェクト項目 (イベント レシーバー、サイト列、リストなど) を追加する目的で使用されます。

 SharePoint の基礎については、[SharePoint Foundation の構成要素](/previous-versions/office/developer/sharepoint-2010/ee534971(v=office.14))に関する記事を参照してください。 上級ユーザーは、プロジェクトやプロジェクト項目のテンプレートを独自に作成することもできます。 詳細については、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

## <a name="project-templates"></a>プロジェクト テンプレート
 ここでは、それぞれの SharePoint プロジェクト テンプレートについて説明します。 Visual Studio で SharePoint プロジェクト テンプレートを表示するには、 **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** を選択します。

### <a name="sharepoint-2010-project"></a>SharePoint 2010 プロジェクト
 "*SharePoint 2010 プロジェクト*" の内容は、すべての SharePoint プロジェクト テンプレートに含まれています。 SharePoint 2010 プロジェクトの内容は次のとおりです。

- プロジェクト ファイル。

- プロジェクトのプロパティ ページ。

- **[参照設定]** フォルダー。プロジェクトのすべてのアセンブリ参照を一覧表示します。

- **[フィーチャー]** フォルダー。SharePoint サーバーにフィーチャーを配置するために使用される *.feature* 構成ファイルを格納します。

- **[パッケージ]** フォルダー。SharePoint にソリューションを配置するために使用される *Package.package* ファイルを格納します。

- key.snk (厳密名キー) ファイル。セキュリティ対策としてアセンブリに厳密な名前で署名するために使用されます。

### <a name="sharepoint-2010-silverlight-web-part"></a>SharePoint 2010 Silverlight Web パーツ
 "*SharePoint 2010 Silverlight Web パーツ*" プロジェクトでは、Silverlight アプリケーションを表示する SharePoint の Web パーツを作成できます。 このプロジェクトを作成するときは、新しい Silverlight アプリケーションを追加するか既存の Silverlight アプリケーションを参照するかを指定できます。 詳細については、「[SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)」と「[チュートリアル: SharePoint の OData を表示する Silverlight Web パーツを作成する](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)」を参照してください。

### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 視覚的 Web パーツ
 "*SharePoint 2010 視覚的 Web パーツ*" プロジェクトには、*Elements.xml* 定義ファイル、**Web パーツ** 項目、および **ユーザー コントロール** 項目が含まれています。 視覚的 Web パーツの外観をデザインするには、Visual Studio のツールボックスからユーザー コントロールのサーフェイスにコントロールをドラッグするかコピーします。 詳細については、「[方法: デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)」と「[構成要素: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

### <a name="import-sharepoint-2010-solution-package"></a>SharePoint 2010 ソリューション パッケージのインポート
 "*SharePoint 2010 ソリューション パッケージのインポート*" プロジェクトでは、SharePoint ソリューション ( *.wsp*) ファイルにエクスポートされた既存の SharePoint 2010 サイトの全体または一部を Visual Studio にインポートできます。 Visual Studio にインポートした後は、その項目をカスタマイズして再配置することができます。 詳細については、「[既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

### <a name="import-reusable-sharepoint-2010-workflow"></a>再利用可能な SharePoint 2010 ワークフローのインポート
 "*再利用可能な SharePoint 2010 ワークフローのインポート*" プロジェクトでは、SharePoint Designer 2010 で作成した再利用可能な宣言型のワークフローを Visual Studio にインポートできます。 ワークフローは、SharePoint サイトから *.wsp* ファイルとしてエクスポートされます。 Visual Studio にインポートした後は、カスタマイズしたりコードを追加したりして、SharePoint サイトに配置できます。 詳細については、「[チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)」を参照してください。

## <a name="project-item-templates"></a>プロジェクト項目テンプレート
 ここでは、それぞれの SharePoint プロジェクト項目テンプレートについて説明します。 プロジェクト項目テンプレートでは、サイト列、リスト、コンテンツ タイプなどの SharePoint 機能をサポートするために、SharePoint ソリューションにファイルを追加します。 たとえば、サイト列をソリューションに追加すると、*Elements.xml* 定義ファイルを含むサイト列プロジェクトが追加されます。 また、視覚的 Web パーツを追加すると、*Elements.xml* ファイル、ユーザー コントロール項目、および視覚的 Web パーツ項目を含む視覚的 Web パーツ プロジェクトがソリューションに追加されます。

 SharePoint プロジェクト項目テンプレートを表示するには、**ソリューション エクスプローラー** で、SharePoint プロジェクトのショートカット メニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。 **[Visual C#]** または **[Visual Basic]** の **[SharePoint]** ノードを展開し、 **[2010]** を選択します。

### <a name="application-page-farm-solution-only"></a>アプリケーション ページ (ファーム ソリューションのみ)
 **[アプリケーション ページ (ファーム ソリューションのみ)]** 項目は、SharePoint サイト用の [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] Web ページをデザインするために使用できます。 アプリケーション ページは、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[方法: アプリケーション ページを作成する](../sharepoint/how-to-create-an-application-page.md)」と「[アプリケーションの _layouts ページの種類](/previous-versions/office/aa979604(v=office.14))」を参照してください。

### <a name="business-data-connectivity-model-farm-solution-only"></a>ビジネス データ接続モデル (ファーム ソリューションのみ)
 **[ビジネス データ接続モデル (ファーム ソリューションのみ)]** 項目は、SharePoint にビジネス データを統合するために使用できます。 [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)]、Siebel、Service Advertising Protocol (SAP) などのバック エンドのサーバー アプリケーションからのデータを使用できます。 ビジネス データ接続モデル (ファーム ソリューションのみ) は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)」、「[方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)」、「[新機能: Business Connectivity Services](/previous-versions/office/developer/sharepoint-2010/ee534979(v=office.14))」を参照してください。

### <a name="content-type"></a>Content type
 "*コンテンツ タイプ*" 項目を使用すると、ドキュメント、お知らせ、タスクなどの既存の (基本) コンテンツ タイプを基にしてカスタム コンテンツ タイプを作成できます。 カスタム コンテンツ タイプでは、独自に定義したサイト列 (フィールド) に加えて、ベース コンテンツ タイプと同じ属性およびフィールドを使用できます。 たとえば、SharePoint に付属している基本の Contact コンテンツ タイプを基にしてカスタムの Contact コンテンツ タイプを作成できます。 コンテンツ タイプのカスタマイズでは、基本コンテンツ タイプの既存のサイト列を変更したり、別のサイト列を追加したりできます。

> [!NOTE]
> SharePoint の制限により、サンドボックス ソリューション コンテンツ タイプを基にしてファーム ソリューション コンテンツ タイプを作成することはできません。

 詳細については、「[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)」と「[構成要素: コンテンツ タイプ](/previous-versions/office/developer/sharepoint-2010/ee535063(v=office.14))」を参照してください。

### <a name="empty-element"></a>空要素
 "*空の要素*" は、ほとんどの場合、Visual Studio のプロジェクト テンプレートまたはプロジェクト項目テンプレートを持たない SharePoint プロジェクト項目を定義するために使用します。 プロジェクトに空の要素を追加すると、EmptyElement[x] というノードが作成されます ([x] は一意の番号\)。 EmptyElement[x] には、*Elements.xml* という名前のファイルが 1 つ含まれています。 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ステートメントを使用して、必要な要素を *Elements.xml* で定義します。

### <a name="event-receiver"></a>イベント レシーバー
 "*イベント レシーバー*" は、リストへの項目の追加、Web 項目の削除、ワークフローの開始など、SharePoint サイト内の項目に対するイベントを処理します。 イベント レシーバー プロジェクト項目テンプレートで処理できるイベントは次のとおりです。

- イベントを一覧表示します

- リスト アイテム イベント

- リスト電子メール イベント

- Web イベント

- リスト ワークフロー イベント

  イベント レシーバー プロジェクト項目では、 **[イベント レシーバー]** フォルダーが作成されます。このフォルダーには、**SharePoint カスタマイズ ウィザード** でプロジェクトの作成時に指定したすべてのイベントのイベント ハンドラーを含む 1 つのクラス ファイルが格納されます。 イベント レシーバー クラスは、SharePoint サイトで項目 (ファイル、フィールド、アイテム、リスト、添付、Web パーツ、ワークフローなど) が追加、更新、または削除されたときに発生するイベントを処理できます。 詳細については、「[方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)」と「[構成要素: イベント処理](/previous-versions/office/developer/sharepoint-2010/ee535057(v=office.14))」を参照してください。

### <a name="list"></a>List
 リストは、再利用可能な基本の SharePoint リスト定義のインスタンスです (予定表、タスク リストなど)。 ソリューションにリストを追加した後、リスト デザイナーで、リストにサイト列を追加したり、リストのカスタム列を作成したりできます。 これにはコンテンツ タイプのサイト列が含まれます。 リストの "*ビュー*" を指定すると、リストに表示される列が決まります。 詳細については、「[チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)」と「[構成要素: リストとドキュメント ライブラリ](/previous-versions/office/developer/sharepoint-2010/ee534985(v=office.14))」を参照してください。

### <a name="module"></a>モジュール
 "*モジュール*" ([!include[vbprvb](../sharepoint/includes/vbprvb-md.md)] のモジュールとは異なる) には、イメージやメモなど、SharePoint サーバーに配置するファイルが格納されます。 モジュール プロジェクト項目には **[モジュール]** ノードが含まれます。 モジュール ノードに 2 つのプロジェクト項目テンプレートが含まれています。1 つはモジュールのマニフェストとして機能する XML 定義ファイルで、もう 1 つはプレースホルダー ファイルの *sample.txt* ファイルです。 詳細については、「[モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)」と「[モジュール](/previous-versions/office/developer/sharepoint-2010/ms453137(v=office.14))」を参照してください。

### <a name="sequential-workflow-farm-solution-only"></a>シーケンシャル ワークフロー (ファーム ソリューションのみ)
 "*シーケンシャル ワークフロー*" は、最後のステップが完了するまで順番に実行される一連のビジネス ロジック ステップです。 シーケンシャル ワークフローは、リストやドキュメントなどの SharePoint アイテムが関係するプロセスを管理する目的で使用します。 サイト レベル (グローバル) のワークフローまたはリスト レベル (ローカル) のワークフローを作成できるほか、ワークフローを自動的に開始するか、手動で開始するかを選択することもできます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)」、「[SharePoint Server 2010 でのワークフロー](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))」、[新機能: ワークフローに関する機能拡張](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))に関する記事を参照してください。

### <a name="silverlight-web-part"></a>Silverlight Web パーツ
 "*Silverlight Web パーツ*" プロジェクト項目では、Silverlight アプリケーションを表示する SharePoint の Web パーツを作成できます。 このプロジェクト項目ソリューションに追加するときは、新しい Silverlight アプリケーションを追加するか既存の Silverlight アプリケーションを後で参照するかを選択できます。 詳細については、「[SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)」と「[チュートリアル: SharePoint の OData を表示する Silverlight Web パーツを作成する](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)」を参照してください。

### <a name="site-column"></a>サイト列
 "*サイト列*" ("*フィールド*" とも呼ばれます) は、SharePoint プロジェクトに追加できる最も基本的な要素の 1 つです。 サイト列はデータの種類を表します。たとえば、連絡先一覧であれば、連絡先の電話番号、テキスト コメント、都市名などです。 詳細については、「[SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)」と「[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))」を参照してください。

### <a name="site-definition-farm-solution-only"></a>サイト定義 (ファーム ソリューションのみ)
 "*サイト定義*" プロジェクト項目には、次のファイルを含むサイト定義フォルダーが含まれています。

- 既定の .aspx ページ。サイトの既定の Web ページとして使用されます。

- *onet.xml* ファイル。サイトの構成要素の定義が含まれています。

- webtemp xml ファイル。 **[新しい SharePoint サイト]** ページの **[テンプレートの選択]** セクションに表示されるサイト定義構成を指定します。

  サイト定義の追加後は、コードおよびファイルを追加して機能を導入できます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[SharePoint のサイト定義を作成する](../sharepoint/creating-site-definitions-for-sharepoint.md)」と「[サイト定義と構成](/previous-versions/office/developer/sharepoint-2010/aa978512(v=office.14))」を参照してください。

### <a name="state-machine-workflow-farm-solution-only"></a>ステート マシンのワークフロー (ファーム ソリューションのみ)
 "*ステート マシン ワークフロー*" は、ビジネス ロジックの状態、遷移、およびアクションで構成されます。 ステート マシン ワークフローに含まれる各ステップは、順番に実行されるのではなく、アクションおよび状態によってトリガーされます。 シーケンシャル ワークフローと同様に、ステート マシン ワークフローは、リストやドキュメントなどの SharePoint アイテムに関連付けられます。 サイト レベル (グローバル) のワークフローまたはリスト レベル (ローカル) のワークフローを作成できることも、シーケンシャル ワークフローと同じです。 ワークフローを自動的に開始するか手動で開始するかを選択することもできます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)」、「[SharePoint Server 2010 でのワークフロー](/previous-versions/office/developer/sharepoint-2010/ms549489(v=office.14))」、[新機能: ワークフローに関する機能拡張](/previous-versions/office/developer/sharepoint-2010/ee537015(v=office.14))に関する記事を参照してください。

### <a name="user-control-farm-solution-only"></a>ユーザー コントロール (ファーム ソリューションのみ)
 "*ユーザー コントロール*" は、他の ASP.NET コントロールや SharePoint コントロールを追加できる再利用可能なカスタムのコントロールです。 ユーザー コントロールは、SharePoint で実行されるアプリケーション ページと Web パーツに追加できます。 このプロジェクト項目は、ファーム ソリューションでのみ使用できます。 このプロジェクト項目はファーム ソリューションにしか追加できません。 詳細については、「[Web パーツまたはアプリケーション ページの再利用できるコントロールの作成](creating-reusable-controls-for-web-parts-or-application-pages.md)」を参照してください。

### <a name="visual-web-part"></a>可視 Web パーツ
 "*視覚的 Web パーツ*" プロジェクト項目には、*Elements.xml* 定義ファイル、**Web パーツ** 項目、および **ユーザー コントロール** 項目が含まれています。 視覚的 Web パーツの外観をデザインするには、Visual Studio のツールボックスからユーザー コントロールのサーフェイスにコントロールをドラッグするかコピーします。 詳細については、「[方法: デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)」と「[構成要素: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

### <a name="web-part"></a>Web パーツ
 "*Web パーツ*" は、Web パーツ ページと呼ばれる特殊な種類のページ内で実行されるサーバー側のコントロールです。 これらは、SharePoint サイトに表示されるページのビルド ブロックです。 Web パーツ項目には、SharePoint サイト用の Web パーツをデザインするためのファイルが用意されています。 詳細については、「[方法: SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)」と「[構成要素: Web パーツ](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint 製品とテクノロジ](/previous-versions/office/developer/sharepoint-2010/dd776256(v=office.12))
