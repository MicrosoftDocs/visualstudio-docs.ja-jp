---
title: '方法: フォーム領域を Outlook アドイン プロジェクトに追加します。'
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.Page1
- VSTO.NewFormRegionWizard.Page3
- VSTO.NewFormRegionWizard.Page2
- VSTO.NewFormRegionWizard.Page0
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], adding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 97d8883ef22fc91b708726fddca60cf757e3d9a8
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56610620"
---
# <a name="how-to-add-a-form-region-to-an-outlook-add-in-project"></a>方法: フォーム領域を Outlook アドイン プロジェクトに追加します。
  **新しい Outlook フォーム領域** ウィザードを使用して、標準またはカスタムの Microsoft Office Outlook フォームを拡張するフォーム領域を作成します。 新しいフォーム領域を作成して Visual Studio でユーザー インターフェイスをデザインするか、または Outlook でデザインしたフォーム領域をインポートして Visual Basic または C# コードを追加することができます。

 別の Outlook プロジェクトで使用した Outlook フォーム領域がある場合は、 **[既存項目の追加]** ダイアログ ボックスを使用して、そのフォーム領域を現在の Outlook VSTO アドイン プロジェクトで再利用できます。 詳細については、[作成の Outlook フォーム領域](../vsto/creating-outlook-form-regions.md)を参照してください。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

### <a name="to-add-a-new-form-region-to-an-outlook-project"></a>新しいフォーム領域を Outlook プロジェクトに追加するには

1.  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]で Outlook VSTO アドイン プロジェクトを開くか、作成します。 詳細については、「[方法 :Visual Studio で Office プロジェクトを作成する方法](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。

2.  **ソリューション エクスプローラー**で Outlook VSTO アドイン プロジェクト ノードを選択します。

3.  **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

4.  **[新しい項目の追加]** ダイアログ ボックスで **[Outlook フォーム領域]** を選択します。

5.  **[名前]** ボックスにフォーム領域の名前を入力してから、 **[追加]** をクリックします。

     **NewOutlook フォーム領域**ウィザードが起動します。

6.  **[フォーム領域を作成する方法を選択します]** ページで、マネージド コントロールをビジュアル デザイナーまでドラッグしてフォーム領域をデザインするか、Outlook でデザインしたフォーム領域からインポートするかを選択します。

    > [!NOTE]
    >  Outlook でデザインしたフォーム領域をインポートするかどうかは、Outlook Form Storage の場所を指定する必要があります (*.ofs*) ファイル。 Outlook でデザインしたフォーム領域にマネージド コントロールを追加することはできません。既存の UI にコードを追加することはできます。 詳細については、[作成の Outlook フォーム領域](../vsto/creating-outlook-form-regions.md)を参照してください。

7.  **[作成するフォーム領域の種類を選択します]** ページでフォーム領域の種類を確認し、種類を 1 つ選択してから、 **[次へ]** をクリックします。 フォーム領域の種類の詳細については、[作成の Outlook フォーム領域](../vsto/creating-outlook-form-regions.md)を参照してください。

8.  **[説明用のテキストを指定し、表示設定を選択します]** ページで、 **[名前]** ボックスにフォーム領域の名前を入力します。 フォーム領域の種類として [置換] および [すべて置換] を選択した場合は、 **[タイトル]** ボックスと **[説明]** ボックスにも入力できます。

     名前、タイトル、および説明フォーム領域を展開するときの Outlook が表示される場所については、[作成の Outlook フォーム領域](../vsto/creating-outlook-form-regions.md)を参照してください。

9. フォーム領域を表示するときの表示モードを 1 つ以上選択します。

     フォーム領域のすべての種類が、作成モード (項目を作成する場合) および開封モード (項目を表示する場合) でインスペクターに表示されることがあります。 さらに、フォーム領域の種類が [隣接]、[置換]、および [すべての置換] の場合も閲覧ウィンドウに表示されることがあります。

10. **[次へ]** をクリックします。

11. **[このフォーム領域を表示するメッセージのクラスを識別します]** ページで、標準の Outlook メッセージ クラスを選択するか、または 1 つ以上のカスタム メッセージ クラスの名前を入力してから、 **[完了]** をクリックします。 詳細については、[フォーム領域を Outlook メッセージ クラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)を参照してください。

## <a name="see-also"></a>関連項目
- [実行時にフォーム領域へのアクセスします。](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook ソリューション](../vsto/outlook-solutions.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域をデザインします。](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [チュートリアル: Outlook でデザインしたフォーム領域をインポートします。](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [Outlook フォーム領域のカスタム アクション](../vsto/custom-actions-in-outlook-form-regions.md)
