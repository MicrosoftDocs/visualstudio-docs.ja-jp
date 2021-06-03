---
title: Office プロジェクトのユーザー補助機能
description: 標準的なユーザー補助の要件を満たすカスタム ソリューションを構築するための多くのユーザー補助機能が、Microsoft Office プロジェクトにどのように含まれているかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, accessibility
- shortcut keys [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], shortcut keys
- accessibility [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4021517aa296f3c1e6355b82260b00590181f4cb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955152"
---
# <a name="accessibility-in-office-projects"></a>Office プロジェクトのユーザー補助機能

Microsoft Visual Studio と Microsoft Office には、標準的なユーザー補助の要件を満たすカスタム ソリューションを構築するためのユーザー補助機能が多数含まれています。 Microsoft では、Web 上のユーザー補助に関するガイドラインを公開しています。 詳しくは、[ユーザー補助の Web サイト](https://www.microsoft.com/accessibility/)をご覧ください。

ほとんどの場合、Visual Studio の Office プロジェクトは、ユーザー補助の標準を満たしているか、ソリューションにアクセスできるように設定できるプロパティを公開しています。 ただし、ユーザー補助が制限されている機能がいくつかあります。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="accessibility-at-design-time"></a>デザイン時のユーザー補助

### <a name="use-shortcut-keys-in-document-level-projects"></a>ドキュメント レベルのプロジェクトでショートカット キーを使用する
 Visual Studio で Microsoft Office Word 文書または Microsoft Office Excel ブックが開いている場合、ショートカット キー コマンドを受け取るアプリケーションは一度に 1 つだけです。 既定では、Visual Studio ではすべてのショートカット キー コマンドを受け取りますが、 **[オプション]** ダイアログ ボックスの **[キーボード設定]** ページで **[ダイナミック キーボード スキーム]** を選択して、ドキュメントにフォーカスがあるときに Word または Excel で受け取るようにすることができます。 詳細については、「[[Microsoft Office Word キーボード] ([オプション] ダイアログ ボックス - [設定])](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)」および「[[Microsoft Office Excel キーボード] ([オプション] ダイアログ ボックス - [設定])](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)」を参照してください。

### <a name="display-shortcut-keys-for-the-ribbon-in-document-level-projects"></a>ドキュメント レベルのプロジェクトでリボンのショートカット キーを表示する
 Visual Studio で Word 文書または Excel ブックが開いている場合は、**Alt** キーを押して、リボン上のタブとコントロールのショートカット キーを表示することはできません。 デザイナーで文書またはブックが開いているときにショートカット キーを表示するには、次の手順を実行します。

#### <a name="to-view-shortcut-keys-for-ribbon-tabs-and-controls-in-the-designer"></a>デザイナーのリボンのタブとコントロールのショートカット キーを表示するには

1. Visual Studio の **[ツール]** メニューで、 **[オプション]** をクリックします。

2. **[Office ツール]** ノードを展開し、必要に応じて **[Microsoft Office Excel キーボード]** または **[Microsoft Office Word キーボード]** を選択します。

3. **[ダイナミック キーボード スキーム]** を選択します。

     変更を有効にするために Visual Studio を再起動する必要があることを示すメッセージが表示されます。

4. **[OK]** をクリックします。

5. Visual Studio を再起動し、プロジェクトを再度開きます。

6. プロジェクトのドキュメントまたはブックのデザイナーを開きます。

7. **F6** キーを押して、リボンのショートカット キーを表示します。

## <a name="accessibility-at-run-time"></a>実行時のユーザー補助

### <a name="windows-forms-controls-on-office-documents"></a>Office ドキュメントでの Windows フォーム コントロール
 Windows フォーム コントロールは、スクリーン リーダーなどのユーザー補助機能のコントロールに関する情報を提供するユーザー補助プロパティを公開します。 ドキュメント レベルのカスタマイズで Office ドキュメントにコントロールがある場合は、これらのユーザー補助プロパティを利用できます。 詳細については、「[Windows フォーム上のコントロールのユーザー補助情報の提供](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)」を参照してください。

 ただし、Windows フォーム コントロールが Excel ブックまたは Word 文書でホストされている場合は、実行時にいくつかのユーザー補助の制限があります。

- 1 つのコントロールから別のコントロールに Tab キーで移動することはできません。

- ドキュメントのコントロールは、ドキュメントのズーム設定を 100% 以外のものに変更すると無効になります。

  ドキュメントの Windows フォーム コントロールの制限事項については、[Office ドキュメントの Windows フォーム コントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)に関するページを参照してください。

### <a name="actions-panes-and-custom-task-panes"></a>操作ウィンドウやカスタム作業ウィンドウ
 操作ウィンドウまたはカスタム作業ウィンドウにフォーカスがある場合は、Windows フォーム アプリケーション上のコントロールにアクセスするのと同じ方法でコントロールにアクセスします。 操作ウィンドウとドキュメントの間でカーソルを移動するには、**F6** キーを押すことができます。

 操作ウィンドウとカスタム作業ウィンドウの詳細については、「[操作ウィンドウの概要](../vsto/actions-pane-overview.md)」および「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

### <a name="display-modes"></a>表示モード

Visual Studio には、表示モードに関連する次の制限事項があります。

- Word 文書または Excel ワークシートのコントロールは、ドキュメントのズーム設定を 100% 以外のものに変更すると無効になります。

- ユーザーがコンピューターのユーザー補助オプションを **[ハイコントラストを使用する]** に変更した場合、 **[新しいプロジェクト]** ダイアログ ボックスにはコントロールが正しく表示されません。

拡大鏡を使用すると、これらの制限に対処できます。 拡大鏡は Windows の表示ユーティリティで、画面の拡大部分を表示する別のウィンドウを作成します。

## <a name="see-also"></a>関連項目

- [Office ソリューションを開発する](../vsto/developing-office-solutions.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [障碍があるユーザーのための機能](../ide/reference/accessibility-features-of-visual-studio.md)
- [Visual Studio のユーザー補助機能](../ide/reference/accessibility-features-of-visual-studio.md)