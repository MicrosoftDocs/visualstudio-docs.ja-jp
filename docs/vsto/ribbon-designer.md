---
title: リボン デザイナー
description: リボン デザイナーを使用して、Microsoft Office アプリケーションのリボンに、カスタムのタブ、グループ、およびコントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- Designer_Microsoft.VisualStudio.Tools.Office.Ribbon.Design.RibbonDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, about Ribbon Designer
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- customizing the Ribbon, about Ribbon Designer
- Ribbon [Office development in Visual Studio], visual designer
- customizing the Ribbon
- custom Ribbon
- designers [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon [Office development in Visual Studio], common tasks
- Ribbon Designer [Office development in Visual Studio]
- read-only properties
- Ribbon [Office development in Visual Studio], shortcut keys
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 06211bb22ae071132b4cfad67352daa46182d366
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99940918"
---
# <a name="ribbon-designer"></a>リボン デザイナー
  リボン デザイナーは、ビジュアルなデザイン キャンバスです。 リボン デザイナーを使用すると、Microsoft Office アプリケーションのリボンに、カスタムのタブ、グループ、およびコントロールを追加できます。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 リボン デザイナーを開くには、プロジェクトに **リボン (ビジュアル デザイナー)** 項目を追加します。 その後、デザイン ツールを使用して、以下のタスクを実行できます。

- [リボン レイアウトのデザイン](#DesigningRibbonLayout)

- [イベントの処理とコントロール プロパティの設定](#HandleEventsSetProperties)

- [Backstage ビューへのコントロールの追加](#CustomizingMicrosoftOfficeButton)

> [!NOTE]
> リボン デザイナーでは行うことのできないタスクがあります。 これらのタスクとその実行方法の詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

## <a name="add-a-ribbon-visual-designer-item-to-a-project"></a>プロジェクトへのリボン (ビジュアル デザイナー) 項目の追加
 リボン デザイナーを使用するには、プロジェクトに新しい **リボン (ビジュアル デザイナー)** 項目を追加します。 詳細については、「[方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)」を参照してください。

 新しい **リボン (ビジュアル デザイナー)** 項目を追加すると、Visual Studio により、次のファイルがプロジェクトに自動的に追加されます。

- リボン コード ファイル。 このファイルの名前は、 **[新しい項目の追加]** ダイアログ ボックスで **リボン (ビジュアル デザイナー)** 項目に指定した名前になります。 このファイルには、リボンのイベントを処理するコードを追加します。

- リボン デザイナー コード ファイル。 このファイルには、リボン デザイナーによって生成されるコードが格納されます。直接編集することはできません。

- リソース ファイル。 このファイルには、リボンの各コントロールのプロパティ値が格納されます。

  別のプロジェクトに既存の **リボン (ビジュアル デザイナー)** 項目がある場合は、 **[既存項目の追加]** ダイアログ ボックスを使用して、その項目を現在のプロジェクトで再利用できます。

## <a name="design-a-ribbon"></a><a name="DesigningRibbonLayout"></a>リボンのデザイン
 リボン デザイナーを開くには、次の 3 つの方法があります。

- **ソリューション エクスプローラー** でリボン コード ファイルをダブルクリックします。

- **ソリューション エクスプローラー** で、リボン コード ファイルを右クリックしてから、 **[デザイナーの表示]** をクリックします。

- **ソリューション エクスプローラー** でリボン コード ファイルを選択してから、 **[表示]** メニューの **[デザイナー]** をクリックします。

  リボン デザイナーには、既定のタブとグループがあります。 既定のタブとグループは、リボン デザイナーから削除することができます。 既定のグループを削除するには、 **[Group1]** を右クリックしてから、 **[削除]** をクリックします。 既定のタブを削除するには、デザイン サーフェイス上の空の領域を右クリックしてから、 **[リボン タブの削除]** をクリックします。

  リボン デザイナーにカスタム タブ、グループ、およびコントロールを追加することもできます。 これらのコントロールは、**ツールボックス** の **[Office リボン コントロール]** グループに含まれています。 **[Office リボン コントロール]** グループからリボン デザイナーにコントロールを追加するには、次の 3 つの方法があります。

- リボン デザイナーの適切な領域にコントロールをドラッグします。

- コントロールをクリックし、リボン デザイナーの適切な領域をクリックします。

- デザイナーの適切な領域を選択し、**ツールボックス** にあるコントロールをダブルクリックします。

### <a name="ribbon-design-workflow"></a>リボン デザインのワークフロー
 リボンのレイアウトをデザインするときの基本的な手順は次のとおりです。

1. [リボンにカスタム タブを追加します](#AddTabToRibbon)。

2. [タブにグループを追加します](#AddGroupsToTab)。

3. [グループにコントロールを追加します](#AddControlsToGroups)。

   コントロールのドロップ操作を行うことができるのは、グループだけです。タブやリボンに対してコントロールを直接ドラッグすることはできません。 グループのドロップ操作を行うことができるのは、タブだけです。リボンに対してグループを直接ドラッグすることはできません。

   コントロールを正確な位置にドラッグして、配置します。 **[プロパティ]** ウィンドウを使用してコントロールのプロパティを設定することもできます。

   コントロールは、リボン上のタブ間でドラッグすることはできません。 コントロールを別のタブに移動する場合は、 **[切り取り]** コマンドを使用してタブからコントロールを切り取り、別のタブに貼り付ける必要があります。コントロールを切り取って貼り付けると、イベント ハンドラーの動作が停止します。 イベント ハンドラーに再接続するには、 **[プロパティ]** ウィンドウを使用します。 詳細については、「[[プロパティ] ウィンドウ](../ide/reference/properties-window.md)」を参照してください。

### <a name="add-custom-tabs-to-the-ribbon"></a><a name="AddTabToRibbon"></a>リボンにカスタム タブを追加する
 リボンにカスタム タブを追加するには、次の 3 つの方法があります。

- **ツールボックス** からタブを追加します。

- リボン デザイナーを右クリックしてから、 **[リボン タブの追加]** をクリックします。

- **タブ コレクション エディター** を開いてから、 **[追加]** をクリックします。

   **タブ コレクション エディター** を開くには、 **[プロパティ]** ウィンドウで **[タブ]** プロパティを選択してから、省略記号ボタン (![ASP.NET モバイル デザイナーの省略](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

  タブを追加すると、グループを追加してコントロールを含めることができます。

#### <a name="remove-custom-tabs-from-the-ribbon"></a>リボンからカスタム タブを削除する
 リボンからカスタム タブを削除するには、次の 3 つの方法があります。

- デザイナーを右クリックしてから、 **[リボン タブの削除]** をクリックします。

- **[プロパティ]** ウィンドウの **コマンド** ペインで、 **[リボン タブの削除]** をクリックします。

- **タブ コレクション エディター** を開き、タブを選択してから、 **[削除]** をクリックします。

#### <a name="change-the-position-of-a-tab-on-the-ribbon"></a>リボンのタブの位置を変更する
 リボンのカスタム タブの順序を変更できます。 また、リボン上の組み込みタブの前または後ろにカスタム タブを配置することもできます。 詳細については、「[方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)」を参照してください。

#### <a name="customize-built-in-tabs-on-the-ribbon"></a>リボンの組み込みタブをカスタマイズする
 組み込みタブは、Microsoft Office アプリケーションのリボンに初めから含まれているタブです。 たとえば、 **[データ]** タブは、Excel の組み込みタブです。

 組み込みタブには、グループやコントロールを追加できます。既定では、カスタム グループは組み込みタブの最後のグループとして表示されます。ただし、タブ上で組み込みグループの前または後ろにカスタム グループを配置することができます。

 組み込みグループを削除することはできません。

 組み込みタブをカスタマイズする方法の詳細については、「[方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)」を参照してください。

### <a name="add-groups-to-a-tab"></a><a name="AddGroupsToTab"></a>タブにグループを追加する
 グループを使用すると、リボンのコントロールを論理的に整理できます。 タブにグループを追加します。 グループに、他のすべてのコントロールを追加します。

### <a name="add-controls-to-groups"></a><a name="AddControlsToGroups"></a>グループにコントロールを追加する
 グループに 1 つ以上のコントロールを追加します。 各コントロールの説明を次の表に示します。

|Control|説明|
|-------------|-----------------|
|**ボックス**|グループ内のコントロールを整理するコンテナー。 区分線、グループ、タブを除き、任意のコントロールを追加できます。ボックスは水平または垂直にできます。|
|**ボタン**|アクションを起動するボタン。 ボタンは、グループ、ボタン グループ、ドロップダウン リスト、ギャラリ、メニュー、分割ボタンのいずれかに追加できます。|
|**ButtonGroup**|1 つ以上のボタン、トグル ボタン、メニュー、分割ボタン、ギャラリを含むグループ。 ボタン グループは、グループまたはメニューに追加できます。|
|**CheckBox**|オンまたはオフにしてオプションの有効/無効を切り換えるボックス。|
|**ComboBox**|リスト ボックスが付属したエディット ボックス。 ユーザーは、選択内容を入力したり、選択したりできます。 ボックスには、現在の選択項目が表示されます。 実行時に、リボンが Office アプリケーションに読み込まれる前または読み込まれた後に項目の追加や削除を行うには、<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Items%2A> プロパティを使用します。|
|**DropDown**|ユーザーが選択できる項目の一覧。 ユーザーがドロップダウン リストに新しい項目を入力することはできません。<br /><br /> 一覧に項目を追加するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Items%2A> プロパティを使用します。 項目の追加や削除は、実行時に行うことができます。<br /><br /> 一覧にボタンを追加するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Buttons%2A> プロパティを使用します。 ただし、実行時にリボンが Office アプリケーションに読み込まれた後で、ボタンの追加や削除を行うことはできません。|
|**EditBox**|ユーザーがテキストを入力できるボックス。|
|**[ギャラリー]**|ユーザーが選択できる項目を配列やグリッドで視覚的に示すメニュー。 メニューの選択項目のレイアウトを調整できます。 ギャラリの項目やボタンを表示する行や列の数を指定するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> プロパティと <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> プロパティを使用します。|
|**Label**|リボン上のコントロールの識別に使用できるテキスト。|
|**Menu**|ドロップダウン リスト。次のいずれかのコントロールを含めることができます。<br /><br /> -   ボタン<br />-   チェック ボックス<br />-   ギャラリー<br />-   メニュー<br />-   分割ボタン<br />-   トグル ボタン<br />-   区切り記号<br /><br /> リボン デザイナーのメニューにコントロールを追加するには、メニューの下向き矢印をクリックし、メニューのデザイン サーフェイスを開きます。 その後、**ツールボックス** からメニューにリボン コントロールをドラッグできます。 コントロールを並べ替えるには、コントロールを目的の位置にドラッグします。<br /><br /> リボンが Office アプリケーションに読み込まれた後でコントロールを <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> に追加する場合は、リボンが読み込まれる前に <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> プロパティを **true** に設定する必要があります。 この方法については、「[リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)」を参照してください。|
|**Separator**|一覧内の項目を分割するために使用する細いバー。 グループに追加すると、バーは垂直に表示されます。 メニュー追加すると、バーは水平に表示されます。|
|**SplitButton**|メニューが付属したボタン。 以下の任意のコントロールを含めることができます。<br /><br /> -   ボタン<br />-   チェック ボックス<br />-   ギャラリー<br />-   メニュー<br />-   分割ボタン<br />-   トグル ボタン<br />-   区切り記号<br /><br /> メニューと同様に、分割ボタンにも独自のデザイン サーフェイスがあります。 ただし、メニューとは異なり、分割ボタンに含まれる項目を更新できるのは、リボンが Office アプリケーションに読み込まれる前だけです。 分割ボタンに含まれる項目を更新する方法については、「[リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)」を参照してください。|
|**ToggleButton**|押された状態または押されていない状態で表示されるボタン。|

## <a name="handle-events-and-setting-properties"></a><a name="HandleEventsSetProperties"></a>イベントの処理とプロパティの設定
 リボン デザイナーでは、 **[プロパティ]** ウィンドウを使用して、デザイン時にコントロールのプロパティを設定できます。 さらにリボンでは、厳密に型指定されたオブジェクト モデルが公開されます。これを使用して、実行時にリボン コントロールのプロパティを取得し、設定できます。

 デザイナー上の任意のコントロールをダブルクリックすると、そのコントロールの既定のイベントのイベント ハンドラーが開きます。 他のすべてのコントロール イベントのイベント ハンドラーを作成するには、 **[プロパティ]** ウィンドウを使用します。

 リボンのイベントとプロパティは、<xref:Microsoft.Office.Tools.Ribbon> 名前空間に格納されています。 **リボン (ビジュアル デザイナー)** 項目によって、自動的にこのアセンブリへの参照がプロジェクトに追加され、適切な **using** または **Imports** ステートメントがリボン コード ファイルの先頭に挿入されます。

 実行時のリボン イベントの処理およびリボン コントロールのプロパティの設定については、「[リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)」を参照してください。

## <a name="customize-backstage-view"></a><a name="CustomizingMicrosoftOfficeButton"></a>Backstage ビューのカスタマイズ
 リボン デザイナーを使用して、 **[ファイル]** タブをクリックしたときに表示されるメニューにコントロールを追加できます。このメニューは Backstage ビューと呼ばれます。

 リボン デザイナーを使用して、ビルトイン コントロールの前または後ろにコントロールを配置することはできません。 ビルトイン コントロールは、Backstage ビューで既に表示されているコントロールです。 ビルトイン コントロールの前または後ろにコントロールを配置するには、リボン XML を使用する必要があります。 **リボン (XML)** の詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。 Backstage ビューのカスタマイズの詳細については、[開発者向け Office 2010 Backstage ビューの概要](/previous-versions/office/developer/office-2010/ee691833(v=office.14))および[開発者向け Office 2010 Backstage ビューのカスタマイズ](/previous-versions/office/developer/office-2010/ee815851(v=office.14))に関するそれぞれのページを参照してください。

 [!INCLUDE[appliesto_ribbon_2010](../vsto/includes/appliesto-ribbon-2010-md.md)]

 Backstage ビューにコントロールを追加する方法については、「[方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)」を参照してください。

## <a name="accessibility-in-the-ribbon-designer"></a><a name="Accessibility"></a>リボン デザイナーでのユーザー補助
 キーボード ショートカットを使用して、リボン デザイナーのコントロールを移動できます。 キーボード ショートカットには、すべてのコントロールに適用されるものと、メニューを備えたコントロールにのみ適用されるものがあります。

 すべてのコントロールに適用されるキーボード ショートカットを、次の表に示します。

|アクション|ショートカット キー|
|------------|-----------------------|
|一覧内の直前のコントロールの前に、コントロールを移動します。|**Ctrl**+**上**<br /><br /> **Ctrl**+**左**|
|一覧内の次のコントロールの後ろに、コントロールを移動します。|**Ctrl**+**下**<br /><br /> **Ctrl**+**右**|
|コントロールでの選択を、同じグループ内の別のコントロールに移動します。 ドロップダウン パネルの場合は、親コントロールとドロップダウン パネル内のコントロールの間で移動します。|**Up**<br /><br /> **[下へ]**|
|すべてのコントロールを通して前方に進む処理を反復します。|**Tab**|
|すべてのコントロールを通して後方に進む処理を反復します。|**Shift**+**Tab**|
|選択したコントロール (1 つまたは一連のコントロール) を削除します。|**削除**|
|選択したコントロールをコピーします。|**Ctrl**+**C**|
|選択したコントロールを切り取ります。|**Ctrl**+**X**|
|クリップボードからコントロールを貼り付けます。|**Ctrl**+**V**|
|**ツールボックス** を選択します。|**Ctrl**+**Alt**+**X**|
|親コンポーネントを選択します。|**Esc**|

 Microsoft Office メニュー、<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>、および <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> にのみ適用されるキーボード ショートカットを、次の表に示します。

|アクション|ショートカット キー|
|------------|-----------------------|
|ドロップダウン パネルが開いていて、パネル上で選択されているコントロールがある場合は、その親コントロールを選択します。|**Left**|
|ドロップダウン パネルが開いていて、親コントロールが選択されている場合は、ドロップダウン パネルを閉じます。|**Left**|
|ドロップダウン パネルを開きます。|**Right**|
|ドロップダウン パネルが開いている場合は、そのパネルにある最初のコントロールを選択します。|**Right**|
|ドロップダウン パネルを閉じます。|**Esc**|

## <a name="see-also"></a>関連項目

- [リボンの概要](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボン デザイナーを使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [方法: リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
