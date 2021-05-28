---
title: 'チュートリアル: Outlook フォーム領域のデザイン'
description: 連絡先アイテムのインスペクター ウィンドウに新しいページとして表示する、カスタムの Microsoft Outlook フォーム領域をデザインする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 80c574799029f3fe8c4769d852886a625ffd93aa
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824282"
---
# <a name="walkthrough-design-an-outlook-form-region"></a>チュートリアル: Outlook フォーム領域のデザイン
  カスタム フォーム領域は、標準またはカスタムの Microsoft Office Outlook フォームを拡張します。 このチュートリアルでは、連絡先アイテムのインスペクター ウィンドウに新しいページとして表示するカスタム フォーム領域をデザインします。 このフォーム領域では、アドレス情報を Windows Live Local Search の Web サイトに送信することによって、連絡先に設定された個々の住所の地図を表示します。 フォーム領域について詳しくは、「[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」をご覧ください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 このチュートリアルでは、次の作業について説明します。

- 新しい Outlook VSTO アドイン プロジェクトの作成。

- VSTO アドイン プロジェクトへのフォーム領域の追加。

- フォーム領域のレイアウトのデザイン。

- フォーム領域の動作のカスタマイズ。

- Outlook フォーム領域のテスト。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)] 以降。

  ![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク") このトピックのビデオ版については、「[ビデオ デモ: Outlook フォーム領域のデザイン](/previous-versions/visualstudio/visual-studio-2008/cc837160(v=vs.90))」をご覧ください。

## <a name="create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成する
 まず、基本的な VSTO アドイン プロジェクトを作成します。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>新しい Outlook VSTO アドイン プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、**MapItAddIn** という名前の Outlook VSTO アドイン プロジェクトを作成します。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。

3. プロジェクトを任意のディレクトリに保存します。

     詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

## <a name="add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Outlook VSTO アドイン プロジェクトにフォーム領域を追加する
 Outlook VSTO アドイン ソリューションには、1 つ以上の Outlook フォーム領域アイテムを格納できます。 プロジェクトにフォーム領域アイテムを追加するには、**新しい Outlook フォーム領域** ウィザードを使用します。

### <a name="to-add-a-form-region-to-the-outlook-vsto-add-in-project"></a>Outlook VSTO アドイン プロジェクトにフォーム領域を追加するには

1. **ソリューション エクスプローラー** で、**MapItAddIn** プロジェクトを選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[Outlook フォーム領域]** を選択し、ファイルに **MapIt** という名前を付けて **[追加]** をクリックします。

     **新しい Outlook フォーム領域** ウィザードが起動します。

4. **[フォーム領域を作成する方法の選択]** ページで **[新しいフォーム領域のデザイン]** をクリックし、 **[次へ]** をクリックします。

5. **[作成するフォーム領域の種類を選択します]** ページで **[分離]** をクリックし、 **[次へ]** をクリックします。

     *分離* フォーム領域によって、Outlook フォームに新しいページが追加されます。 フォーム領域の種類の詳細については、「[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)」を参照してください。

6. **[説明用のテキストを指定し、表示設定を選択します]** ページで、 **[名前]** ボックスに「**Map It**」と入力します。

     この名前は、連絡先アイテムを開いたときにインスペクター ウィンドウのリボンに表示されます。

7. **[作成モードのインスペクター]** と **[開封モードのインスペクター]** を選択し、 **[次へ]** をクリックします。

8. **[このフォーム領域を表示するメッセージ クラスを識別します]** ページで、 **[メール メッセージ]** をオフにし、 **[連絡先]** をオンにして、 **[完了]** をクリックします。

     *MapIt.cs* または *MapIt.vb* ファイルがプロジェクトに追加されます。

## <a name="design-the-layout-of-the-form-region"></a>フォーム領域のレイアウトをデザインする
 *フォーム領域デザイナー* を使用してフォーム領域を視覚的に作成します。 フォーム領域デザイナーの画面にマネージド コントロールをドラッグできます。 デザイナーと **プロパティ** ウィンドウを使用して、コントロールのレイアウトと外観を調整します。

### <a name="to-design-the-layout-of-the-form-region"></a>フォーム領域のレイアウトをデザインするには

1. **ソリューション エクスプローラー** で、**MapItAddIn** プロジェクトを展開し、*MapIt.cs* または *MapIt.vb* をダブルクリックしてフォーム領域デザイナーを開きます。

2. デザイナーを右クリックし、 **[プロパティ]** をクリックします。

3. **[プロパティ]** ウィンドウで、 **[サイズ]** を **664, 469** に設定します。

     これにより、フォーム領域が地図を表示するのに十分な大きさになります。

4. **[表示]** メニューの **[ツールボックス]** をクリックします。

5. **ツールボックス** の **[コモン コントロール]** タブから、**WebBrowser** をフォーム領域に追加します。

     **WebBrowser** によって、連絡先に設定されている各住所の地図が表示されます。

## <a name="customize-the-behavior-of-the-form-region"></a>フォーム領域の動作をカスタマイズする
 フォーム領域の実行時の動作をカスタマイズするには、フォーム領域のイベント ハンドラーにコードを追加します。 このフォーム領域に対して、コードは Outlook アイテムのプロパティを調べ、Map It フォーム領域を表示するかどうかを決定します。 フォーム領域を表示する場合、コードは Windows Live Local Search に接続し、Outlook 連絡先アイテムに設定された各住所の地図を読み込みます。

### <a name="to-customize-the-behavior-of-the-form-region"></a>フォーム領域の動作をカスタマイズするには

1. **ソリューション エクスプローラー** で、*MapIt.cs* または *MapIt.vb* を右クリックし、 **[コードの表示]** をクリックします。

    *MapIt.cs* または *MapIt.vb* がコード エディターで開きます。

2. **[フォーム領域ファクトリ]** コード領域を展開します。

    `MapItFactory` という名前のフォーム領域ファクトリ クラスが公開されます。

3. `MapItFactory_FormRegionInitializing` イベント ハンドラーに次のコードを追加します。 このイベント ハンドラーは、ユーザーが連絡先アイテムを開いたときに呼び出されます。 次のコードは、連絡先アイテムに住所が含まれているかどうかを判定します。 連絡先アイテムに住所が含まれていない場合は、このコードが <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> クラスの <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> プロパティを **true** に設定し、フォーム領域は表示されません。 それ以外の場合は、VSTO アドインで <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> イベントが発生し、フォーム領域が表示されます。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet1":::

4. <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> イベント ハンドラーに次のコードを追加します。 このコードは、以下のタスクを実行します。

   - 連絡先アイテムの各住所を連結し、URL 文字列を作成します。

   - <xref:System.Windows.Forms.WebBrowser> オブジェクトの <xref:System.Windows.Forms.WebBrowser.Navigate%2A> メソッドを呼び出し、パラメーターとして URL 文字列を渡します。

     Map It フォーム領域に Local Search の Web サイトが表示され、スクラッチ パッドに各住所が表示されます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb" id="Snippet2":::

## <a name="test-the-outlook-form-region"></a>Outlook フォーム領域をテストする
 プロジェクトを実行すると、Visual Studio によって Outlook が開かれます。 連絡先アイテムを開くと、Map It フォーム領域が表示されます。 Map It フォーム領域は、住所が含まれる連絡先アイテムのフォームのページとして表示されます。

### <a name="to-test-the-map-it-form-region"></a>Map It フォーム領域をテストするには

1. **F5** キーを押してプロジェクトを実行します。

     Outlook が開きます。

2. Outlook の **[ホーム]** タブで、 **[新しいアイテム]** をクリックし、 **[連絡先]** をクリックします。

3. 連絡先フォームで、連絡先の名前を「**Ann Beebe**」と入力し、以下の 3 つの住所を指定します。

    |住所の種類|Address|
    |------------------|-------------|
    |**勤務先**|**4567 Main St. Buffalo, NY**|
    |**Home**|**1234 North St. Buffalo, NY**|
    |**その他**|**3456 Main St. Seattle, WA**|

4. 連絡先アイテムを保存して閉じます。

5. **Ann Beebe** 連絡先アイテムを再度開きます。

    Outlook の **[検索]** グループでこの操作を行うには、連絡先のアドレス帳を開くか、 **[ユーザーの検索]** に「Ann Beebe」と入力します。

6. 連絡先アイテムのリボンの **[表示]** グループで **[Map It]** をクリックし、Map It フォーム領域を開きます。

     Map It フォーム領域が開き、Local Search の Web サイトが表示されます。 スクラッチ パッドに **会社住所**、**自宅住所**、および **その他の住所** が表示されます。 スクラッチ パッドで、地図を表示する住所を選択します。

## <a name="next-steps"></a>次のステップ
 Outlook アプリケーションの UI をカスタマイズする方法の詳細については、次のトピックを参照してください。

- Outlook アイテムのリボンをカスタマイズする方法について詳しくは、「[Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)」をご覧ください。

## <a name="see-also"></a>関連項目
- [実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [チュートリアル : Outlook でデザインしたフォーム領域のインポート](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [方法: フォーム領域を Outlook アドイン プロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [フォーム領域を Outlook メッセージ クラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [Outlook フォーム領域のカスタム動作](../vsto/custom-actions-in-outlook-form-regions.md)
- [方法: Outlook にフォーム領域が表示されないようにする](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
