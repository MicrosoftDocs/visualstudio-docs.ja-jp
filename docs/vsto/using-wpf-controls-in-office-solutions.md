---
title: Office ソリューションでの WPF コントロールの使用
description: Windows Presentation Foundation (WPF) コントロールを使用して、Visual Studio でユーザーインターフェイスをデザインする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WPF [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7bc720e6218e4cbb76b14f356d190b738e31ede3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921899"
---
# <a name="use-wpf-controls-in-office-solutions"></a>Office ソリューションでの WPF コントロールの使用

Visual Studio の Office 開発ツールを使用して作成されたソリューションは、Windows フォーム コントロールを使用して直接操作することを前提としていますが、ソリューションで WPF コントロールを使用することもできます。 Windows Presentation Foundation (WPF) は、ユーザー インターフェイスをデザインするときに Windows フォームの代わりとして使用できます。 WPF では、UI、メディア、および文書を取り込むための新しい手法として、Extensible Application Markup Language (XAML) というマークアップ言語を使用します。 詳細については、「 [WPF の概要](/dotnet/framework/wpf/introduction-to-wpf)」を参照してください。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

Office ソリューションの Windows フォーム コントロールをホストする UI 要素は、WPF コントロールもホストできます。 そうした UI 要素には次のようなものがあります。

- ドキュメント レベルのカスタマイズに含まれる文書およびワークシート

- ドキュメント レベルのカスタマイズに含まれる操作ウィンドウ

- VSTO アドインにおけるカスタム作業ウィンドウ

- Outlook 用 VSTO アドインのフォーム領域

## <a name="add-wpf-controls-to-office-projects-at-design-time"></a>デザイン時に Office プロジェクトに WPF コントロールを追加する

Office ソリューションの UI 要素に WPF コントロールを直接追加することはできません。 代わりに、 **ユーザーコントロール (wpf)** 項目をプロジェクトに追加し、wpf コントロールのデザインサーフェイスとして使用します。 次に、WPF ユーザー コントロールをプロジェクトの UI 要素に追加します。

### <a name="to-add-wpf-controls-to-an-actions-pane-custom-task-pane-or-form-region"></a>操作ウィンドウ、カスタム作業ウィンドウ、またはフォーム領域に WPF コントロールを追加するには

1. カスタム作業ウィンドウ、操作ウィンドウ、またはフォーム領域を追加するプロジェクトを開きます。

2. **ユーザーコントロール (WPF)** 項目をプロジェクトに追加します。

3. [ **ツールボックス**] から wpf コントロールを wpf ユーザーコントロールのデザイン画面に追加します。

     既定では、WPF ユーザーコントロールデザイナーが開いている場合、 **ツールボックス** には wpf コントロールのみが含まれます。

4. プロジェクトをビルドします。

5. 操作ウィンドウ、フォーム領域、またはカスタム作業ウィンドウをプロジェクトに追加します。

    - フォーム領域の場合は、 **Outlook フォーム領域** アイテムをプロジェクトに追加します。 詳細については、「 [方法: フォーム領域を Outlook アドインプロジェクトに追加](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)する」を参照してください。

    - 操作ウィンドウの場合は、 **操作ウィンドウコントロール** または **ユーザーコントロール** アイテムをプロジェクトに追加します。 詳細については、「 [方法: Word 文書または Excel ブックに操作ウィンドウを追加](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)する」を参照してください。

    - カスタム作業ウィンドウの場合は、 **ユーザーコントロール** 項目をプロジェクトに追加します。 詳細については、「 [方法: カスタム作業ウィンドウをアプリケーションに追加](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)する」を参照してください。

6. [**ツールボックス**] の [ *ProjectName* **WPF ユーザーコントロール**] タブから、操作ウィンドウ、フォーム領域、またはカスタム作業ウィンドウのデザイナーに WPF ユーザーコントロールをドラッグします。

     UI 要素内の WPF ユーザー コントロールをホストする <xref:System.Windows.Forms.Integration.ElementHost> オブジェクトが自動的に作成されます。

7. プロジェクトをリビルドします。

#### <a name="to-add-wpf-controls-to-a-document-or-worksheet-in-a-document-level-project"></a>ドキュメント レベルのプロジェクト内の文書またはワークシートに WPF コントロールを追加するには

1. Word または Excel のドキュメント レベルのプロジェクトを開きます。

2. **ユーザーコントロール (WPF)** 項目をプロジェクトに追加します。

3. [ **ツールボックス**] から wpf コントロールを wpf ユーザーコントロールのデザイン画面に追加します。

4. プロジェクトをビルドします。

5. **ユーザーコントロール** 項目 (つまり、Windows フォームユーザーコントロール) をプロジェクトに追加します。

6. Windows フォーム ユーザー コントロールのデザイナーを開きます。

7. [**ツールボックス**] の [ *ProjectName* **WPF ユーザーコントロール**] タブから、WPF ユーザーコントロールをデザイナーにドラッグします。

     Windows フォーム ユーザー コントロール内の WPF ユーザー コントロールをホストする <xref:System.Windows.Forms.Integration.ElementHost> オブジェクトが自動的に作成されます。

8. Windows フォーム ユーザー コントロールを文書またはブックにプログラムで追加するコードを作成します。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

    > [!NOTE]
    > Windows フォーム ユーザー コントロールをデザイナー上の文書またはワークシートにドラッグすることはできません。

9. プロジェクトをリビルドします。

## <a name="host-wpf-controls-by-using-the-elementhost-class"></a>コントロールクラスを使用して WPF コントロールをホストする

Visual Studio には Office ソリューションで Windows フォーム コントロールを使用できるようにする機能がありますが、WPF コントロールを対象とする同様の機能はありません。 たとえば、デザイン時に、 **ツールボックス** からコントロールをドラッグして、またはヘルパーメソッドを使用して実行時に、Windows フォームコントロールをドキュメントやワークシートに追加できます。 それに対し、これらの機能は WPF コントロールには使用できません。

WPF コントロールでは、Windows フォーム コントロールまたはフォームと WPF コントロールとの間の統合レイヤーとして <xref:System.Windows.Forms.Integration.ElementHost> クラスを使用します。 デザイン時に WPF コントロールをソリューションに追加すると、<xref:System.Windows.Forms.Integration.ElementHost> オブジェクトが自動的に作成されます。

## <a name="wpf-resources"></a>WPF のリソース

Windows フォーム コントロールおよびフォーム上での WPF のホストに関連するアーキテクチャおよびデザイン上の問題の詳細については、以下のトピックを参照してください。

- [Windows フォームと WPF の相互運用性入力アーキテクチャ](/dotnet/framework/wpf/advanced/windows-forms-and-wpf-interoperability-input-architecture)

- [Windows フォームと WPF プロパティのマッピング](/dotnet/framework/wpf/advanced/windows-forms-and-wpf-property-mapping)

- [WPF と Windows フォームの相互運用](/dotnet/framework/wpf/advanced/wpf-and-windows-forms-interoperation)

- [Windows フォーム コントロールおよび同等の WPF コントロール](/dotnet/framework/wpf/advanced/windows-forms-controls-and-equivalent-wpf-controls)

Visual Studio でデザイン時に WPF コントロールを Windows フォーム コントロールおよびフォームに追加する方法の詳細については、以下のトピックを参照してください。

- [チュートリアル: デザイン時の Windows フォームでの新しい WPF コンテンツの作成](/dotnet/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time)

- [チュートリアル: デザイン時の Windows フォームでの WPF コンテンツの配置](/dotnet/framework/winforms/advanced/walkthrough-arranging-wpf-content-on-windows-forms-at-design-time)

- [チュートリアル: WPF コンテンツのスタイルを適用する](/dotnet/framework/winforms/advanced/walkthrough-styling-wpf-content)

## <a name="see-also"></a>関連項目

- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office ドキュメントのコントロールの Windows フォームの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [方法: カスタム作業ウィンドウをアプリケーションに追加する](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [方法: フォーム領域を Outlook アドインプロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
