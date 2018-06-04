---
title: リボン オブジェクト モデルの概要
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], object model
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2be8f0ecdb4f2d7a8ea379474c4b5ec0062d2b57
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34692962"
---
# <a name="ribbon-object-model-overview"></a>リボン オブジェクト モデルの概要
  [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]を取得し、実行時にリボン コントロールのプロパティを設定に使用できる厳密に型指定のオブジェクト モデルを公開します。 たとえば、メニュー コントロールを動的に設定したり、コントロールの表示/非表示をコンテキストに応じて切り替えたりすることができます。 Office アプリケーションがリボンを読み込む前であれば、タブ、グループ、およびコントロールをリボンに追加することもできます。 詳細については、次を参照してください。[読み取り専用になるプロパティを設定](#SettingReadOnlyProperties)です。  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
 大部分は、このリボン オブジェクト モデル、[リボン クラス](#RibbonClass)、[リボン イベント](#RibbonEvents)、および[リボン コントロール クラス](#RibbonControlClasses)です。  
  
##  <a name="RibbonClass"></a> リボン クラス  
 新しいを追加すると**リボン (ビジュアル デザイナー)** 項目、プロジェクトを Visual Studio は追加、**リボン**をプロジェクトにクラスです。 **リボン**クラスから継承、<xref:Microsoft.Office.Tools.Ribbon.RibbonBase>クラスです。  
  
 このクラスは、リボン コード ファイルとリボン デザイナー コード ファイルを分割する部分クラスとして位置付けられます。  
  
##  <a name="RibbonEvents"></a> リボン イベント  
 **リボン**クラスには、次の 3 つのイベントが含まれています。  
  
|event|説明|  
|-----------|-----------------|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|Office アプリケーションがリボンのカスタマイズを読み込むときに発生します。 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>イベント ハンドラーは、リボン コード ファイルに自動的に追加します。 このイベント ハンドラーを使用して、リボンが読み込まれるときにカスタム コードを実行します。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|リボンが読み込まれるときに、リボンのカスタマイズでイメージをキャッシュできます。 このイベント ハンドラーで、リボンのイメージをキャッシュするコードを記述する場合は、わずかなパフォーマンスの向上を入手できます。 詳細については、「<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage>」を参照してください。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|リボンのインスタンスを閉じるときに発生します。|  
  
##  <a name="RibbonControlClasses"></a> リボン コントロール  
 <xref:Microsoft.Office.Tools.Ribbon>名前空間には、各コントロールに表示される型が含まれています、 **Office リボン コントロール**のグループ、**ツールボックス**です。  
  
 各 `Ribbon` コントロールの型を次の表に示します。 各コントロールの説明は、次を参照してください。[リボンの概要](../vsto/ribbon-overview.md)です。  
  
|コントロール名|クラス名|  
|------------------|----------------|  
|**ボックス**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|  
|**Button**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|  
|**ButtonGroup**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|  
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|  
|**ComboBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|  
|**ドロップダウン リスト**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|  
|**エディット ボックス**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|  
|**ギャラリー**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**グループ**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|  
|**Label**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|  
|**Menu**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|  
|**Separator**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|  
|**SplitButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|  
|**Tab**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|  
|**トグル ボタン**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|  
  
 <xref:Microsoft.Office.Tools.Ribbon> 名前空間では、<xref:System.Windows.Forms> 名前空間に属するコントロール クラスとの名前の衝突を回避するために、型名にプレフィックス "Ribbon" が追加されています。  
  
 リボン デザイナーにコントロールを追加すると、そのコントロールのクラスがリボン デザイナー コード ファイルにフィールドとして宣言されます。  
  
### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>リボン コントロールのプロパティを使用した共通タスク  
 各 `Ribbon` コントロールには、コントロールへのラベルの割り当てやコントロールの表示/非表示の切り替えなど、さまざまなタスクの実行に使用できるプロパティが含まれています。  
  
 場合によっては、プロパティ読み取り専用にリボンが読み込まれた後、または動的メニューにコントロールを追加した後です。 詳細については、次を参照してください。[読み取り専用になるプロパティを設定](#SettingReadOnlyProperties)です。  
  
 `Ribbon` コントロールのプロパティを使用して実行できる一部のタスクについて、次の表で説明します。  
  
|タスク :|方法 :|  
|--------------------|--------------|  
|コントロールの表示/非表示を切り替える。|Visible プロパティを使用します。|  
|コントロールを有効または無効にする。|Enabled プロパティを使用します。|  
|コントロールのサイズを設定する。|ControlSize プロパティを使用します。|  
|コントロールに表示するイメージを取得する。|イメージのプロパティを使用します。|  
|コントロールのラベルを変更する。|ラベルのプロパティを使用します。|  
|ユーザー定義のデータをコントロールに追加する。|Tag プロパティを使用します。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>、<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>、<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> コントロール。|項目プロパティを使用します。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>、<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> のいずれかのコントロールに項目を追加する。|項目プロパティを使用します。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> にコントロールを追加する。|項目プロパティを使用します。<br /><br /> コントロールを追加する、<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>設定する必要があります、リボンが Office アプリケーションに読み込まれた後、<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A>プロパティを**true**リボンが Office アプリケーションに読み込まれる前にします。 詳細については、次を参照してください。[読み取り専用になるプロパティを設定](#SettingReadOnlyProperties)です。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> 内の選択された項目を取得する。<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> または <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|SelectedItem プロパティを使用します。 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> では、<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A> プロパティを使用します。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab> 上のグループを取得する。|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A> プロパティを使用します。|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> に表示する行および列の数を指定する。|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> プロパティおよび <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> プロパティを使用します。|  
  
##  <a name="SettingReadOnlyProperties"></a> 読み取り専用になるプロパティを設定します。  
 リボンが読み込まれる前にのみ設定できるプロパティがあります。 それらのプロパティは次の 3 つの方法で設定できます。  
  
-   Visual Studio で**プロパティ**ウィンドウです。  
  
-   コンス トラクターで、**リボン**クラスです。  
  
-   プロジェクトの `CreateRibbonExtensibilityObject`、`ThisAddin`、または `ThisWorkbook` クラスの `ThisDocument` メソッド  
  
 動的メニューにはいくつかの例外があります。 新しいコントロールを作成、プロパティの設定し追加、実行時に動的メニューにメニューを含むリボンが読み込まれた後にもできます。  
  
 動的メニューに追加するコントロールのプロパティは、いつでも設定できます。  
  
 詳細については、次を参照してください。[読み取り専用になるプロパティ](#ReadOnlyProperties)です。  
  
### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>リボンのコンス トラクターでプロパティを設定  
 プロパティを設定することができます、`Ribbon`のコンス トラクター内のコントロール、**リボン**クラスです。 このコードは、`InitializeComponent` メソッドの呼び出しの後に置く必要があります。 次のコード例は、現在の時刻が太平洋標準時間 (UTC-8) の 17:00 以降である場合に、新しいボタンをグループに追加します。  
  
 次のコードを追加します。  
  
 [!code-csharp[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs#1)]
 [!code-vb[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb#1)]  
  
 Visual c# のプロジェクトで Visual Studio 2008 からアップグレードしたコンス トラクターは、リボン コード ファイルに表示されます。  
  
 Visual Basic プロジェクト、または [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] で作成した Visual C# プロジェクトでは、リボン デザイナー コード ファイルにコンストラクターがあります。 このファイルの名前は*YourRibbonItem*です。Designer.cs または*YourRibbonItem*です。します。 Visual Basic プロジェクトでこのファイルを表示する必要がありますをクリックする、 **すべてのファイル**ソリューション エクスプ ローラーでボタンをクリックします。  
  
### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>CreateRibbonExtensibilityObject メソッドでプロパティを設定  
 プロジェクトの `Ribbon`、`CreateRibbonExtensibilityObject`、または `ThisAddin` のいずれかのクラスの `ThisWorkbook` メソッドをオーバーライドするときに、`ThisDocument` コントロールのプロパティを設定できます。 詳細については、`CreateRibbonExtensibilityObject`メソッドを参照してください[リボンの概要](../vsto/ribbon-overview.md)です。  
  
 次の例では、リボンのプロパティを設定、`CreateRibbonExtensibilityObject`のメソッド、 `ThisWorkbook` Excel ブック プロジェクトのクラスです。  
  
 次のコードを追加します。  
  
 [!code-vb[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb#2)]
 [!code-csharp[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs#2)]  
  
###  <a name="ReadOnlyProperties"></a> 読み取り専用になるプロパティ  
 次の表は、リボンが読み込まれる前にのみ設定できるプロパティを示します。  
  
> [!NOTE]  
>  動的メニューのコントロールのプロパティは、いつでも設定できます。 この場合、次の表の内容は該当しません。  
  
|プロパティ|リボン コントロール クラス|  
|--------------|--------------------------|  
|**BoxStyle**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|  
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|  
|**列数**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**controlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|  
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|  
|**動的**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|  
|**Global**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**グループ**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|  
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|  
|**Itemsize されています。**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|  
|**maxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|  
|**Name**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|  
|**位置**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|  
|**[Ribbontype]**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**行数**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|  
|**SizeString**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|  
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**タブ**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|  
|**タイトル**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|  
  
### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>Outlook インスペクターに表示されるリボンのプロパティを設定  
 ユーザーがリボンを含むインスペクターを開くたびにリボンの新しいインスタンスが作成されます。 ただし、上の表に示すプロパティは、リボンの最初のインスタンスが作成される前にのみ設定できます。 最初のインスタンスが作成されると、そのインスタンスによって Outlook がリボンの読み込みに使用する XML ファイルを定義するため、これらのプロパティは読み取り専用になります。  
  
 リボンの他のインスタンスが作成されたときにこれらのプロパティを別の値に設定する条件ロジックがある場合、そのコードは何の効果ももたらしません。  
  
> [!NOTE]  
>  いることを確認、**名前**Outlook リボンに追加する各コントロールのプロパティを設定します。 実行時に Outlook リボンにコントロールを追加する場合は、コードでこのプロパティを設定する必要があります。 デザイン時にコントロールを Outlook リボンに追加する場合は、Name プロパティが自動的に設定されます。  
  
## <a name="ribbon-control-events"></a>リボン コントロール イベント  
 各コントロール クラスに 1 つ以上のイベントが含まれています。 次の表は、それらのイベントについての説明です。  
  
|event|説明|  
|-----------|-----------------|  
|クリック|コントロールがクリックされたときに発生します。|  
|TextChanged|編集ボックスまたはコンボ ボックス内のテキストが変更されたときに発生します。|  
|ItemsLoading|コントロールの項目のコレクションが Office から要求されたときに発生します。 オフィスのキャッシュ項目のコレクション、コード、コントロールのプロパティを変更するかを呼び出すまで、<xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A>メソッドです。|  
|クリック|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> または <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 内のボタンがクリックされたときに発生します。|  
|SelectionChanged|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> または <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 内の選択項目が変更されたときに発生します。|  
|DialogLauncherClick|グループの右下にあるダイアログ ランチャー アイコンがクリックされたときに発生します。|  
  
 これらのイベントのイベント ハンドラーには、次の 2 つのパラメーターがあります。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*送信者*|イベントを発生させたコントロールを表す <xref:System.Object>。|  
|*e*|<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs> を格納している <xref:Microsoft.Office.Core.IRibbonControl>。 このコントロールを使用すると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって提供されるリボン オブジェクト モデルには用意されていないプロパティにアクセスできます。|  
  
## <a name="see-also"></a>関連項目  
 [実行時にリボンにアクセスします。](../vsto/accessing-the-ribbon-at-run-time.md)   
 [リボンの概要](../vsto/ribbon-overview.md)   
 [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)   
 [リボン デザイナー](../vsto/ribbon-designer.md)   
 [チュートリアル: リボン デザイナーを使用してカスタム タブを作成します。](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)   
 [チュートリアル: 実行時にリボン上のコントロールを更新します。](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)   
 [Outlook のリボンをカスタマイズします。](../vsto/customizing-a-ribbon-for-outlook.md)   
 [方法: 組み込みタブをカスタマイズします。](../vsto/how-to-customize-a-built-in-tab.md)   
 [方法: コントロール、Backstage ビューを追加します。](../vsto/how-to-add-controls-to-the-backstage-view.md)   
 [方法: リボンをリボン デザイナーからリボン XML にエクスポート](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)   
 [方法: アドインの表示は、ユーザー インターフェイス エラー](../vsto/how-to-show-add-in-user-interface-errors.md)  
 