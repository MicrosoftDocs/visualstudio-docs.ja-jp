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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1e8056eddef6329aeb10ed5545c4146f0af0f167
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96845051"
---
# <a name="how-to-add-a-custom-task-pane-to-an-application"></a>方法: カスタム作業ウィンドウをアプリケーションに追加する
  VSTO アドインを使用して、上記にリストしたアプリケーションにカスタム作業ウィンドウを追加できます。 詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="add-a-custom-task-pane-to-an-application"></a>カスタム作業ウィンドウをアプリケーションに追加する

### <a name="to-add-a-custom-task-pane-to-an-application"></a>カスタム作業ウィンドウをアプリケーションに追加するには

1. 上記のアプリケーションのいずれかの VSTO アドイン プロジェクトを開くか、作成します。 詳細については、「 [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2. **[プロジェクト]** メニューの **[ユーザー コントロールの追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで、新しいユーザーコントロールの名前を **MyUserControl** に変更し、[ **追加**] をクリックします。

     ユーザー コントロールがデザイナーで開きます。

4. **ツールボックス** から1つまたは複数の Windows フォームコントロールをユーザーコントロールに追加します。

5. **ThisAddIn.cs** または **ThisAddIn** コードファイルを開きます。

6. 次のコードを `ThisAddIn` クラスに追加します。 このコードは `MyUserControl` と <xref:Microsoft.Office.Tools.CustomTaskPane> のインスタンスを `ThisAddIn` クラスのメンバーとして宣言します。

     [!code-vb[Trin_TaskPaneBasic#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#1)]
     [!code-csharp[Trin_TaskPaneBasic#1](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#1)]

7. `ThisAddIn_Startup` イベント ハンドラーに次のコードを追加します。 このコードは <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトを `MyUserControl` コレクションに追加することにより、新しい `CustomTaskPanes` を作成します。 コードでは、作業ウィンドウも表示されます。

     [!code-vb[Trin_TaskPaneBasic#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#2)]
     [!code-csharp[Trin_TaskPaneBasic#2](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#2)]

    > [!NOTE]
    > このコードは、カスタム作業ウィンドウをアプリケーションのアクティブ ウィンドウに関連付けます。 一部のアプリケーションでは、他のドキュメントやアプリケーションのアイテムで作業ウィンドウが表示されるように、このコードを変更する場合があります。 詳細については、「 [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [カスタム作業ウィンドウ](../vsto/custom-task-panes.md)
- [チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
