---
title: 'チュートリアル: リボン XML を使用してカスタム タブを作成する'
description: リボン (XML) を使用して、[アドイン] タブにボタンを追加し、Microsoft Word を自動化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- customizing the Ribbon, tabscustom Ribbon, tabs
- Ribbon [Office development in Visual Studio], XML
- XML [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Custom tab [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a5d7992462ac3ece9782b0168feedd87577c2d0e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826331"
---
# <a name="walkthrough-create-a-custom-tab-by-using-ribbon-xml"></a>チュートリアル: リボン XML を使用してカスタム タブを作成する
  このチュートリアルでは、**リボン (XML)** 項目を使用してカスタム リボン タブを作成する方法について説明します。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 このチュートリアルでは、次の作業について説明します。

- **[アドイン]** タブへのボタンの追加。 **[アドイン]** タブは、リボン XML ファイルで定義されている既定のタブです。

- **[アドイン]** タブ上のボタンを使用した Microsoft Office Word の自動化。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>プロジェクトを作成する
 まず、Word VSTO アドイン プロジェクトを作成します。 後の手順で、このドキュメントの **[アドイン]** タブをカスタマイズします。

### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには

1. **MyRibbonAddIn** という名前の **Word アドイン** プロジェクトを作成します。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、 **ThisAddIn.cs** コード ファイルまたは **ThisAddIn.vb** コード ファイルが開かれ、 **ソリューション エクスプローラー** に **MyRibbonAddIn** プロジェクトが追加されます。

## <a name="create-the-vsto-add-ins-tab"></a>VSTO アドイン タブを作成する
 **[アドイン]** タブを作成するには、**リボン (XML)** 項目をプロジェクトに追加します。 このチュートリアルの後半で、このタブにボタンを追加します。

### <a name="to-create-the-add-ins-tab"></a>[アドイン] タブを作成するには

1. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

2. **[新しい項目の追加]** ダイアログ ボックスで、 **[リボン (XML)]** をクリックします。

3. 新しいリボンの名前を " **MyRibbon**" に変更し、 **[追加]** をクリックします。

     デザイナーに **MyRibbon.cs** ファイルか **MyRibbon.vb** ファイルが開きます。 **MyRibbon.xml** という名前の XML ファイルもプロジェクトに追加されます。

4. **ソリューション エクスプローラー** で、**ThisAddin.cs** または **ThisAddin.vb** を右クリックし、 **[コードの表示]** をクリックします。

5. 次のコードを **ThisAddin** クラスに追加します。 このコードは、`CreateRibbonExtensibilityObject` メソッドをオーバーライドし、Office アプリケーションにリボン XML クラスを返します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb" id="Snippet1":::

6. **ソリューション エクスプローラー** で、**MyRibbonAddIn** プロジェクトを右クリックし、 **[ビルド]** をクリックします。 プロジェクトのビルドでエラーが発生しないことを確認します。

## <a name="add-buttons-to-the-add-ins-tab"></a>[アドイン] タブにボタンを追加する
 この VSTO アドインの目的は、定型句や特定の表を作業中のドキュメントに追加する手段をユーザーに提供することです。 このユーザー インターフェイスを提供するには、リボン XML ファイルを変更して、2 つのボタンを **[アドイン]** タブに追加します。 このチュートリアルの後半で、これらのボタンのコールバック メソッドを定義します。 リボン XML ファイルの詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。

### <a name="to-add-buttons-to-the-add-ins-tab"></a>[アドイン] タブにボタンを追加するには

1. **ソリューション エクスプローラー** で **MyRibbon.xml** を右クリックし、 **[開く]** をクリックします。

2. **tab** 要素の内容を次の XML に置き換えます。 この XML は、既定のコントロール グループのラベルを **Content** に変更して、**Insert Text** および **Insert Table** というラベルが付いた 2 つのボタンを新しく追加します。

    ```xml
    <tab idMso="TabAddIns">
        <group id="ContentGroup" label="Content">
            <button id="textButton" label="Insert Text"
                 screentip="Text" onAction="OnTextButton"
                 supertip="Inserts text at the cursor location."/>
            <button id="tableButton" label="Insert Table"
                 screentip="Table" onAction="OnTableButton"
                 supertip="Inserts a table at the cursor location."/>
        </group>
    </tab>
    ```

## <a name="automate-the-document-by-using-the-buttons"></a>ボタンを使用してドキュメントを自動化する
 ユーザーが **[Insert Text]** ボタンや **[Insert Table]** ボタンをクリックしたときにアクションが実行されるようにするには、これらのボタンの `onAction` コールバック メソッドを追加する必要があります。 リボン コントロールのコールバック メソッドの詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。

### <a name="to-add-callback-methods-for-the-buttons"></a>ボタンのコールバック メソッドを追加するには

1. **ソリューション エクスプローラー** で **MyRibbon.cs** または **MyRibbon.vb** を右クリックし、 **[開く]** をクリックします。

2. **MyRibbon.cs** ファイルまたは **MyRibbon.vb** ファイルの先頭に次のコードを追加します。  このコードによって、<xref:Microsoft.Office.Interop.Word> 名前空間のエイリアスが作成されます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonButtons/MyRibbon.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonButtons/MyRibbon.vb" id="Snippet1":::

3. `MyRibbon` クラスに次のメソッドを追加します。 これは **[Insert Text]** ボタンのコールバック メソッドで、作業中のドキュメント内のカーソルの現在位置に文字列を追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb" id="Snippet2":::

4. `MyRibbon` クラスに次のメソッドを追加します。 これは **[Insert Table]** ボタンのコールバック メソッドで、作業中のドキュメント内のカーソルの現在位置に表を追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb" id="Snippet3":::

## <a name="testing-the-vsto-add-in"></a>VSTO アドインのテスト
 プロジェクトを実行すると、Word が開き、 **[アドイン]** タブがリボン上に表示されます。 **[アドイン]** タブの **[Insert Text]** ボタンと **[Insert Table]** ボタンをクリックして、コードをテストします。

### <a name="to-test-your-vsto-add-in"></a>VSTO アドインをテストするには

1. **F5** キーを押してプロジェクトを実行します。

2. **[アドイン]** タブがリボンに表示されていることを確認します。

3. **[アドイン]** タブをクリックします。

4. **[Content]** グループがリボンに表示されていることを確認します。

5. **[Content]** グループの **[Insert Text]** ボタンをクリックします。

     ドキュメント内のカーソルの現在位置に文字列が追加されます。

6. **[Content]** グループの **[Insert Table]** ボタンをクリックします。

     ドキュメント内のカーソルの現在位置に表が追加されます。

## <a name="next-steps"></a>次のステップ
 Office UI をカスタマイズする方法の詳細については、次のトピックで説明します。

- 別の Office アプリケーションのリボンをカスタマイズする。 リボンのカスタマイズをサポートするアプリケーションの詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

- リボン デザイナーを使用して Office アプリケーションのリボンをカスタマイズする。 詳細については、「 [Ribbon Designer](../vsto/ribbon-designer.md)」を参照してください。

- カスタム操作ウィンドウを作成する。 詳細については、「[操作ペインの概要](../vsto/actions-pane-overview.md)」を参照してください。

- Outlook フォーム領域を使用して Microsoft Office Outlook の UI をカスタマイズする。 詳細については、「[チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
