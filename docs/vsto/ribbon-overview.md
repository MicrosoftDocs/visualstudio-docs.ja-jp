---
title: "リボンの概要"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "office-development"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "カスタム リボン, 複数のリボン"
  - "カスタマイズ (リボンを), 複数のリボン"
  - "リボン [Visual Studio での Office 開発]"
  - "リボン [Visual Studio での Office 開発], リボンの概要"
  - "リボン [Visual Studio での Office 開発], 複数のリボン"
  - "ツール バー [Visual Studio での Office 開発]"
  - "ツール バー [Visual Studio での Office 開発], リボン"
ms.assetid: 2bdef092-190d-47e3-9440-e862b95dacaa
caps.latest.revision: 64
author: "kempb"
ms.author: "kempb"
manager: "ghogen"
caps.handback.revision: 62
---
# リボンの概要
  リボンは、関連するコマンドを見つけやすいように整理するための手段です。  コマンドは、コントロールとしてリボンに表示されます。  コントロールは、アプリケーション ウィンドウの上端に水平に表示されるストリップに、*グループ*ごとに整理されます。  関連するグループは、タブに整理されます。  
  
 旧バージョンの Microsoft Office system でメニューとツールバーを使用してアクセスしていた機能の多くは、現在ではリボンを使用してアクセスできます。  詳細については、技術資料「[2007 Microsoft Office System のユーザー インターフェイスの開発者向け概要](http://go.microsoft.com/fwlink/?LinkID=70860)」を参照してください。  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
## Microsoft Office リボンのカスタマイズ  
 リボンをカスタマイズするには、Office プロジェクトに次のいずれかのリボン項目を追加します。  
  
-   **リボン \(ビジュアルなデザイナー\)**  
  
-   **リボン \(XML\)**  
  
 たとえば、Excel のリボンをカスタマイズするには、Excel VSTO アドイン プロジェクトにリボン項目を追加します。  
  
### リボン \(ビジュアル デザイナー\) 項目  
 **リボン \(ビジュアル デザイナー\)** 項目は、カスタム リボンのデザイン作業と開発作業を容易にするための高度なツールを提供します。  **リボン \(ビジュアル デザイナー\)** 項目を使用すると、次のようにリボンをカスタマイズできます。  
  
-   リボンにカスタム タブまたは組み込みタブを追加します。  
  
-   カスタム タブまたは組み込みタブにカスタム グループを追加します。  
  
    > [!NOTE]  
    >  組み込みタブまたは組み込みグループは、Microsoft Office アプリケーションのリボンにあらかじめ用意されているものです。  たとえば、**\[データ\]** タブは、Excel の組み込みタブです。  **\[接続\]** グループは、**\[データ\]** タブの組み込みのグループです。  
  
-   カスタム コントロールをカスタム グループに追加します。  
  
-   Backstage ビューにカスタム コントロールを追加します。  
  
 **リボン \(ビジュアル デザイナー\)** 項目を使用してリボンをカスタマイズする方法の詳細については、「[リボン デザイナー](../vsto/ribbon-designer.md)」を参照してください。  
  
### リボン \(XML\) 項目  
 **リボン \(ビジュアル デザイナー\)** 項目ではサポートされていない方法でリボンをカスタマイズする場合は、**リボン \(XML\)** 項目を使用します。  **リボン \(XML\)** 項目を使用すると、次のようにリボンをカスタマイズできます。  
  
-   カスタム タブまたは組み込みタブに*組み込み*グループを追加します。  
  
-   組み込みコントロールをカスタム グループに追加します。  
  
-   カスタム コードを追加して、組み込みコントロールのイベント ハンドラーをオーバーライドします。  
  
-   クイック アクセス ツールバーをカスタマイズします。  
  
-   修飾 ID を使用して、VSTO アドイン間でリボンのカスタマイズを共有します。  
  
 **リボン \(XML\)** 項目を使用してリボンをカスタマイズする方法の詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。  
  
## リボン デザイナーからリボン XML へのリボンのエクスポート  
 リボン デザイナーを使用してリボンを作成している場合に、**リボン \(ビジュアル デザイナー\)** 項目ではサポートされていない方法でリボンをカスタマイズするには、リボンを XML にエクスポートします。  
  
 Visual Studio によって自動的に**リボン \(XML\)** 項目が作成され、リボンの各コントロールについて要素と属性のデータがリボン XML ファイルに読み込まれます。  
  
 リボン デザイナーの **\[プロパティ\]** ウィンドウにあるすべてのプロパティがリボン XML ファイルに転送されるわけではありません。  たとえば、Visual Studio では、**Image** プロパティや **Text** プロパティの値はエクスポートされません。  これは、コントロールのイメージを割り当てたり、コントロールのテキストを設定したりするには、エクスポートしたプロジェクトのリボン コード ファイルにコールバック メソッドを作成する必要があるためです。  Visual Studio で、エクスポート プロセスの一部としてコールバック メソッドが自動的に生成されることはありません。  
  
 また、既定値から変更されていないプロパティ値は、結果として得られるリボン XML ファイルには含められません。  
  
 リボンを XML にエクスポートする方法の詳細については、「[方法 : リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)」を参照してください。  
  
### コードの更新  
 新しいリボン コード ファイルが、**ソリューション エクスプローラー**に追加されます。  このファイルにはリボン XML クラスが含まれています。  ボタンのクリックなどのユーザー操作を処理するには、このクラスの `Ribbon Callbacks` 領域にコールバック メソッドを作成する必要があります。  イベント ハンドラーからこれらのコールバック メソッドにコードを移動し、リボン機能拡張 \(RibbonX\) プログラミング モデルで動作するようにコードを変更します。  詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください  
  
 さらに、`ThisAddIn`、`ThisWorkbook`、または `ThisDocument` のいずれかのクラスに、CreateRibbonExtensibilityObject メソッドをオーバーライドして Office アプリケーションにリボン XML クラスを返すコードを追加する必要もあります。  
  
 詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。  
  
## プロジェクトへの複数のリボン項目の追加  
 1 つのプロジェクトに複数のリボン項目を追加することができます。  これは、次の 2 つのタスクのいずれかを実行する場合に便利です。  
  
-   Outlook *インスペクター* にリボンを作成します。  詳細については、「[Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)」を参照してください。  
  
    > [!NOTE]  
    >  インスペクターは、ユーザーが電子メール メッセージを作成するなど、特定のタスクを実行するときに表示されるウィンドウです。  
  
-   実行時に表示するリボンを選択します。  
  
### 実行時に表示するリボンの選択  
 1 つのプロジェクトに複数のリボンを含めることができるため、実行時に表示するリボンを選択できます。  
  
 実行時に表示するリボンを選択するには、プロジェクトの `ThisAddin`、`ThisWorkbook`、`ThisDocument` のいずれかのクラスの CreateRibbonExtensibilityObject メソッドをオーバーライドし、表示するリボンを返します。  次の例では、`myCondition` というフィールドの値をチェックし、適切なリボンを返します。  
  
> [!NOTE]  
>  この例で使用している構文では、**リボン \(ビジュアル デザイナー\)** 項目を使用して作成したリボンが返されます。  **リボン \(XML\)** 項目を使用して作成したリボンを返す構文は、少し違いがあります。  **リボン \(XML\)** 項目を返す場合の詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。  
  
 次のコードを追加します。  
  
 [!code-csharp[Trin_Ribbon_Choose_Ribbon#1](../snippets/csharp/VS_Snippets_OfficeSP/Trin_Ribbon_Choose_Ribbon/CS/ThisWorkbook.cs#1)]
 [!code-vb[Trin_Ribbon_Choose_Ribbon#1](../snippets/visualbasic/VS_Snippets_OfficeSP/Trin_Ribbon_Choose_Ribbon/VB/ThisWorkbook.vb#1)]  
  
### 関連トピック  
  
|タイトル|説明|  
|----------|--------|  
|[方法 : リボンのカスタマイズの概要](../vsto/how-to-get-started-customizing-the-ribbon.md)|Microsoft Office アプリケーションのリボンをカスタマイズし、**リボン \(ビジュアル デザイナー\) 項目**または**リボン \(XML\)** 項目を Office プロジェクトに追加する方法について説明します。|  
|[リボン デザイナー](../vsto/ribbon-designer.md)|リボン デザイナーを使用して、Microsoft Office アプリケーションのリボンに、カスタムのタブ、グループ、およびコントロールを追加する方法について説明します。|  
|[チュートリアル : リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|リボン デザイナーを使用してカスタム リボン タブを作成する方法について説明します。  リボン デザイナーを使用すると、カスタム タブにコントロールを追加し、位置を設定することができます。|  
|[リボン オブジェクト モデルの概要](../vsto/ribbon-object-model-overview.md)|実行時にリボン コントロールのプロパティを取得および設定するために使用できる厳密に型指定されたオブジェクト モデルの概要について説明します。|  
|[チュートリアル : 実行時のリボン コントロールの更新](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)|Office アプリケーションにリボンを読み込んだ後に、リボン オブジェクト モデルを使用してリボン上のコントロールを更新する方法を説明します。|  
|[Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)|Microsoft Office Outlook のリボンをカスタマイズするためのガイダンスを提供します。|  
|[InfoPath のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-infopath.md)|Microsoft Office InfoPath のリボンをカスタマイズするためのガイダンスを提供します。|  
|[実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)|リボンを表示\/非表示にしたり、変更を加えたり、ユーザーがコードをカスタム作業ウィンドウ、操作ウィンドウ、または Outlook フォーム領域のコントロールから実行できるようにしたりする方法について説明します。|  
|[方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)|リボン上のタブの順序を変更する方法について説明します。|  
|[方法 : 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)|組み込みタブにグループやコントロールを追加する方法について説明します。|  
|[方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)|**\[ファイル\]** をクリックしたときに表示されるメニューにコントロールを追加する方法について説明します。|  
|[方法 : リボン グループにダイアログ ボックス起動ツールを追加する](../vsto/how-to-add-a-dialog-box-launcher-to-a-ribbon-group.md)|リボン上の任意のグループにダイアログ ボックス起動ツールを追加する方法について説明します。|  
|[方法 : リボンをリボン デザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)|リボンをデザイナーからリボン XML にエクスポートし、高度な方法でリボンをカスタマイズする方法について説明します。|  
|[リボン XML](../vsto/ribbon-xml.md)|リボン XML を使用してリボンをカスタマイズする方法について説明します。|  
|[チュートリアル : リボン デザイナーを使用したカスタム タブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)|**リボン \(XML\)** 項目を使用してカスタム リボン タブを作成する方法について説明します。|  
  
  