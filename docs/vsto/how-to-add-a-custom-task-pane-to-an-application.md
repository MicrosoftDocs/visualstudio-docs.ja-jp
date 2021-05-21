---
title: '方法: カスタム作業ウィンドウをアプリケーションに追加する'
description: Visual Studio Tools for Office (VSTO) アドインを使用して、カスタム作業ウィンドウをアプリケーションに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], adding to application
- custom task panes [Office development in Visual Studio], adding to application
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d85edb9773783abe6282918c432fc1a4eff83944
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826721"
---
# <a name="how-to-add-a-custom-task-pane-to-an-application"></a>方法: カスタム作業ウィンドウをアプリケーションに追加する
  VSTO アドインを使用して、上記にリストしたアプリケーションにカスタム作業ウィンドウを追加できます。 詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="add-a-custom-task-pane-to-an-application"></a>カスタム作業ウィンドウをアプリケーションに追加する

### <a name="to-add-a-custom-task-pane-to-an-application"></a>カスタム作業ウィンドウをアプリケーションに追加するには

1. 上記のアプリケーションのいずれかの VSTO アドイン プロジェクトを開くか、作成します。 詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで新しいユーザー コントロールの名前を **MyUserControl** に変更し、 **[追加]** をクリックします。

     ユーザー コントロールがデザイナーで開きます。

4. **[ツールボックス]** から 1 つまたは複数の Windows フォーム コントロールをユーザー コントロールに追加します。

5. **ThisAddIn.cs** または **ThisAddIn.vb** コード ファイルを開きます。

6. 次のコードを `ThisAddIn` クラスに追加します。 このコードは `MyUserControl` と <xref:Microsoft.Office.Tools.CustomTaskPane> のインスタンスを `ThisAddIn` クラスのメンバーとして宣言します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs" id="Snippet1":::

7. `ThisAddIn_Startup` イベント ハンドラーに次のコードを追加します。 このコードは <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトを `MyUserControl` コレクションに追加することにより、新しい `CustomTaskPanes` を作成します。 コードでは、作業ウィンドウも表示されます。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs" id="Snippet2":::

    > [!NOTE]
    > このコードは、カスタム作業ウィンドウをアプリケーションのアクティブ ウィンドウに関連付けます。 一部のアプリケーションでは、他のドキュメントやアプリケーションのアイテムで作業ウィンドウが表示されるように、このコードを変更する場合があります。 詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
