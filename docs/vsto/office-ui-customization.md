---
title: Office UI のカスタマイズ
description: Visual Studio の Office Developer Tools を使用して Microsoft Office アプリケーションのユーザー インターフェイス (UI) をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- menus [Office development in Visual Studio], customizing
- actions panes [Office development in Visual Studio], creating
- WPF [Office development in Visual Studio]
- toolbars [Office development in Visual Studio], customizing
- Office applications [Office development in Visual Studio], UI customization
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ed604b1bbbfcd5b217935b541325c121d521e878
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99849815"
---
# <a name="office-ui-customization"></a>Office UI のカスタマイズ
  Microsoft Office アプリケーションのユーザー インターフェイス (UI) は、Visual Studio の  Office Developer Tools を使用してカスタマイズできます。 以下のトピックでは、カスタマイズできる UI 機能について説明します。

- [UI の機能の比較](#Comparison)

- [操作ウィンドウとカスタム作業ウィンドウ](#Actions)

- [カスタム リボンの UI](#Ribbon)

- [Backstage ビュー](#Backstage)

- [Outlook フォーム領域](#FormRegion)

- [文書のコントロール](#Controls)

- [ショートカット メニュー](#Shortcut)

## <a name="comparison-of-ui-features"></a><a name="Comparison"></a> UI の機能の比較
 次の表では、Microsoft Office プロジェクトでカスタマイズできる主な UI 機能を比較します。

|機能|サポートされているプロジェクトの種類|サポートされる Microsoft Office アプリケーション|
|-------------|-----------------------------|---------------------------------------------|
|[操作] ウィンドウ|ドキュメント レベルのカスタマイズ|Excel<br /><br /> Word|
|カスタム作業ウィンドウ|VSTO アドイン|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Word|
|カスタム リボンの UI|ドキュメント レベルのカスタマイズ<br /><br /> VSTO アドイン|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Word<br /><br /> Visio|
|Backstage ビュー|ドキュメント レベルのカスタマイズ<br /><br /> VSTO アドイン|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)].<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Word<br /><br /> Visio|
|Outlook フォーム領域|VSTO アドイン|Outlook|
|ドキュメントのコントロール|ドキュメント レベルのカスタマイズ<br /><br /> VSTO アドイン|Excel<br /><br /> Word|
|ショートカット メニュー|ドキュメント レベルのカスタマイズ<br /><br /> VSTO アドイン|Excel<br /><br /> [!INCLUDE[InfoPath_15_short](../vsto/includes/infopath-15-short-md.md)]<br /><br /> [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)]<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Word<br /><br /> Visio<br /><br /> Excel|

## <a name="actions-panes-and-custom-task-panes"></a><a name="Actions"></a> 操作ウィンドウとカスタム作業ウィンドウ
 作業ウィンドウは、通常、Microsoft Office アプリケーションのウィンドウの一辺にドッキングされているユーザー インターフェイス ウィンドウです。 ほぼすべての Microsoft Office アプリケーションには組み込みの作業ウィンドウがあります。 作業ウィンドウの例として、Word のヘルプ作業ウィンドウがあります。

 Visual Studio の Office 開発ツールには、作業ウィンドウをカスタマイズする方法が 2 つあります。

- ドキュメントレベルのカスタマイズには、操作ウィンドウを追加できます。 既定では、アプリケーションの右側、ドキュメントの右側に操作ウィンドウが表示されます。 操作ウィンドウは、ドキュメントの左、上、または下に表示することもできます。

- VSTO アドインには、カスタム作業ウィンドウを追加できます。 ユーザーは、アプリケーション ウィンドウのいずれかの辺にカスタム作業ウィンドウをドッキングすることができます。また、ウィンドウの任意の場所にカスタム作業ウィンドウをドラッグすることができます。

  操作ウィンドウやカスタム作業ウィンドウには、データ エントリなど、ユーザーのタスクを支援するさまざまなコントロールが用意されています。 リボン グループと比較すると、操作ウィンドウとカスタム作業ウィンドウには、テキストやコントロールを含む大きな領域があります。

  操作ウィンドウの詳細については、「[操作ウィンドウの概要](../vsto/actions-pane-overview.md)」を参照してください。 カスタム作業ウィンドウの詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="custom-ribbon-ui"></a><a name="Ribbon"></a> カスタム リボンの UI
 Office のアプリケーションに追加する機能を表示するようにリボン UI をカスタマイズすることができます。 リボンを使用すると、関連するコマンドを (コントロールの形式で) 見つけやすいように整理できます。 独自のリボン タブとグループを作成し、ソリューションで提供する機能にユーザーがアクセスできるようにすることができます。 旧バージョンの Microsoft Office System でメニューとツールバーを使用してアクセスしていた機能の多くは、現在ではリボンを使用してアクセスできます。

 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

## <a name="backstage-view"></a><a name="Backstage"></a> Backstage ビュー
 Office アプリケーションで **[ファイル]** タブをクリックすると、Backstage ビューが開きます。 Backstage ビューには、ファイルレベルのタスクと操作を組み合わせた UI が用意されています。Backstage は、2007 Microsoft Office System の Microsoft Office ボタンで使用できる似た機能の置き換えです。 Backstage ビューは、XML を使用してフルに拡張することができます。

 Visual Studio には、Backstage ビューをカスタマイズできるデザイナーや API が用意されていません。 ただし、Office プロジェクトに **リボン (XML)** 項目を追加する場合、XML をリボン XML ファイルに追加して Backstage ビューをカスタマイズすることはできます。 **リボン (XML)** 項目の詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。

 Backstage ビューのカスタマイズの詳細については、[開発者向け Office 2010 Backstage ビューの概要](/previous-versions/office/developer/office-2010/ee691833(v=office.14))および[開発者向け Office 2010 Backstage ビューのカスタマイズ](/previous-versions/office/developer/office-2010/ee815851(v=office.14))に関するそれぞれのページを参照してください。

## <a name="outlook-form-regions"></a><a name="FormRegion"></a> Outlook フォーム領域
 標準の Microsoft Office Outlook フォームにカスタム機能を追加するには、フォーム領域を使用します。 フィールドまたはコントロールを追加して既存のフォームを拡張するフォーム領域を作成できます。 Visual Studio で Office 開発ツールを使用して新しいフォーム領域を作成する場合、フォーム領域には Windows フォーム コントロールのみを使用できます。 Outlook で設計したフォーム領域をインポートする場合、ネイティブ Outlook コントロールのみを使用できます。

 Outlook UI のさまざまな領域を占有するフォーム領域を作成できます。 たとえば、隣接するフォーム領域をフォームの最初のページの下部に表示し、隣接する各フォーム領域を展開可能にすることができます。 また、完全な追加のフォーム ページとして表示し、既存の標準フォームまたはカスタム フォームに表示できる個別のフォーム領域を追加することもできます。

 詳細については、「[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」を参照してください。

## <a name="controls-on-documents"></a><a name="Controls"></a> 文書のコントロール
 Word 文書と Excel ワークシートには多様なコントロールを追加できます。 たとえば、日付選択カレンダー コントロールを文書に追加して、ユーザーが標準の形式で日付を入力できるようにしたり、データベースにデータを送信するボタンをワークシートに追加したりすることができます。

 Excel または Word のドキュメントレベル プロジェクトを開発する場合、Visual Studio デザイナーを使用し、設計時にプロジェクトの文書またはブックにコントロールを追加できます。また、実行時にプログラムで追加することもできます。 Excel または Word の VSTO アドイン プロジェクトを開発するとき、実行時に開いているドキュメントやブックにこれらのコントロールをプログラミングで追加できます。

 詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」および「[Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)」を参照してください。

## <a name="shortcut-menus"></a><a name="Shortcut"></a> ショートカット メニュー
 ドキュメント ウィンドウやアプリケーション ウィンドウを右クリックすると、ショートカット メニューが表示されます。 ユーザーがドキュメント、ブック、またはホスト コントロールを右クリックするなど、イベントが発生した後に表示されるようにショートカット メニューを設定することができます。 ショートカット メニューには、さまざまなメニュー コマンドやコントロールを追加できます。 ショートカット メニューを作成するには、XML を使用します。 Office プロジェクトに **リボン (XML)** 項目を追加する場合、XML をリボン XML ファイルに追加してショートカット メニューを作成することができます。 XML を使用してショートカット メニューを作成する方法については、「[方法: ショートカット メニューにコマンドを追加する](../vsto/how-to-add-commands-to-shortcut-menus.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [Office ソリューションで WPF コントロールを使用する](../vsto/using-wpf-controls-in-office-solutions.md)
- [方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)
- [方法: アドインのユーザー インターフェイス エラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)
- [チュートリアル : Windows フォームを使用してデータを収集する](../vsto/walkthrough-collecting-data-using-a-windows-form.md)
