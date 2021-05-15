---
title: Office プログラミングの共通タスク
description: Microsoft Office Word または Office Excel のオブジェクト モデルを使用せずに、ドキュメントレベルのカスタマイズでデータに対してプログラミングする方法について説明します。
ms.custom: SEO-VS-2020SS
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, getting started
- FAQs (frequently asked questions) [Office development in Visual Studio]
- Office development in Visual Studio, frequently asked questions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 67b09d3881dcde1d404b7ff0c1096ced1ecb50ea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910602"
---
# <a name="common-tasks-in-office-programming"></a>Office プログラミングの共通タスク
  このトピックは、Visual Studio を使用した Office ソリューションのプログラミングに共通する質問のうち、次のカテゴリの質問に対する回答を簡単に見つけることができるように構成されています。

- [セットアップ タスクと一般的なタスク](#projects)。

- [ユーザー インターフェイスのカスタマイズ タスク](#ui)。

- [Excel の自動化タスク](#excel)。

- [Word の自動化タスク](#word)。

- [データ タスク](#data)。

- [サーバー側のドキュメント管理タスク](#server)

- [セキュリティ タスク](#security)

- [配置タスク](#deployment)

## <a name="setup-and-general-tasks"></a><a name="projects"></a> セットアップ タスクと一般的なタスク

- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)。

- [方法: Office ソリューションをアップグレードする](/previous-versions/4bez6837(v=vs.140))。

- [方法: Office のプライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)。

- [方法: プライマリ相互運用機能アセンブリを使用して Office アプリケーションを対象にする](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)。

- [方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)。

- [方法: コードを実行せずに Office ソリューションを開く](../vsto/how-to-open-office-solutions-without-running-code.md)。

- [方法: Office ソリューションの構成情報を設定する](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)。

- [方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

- [方法: アドインのユーザー インターフェイス エラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)。

## <a name="user-interface-customization-tasks"></a><a name="ui"></a> ユーザー インターフェイスのカスタマイズ タスク

### <a name="controls-on-documents-and-worksheets"></a>ドキュメントとワークシートに含まれるコントロール

- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

- [方法: ワークシートに NamedRange コントロールを追加する](../vsto/how-to-add-namedrange-controls-to-worksheets.md)。

- [方法: ワークシートに ListObject コントロールを追加する](../vsto/how-to-add-listobject-controls-to-worksheets.md)。

- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)。

- [方法: Word 文書にコンテンツ コントロールを追加する](../vsto/how-to-add-content-controls-to-word-documents.md)。

- [方法: Word 文書に Bookmark コントロールを追加する](../vsto/how-to-add-bookmark-controls-to-word-documents.md)。

### <a name="task-panes-in-document-level-customizations"></a>ドキュメントレベルのカスタマイズに含まれるタスク ウィンドウ

- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)。

### <a name="task-panes-in-vsto-add-ins"></a>VSTO アドインに含まれるタスク ウィンドウ

- [方法: カスタム タスク ウィンドウをアプリケーションに追加する](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)。

### <a name="ribbon-customizations"></a>リボンのカスタマイズ

- [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)。

- [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)。

- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)。

- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)。

- [方法: リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)。

### <a name="outlook-form-regions"></a>Outlook フォーム領域

- [方法: フォーム領域を Outlook アドイン プロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

- [方法: Outlook にフォーム領域が表示されないようにする](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)。

### <a name="custom-menus"></a>カスタム メニュー

- [方法: ショートカット メニューにコマンドを追加する](../vsto/how-to-add-commands-to-shortcut-menus.md)。

## <a name="excel-automation-tasks"></a><a name="excel"></a> Excel の自動化タスク

- [方法: プログラムによってワークシートのセルに文字列を表示する](../vsto/how-to-programmatically-display-a-string-in-a-worksheet-cell.md)。

- [方法: プログラムによって新しいブックを作成する](../vsto/how-to-programmatically-create-new-workbooks.md)。

- [方法: プログラムによってブックを開く](../vsto/how-to-programmatically-open-workbooks.md)。

- [方法: プログラムによってブックを保存する](../vsto/how-to-programmatically-save-workbooks.md)。

- [方法: プログラムによってブックを閉じる](../vsto/how-to-programmatically-close-workbooks.md)。

- [方法: プログラムを使用して新しいワークシートをブックに追加する](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)。

- [方法: プログラムによってワークシートを非表示にする](../vsto/how-to-programmatically-hide-worksheets.md)。

- [方法: ブック内のワークシートをプログラムによって移動する](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)。

- [方法: プログラムによってブックを保護する](../vsto/how-to-programmatically-protect-workbooks.md)。

- [方法: プログラムによってコード内でワークシートの範囲を参照する](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)。

- [方法: プログラムによってブック内の範囲にスタイルを適用する](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)。

- [方法: 選択されたセルを含むワークシートの行の書式をプログラムによって変更する](../vsto/how-to-programmatically-change-formatting-in-worksheet-rows-containing-selected-cells.md)。

- [方法: プログラムによってワークシートの範囲内のテキストを検索する](../vsto/how-to-programmatically-search-for-text-in-worksheet-ranges.md)。

- [方法: プログラムによってワークシートを印刷する](../vsto/how-to-programmatically-print-worksheets.md)。

- [方法: Excel の計算をプログラムで実行する](../vsto/how-to-programmatically-run-excel-calculations-programmatically.md)。

- [方法: プログラムを使用してワークシート内のデータを並べ替える](../vsto/how-to-programmatically-sort-data-in-worksheets.md)。

## <a name="word-automation-tasks"></a><a name="word"></a> Word の自動化タスク

- [方法: プログラムによって新しい文書を作成する](../vsto/how-to-programmatically-create-new-documents.md)。

- [方法: プログラムによって既存文書を開く](../vsto/how-to-programmatically-open-existing-documents.md)。

- [方法: プログラムによって文書を保存する](../vsto/how-to-programmatically-save-documents.md)。

- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)。

- [方法: プログラムによって Word 文書にテキストを挿入する](../vsto/how-to-programmatically-insert-text-into-word-documents.md)。

- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)。

- [方法: プログラムによって Word 文書の範囲をリセットする](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)。

- [方法: プログラムによって文書内のテキストに書式を設定する](../vsto/how-to-programmatically-format-text-in-documents.md)。

- [方法: Word 文書に XMLNode コントロールを追加する](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)。

- [方法: プログラムによってブックマークのテキストを更新する](../vsto/how-to-programmatically-update-bookmark-text.md)。

- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)。

- [方法: プログラムによって文書を印刷する](../vsto/how-to-programmatically-print-documents.md)。

- [方法: プログラムによって Word の表を作成する](../vsto/how-to-programmatically-create-word-tables.md)。

- [方法: プログラムによって Word の表に行と列を追加する](../vsto/how-to-programmatically-add-rows-and-columns-to-word-tables.md)。

- [方法: プログラムによって文書内の文字数をカウントする](../vsto/how-to-programmatically-count-characters-in-documents.md)。

## <a name="data-tasks"></a><a name="data"></a> データ タスク

### <a name="data-bound-controls"></a>データ バインド コントロール

- [方法: データベースのデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)。

- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)。

- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)。

- [方法: ホスト コントロールのデータでデータ ソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

### <a name="cached-data-in-document-level-solutions"></a>ドキュメントレベルのソリューションでキャッシュされるデータ

- [方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- [方法: Office ドキュメント内のデータ ソースをプログラムでキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)。

- [方法: パスワードで保護されたドキュメント内のデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

### <a name="custom-xml-data"></a>カスタム XML データ

- [方法: ドキュメントレベルのカスタマイズにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)。

- [方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)。

## <a name="server-side-document-management-tasks"></a><a name="server"></a> サーバー側ドキュメントの管理タスク

- [方法: マネージド コード拡張をドキュメントから削除する](../vsto/how-to-remove-managed-code-extensions-from-documents.md)。

- [方法: マネージド コード拡張機能をドキュメントにアタッチする](../vsto/how-to-attach-managed-code-extensions-to-documents.md)。

## <a name="security-tasks"></a><a name="security"></a> セキュリティ タスク

- [方法: Office ソリューションに署名する](../vsto/how-to-sign-office-solutions.md)。

## <a name="deployment-tasks"></a><a name="deployment"></a> 配置タスク

- [方法: ClickOnce を使用して Office ソリューションを発行する](/previous-versions/bb386095(v=vs.110))。

- [方法: ClickOnce を使用してドキュメント レベルの Office ソリューションを SharePoint Server に発行する](/previous-versions/bb608595(v=vs.110))。

- [方法: ClickOnce Office ソリューションをインストールする](/previous-versions/bb608592(v=vs.110))。

- [方法: Office ソリューションを実行するためにエンド ユーザーのコンピューターに必須コンポーネントをインストールする](/previous-versions/bb608608(v=vs.110))。

- [方法: Office ソリューションの配置用に IIS を準備する](/previous-versions/bb608629(v=vs.110))。

- [方法: 配置した Office ソリューションを更新する](/previous-versions/bb157871(v=vs.110))。

- [方法: Office ソリューションのインストール パスを変更する](/previous-versions/bb608626(v=vs.110))。

## <a name="see-also"></a>関連項目
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office アプリケーションとプロジェクト タイプ別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)