---
title: Ribbon XML
description: リボン (ビジュアル デザイナー) 項目ではサポートされていない方法でリボンをカスタマイズする場合に、リボン (XML) 項目を使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.Ribbon.RibbonXMLItem
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- callback methods
- custom Ribbon, displaying
- custom Ribbon, defining behavior
- XML [Office development in Visual Studio], Ribbon
- customizing the Ribbon, defining behavior
- Ribbon [Office development in Visual Studio], customizing
- customizing the Ribbon, displaying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a84a0c21bba42263e7b4dad9ad9118f462389ad6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827501"
---
# <a name="ribbon-xml"></a>Ribbon XML
  リボン (XML) 項目では XML を使用してリボンをカスタマイズできます。 リボン (ビジュアル デザイナー) 項目ではサポートされていない方法でリボンをカスタマイズする場合は、リボン (XML) 項目を使用します。 各項目で実行できる操作の比較については、「[リボンの概要](../vsto/Ribbon-overview.md)」をご覧ください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="add-a-ribbon-xml-item-to-a-project"></a>リボン (XML) 項目をプロジェクトに追加する
 **[新しい項目の追加]** ダイアログ ボックスから、 **リボン (XML)** 項目を任意の Office プロジェクトに追加できます。 Visual Studio によってプロジェクトに次のファイルが自動的に追加されます。

- リボン XML ファイル。 このファイルは、リボン ユーザー インターフェイス (UI) を定義します。 タブ、グループ、およびコントロールなどの UI 要素を追加するには、このファイルを使用します。 詳細については、このトピックで後述する「[リボン XML ファイル リファレンス](#RibbonDescriptorFile)」を参照してください。

- リボン コード ファイル。 このファイルには *リボン クラス* が含まれています。 このクラスの名前は、 **[新しい項目の追加]** ダイアログ ボックスで **リボン (XML)** 項目に指定した名前になります。 Microsoft Office アプリケーションでは、このクラスのインスタンスを使用して、カスタム リボンを読み込みます。 詳細については、このトピックで後述する「[リボン クラスのリファレンス](#RibbonExtensionClass)」を参照してください。

  既定では、これらのファイルによって、カスタム グループがリボンの **[アドイン]** タブに追加されます。

## <a name="display-the-custom-ribbon-in-a-microsoft-office-application"></a>Microsoft Office アプリケーションでカスタム リボンを表示する
 **リボン (XML)** 項目をプロジェクトに追加した後に、`CreateRibbonExtensibilityObject` メソッドをオーバーライドし Office アプリケーションにリボン XML クラスを返すコードを **ThisAddin**、**ThisWorkbook**、または **ThisDocument** クラスに追加する必要があります。

 次のコード例は `CreateRibbonExtensibilityObject` メソッドをオーバーライドして、MyRibbon という名前のリボン XML クラスを返します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb" id="Snippet1":::

## <a name="define-the-behavior-of-the-custom-ribbon"></a>カスタムのリボンの動作を定義する
 *コールバック メソッド* を作成することで、リボン上のボタンのクリックなどのユーザー操作に応答できます。 コールバック メソッドは Windows フォーム コントロールのイベントと似ていますが、UI 要素の XML の属性によって識別されます。 リボン クラスでメソッドを記述すると、コントロールは属性値と同じ名前を持つメソッドを呼び出します。 たとえば、ユーザーがリボン上のボタンをクリックしたときに呼び出されるコールバック メソッドを作成できます。 コールバック メソッドを作成するには、2 つの手順が必要です。

- コード内のコールバック メソッドを識別するリボン XML ファイル内のコントロールに、属性を割り当てます。

- リボン クラスでコールバック メソッドを定義します。

> [!NOTE]
> Outlook では追加の手順が必要です。 詳細については、「[Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)」を参照してください。

 リボンからアプリケーションを自動化する方法を示すチュートリアルについては、「[チュートリアル : リボン XML を使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)」をご覧ください。

### <a name="assign-callback-methods-to-controls"></a>コントロールにコールバック メソッドを割り当てる
 コールバック メソッドをリボン XML ファイル内のコントロールに割り当てるには、コールバック メソッドの種類とメソッドの名前を指定する属性を追加します。 たとえば、次の要素は **OnToggleButton1** という名前の `OnToggleButton1`」をご覧ください。

```xml
<toggleButton id="toggleButton1" onAction="OnToggleButton1" />
```

 **onAction** は、特定のコントロールに関連付けられている主なタスクをユーザーが実行すると呼び出されます。 たとえば、トグル ボタンの **onAction** コールバック メソッドは、ユーザーがボタンをクリックするとが呼び出されます。

 属性で指定するメソッドは、どんな名前をつけてもかまいません。 ただし、その名前はリボンのコード ファイルで定義するメソッドの名前と一致する必要があります。

 リボン コントロールに割り当てることができるコールバック メソッドにはさまざまな種類があります。 各コントロールの使用可能なコールバック メソッドの完全な一覧については、[開発者向けの Office (2007) リボンのユーザー インターフェイスをカスタマイズする (パート 3/3)](/previous-versions/office/developer/office-2007/aa722523(v=office.12)) に関する技術記事を参照してください。

### <a name="define-callback-methods"></a><a name="CallBackMethods"></a> コールバック メソッドを定義する
 リボン クラスのコールバック メソッドはリボン コード ファイルで定義します。 コールバック メソッドにはいくつかの要件があります。

- コールバック メソッドはパブリック メソッドとして宣言されなければなりません。

- コールバック メソッドの名前は、リボン XML ファイル内のコントロールに割り当てたコールバック メソッドの名前と一致する必要があります。

- コールバック メソッドのシグネチャは、関連付けられているリボン コントロールの利用可能なコールバック メソッドの型のシグネチャと一致する必要があります。

  リボン コントロールのコールバック メソッドのシグネチャの完全な一覧については、[開発者向けの Office (2007) リボンのユーザー インターフェイスをカスタマイズする (パート 3/3)](/previous-versions/office/developer/office-2007/aa722523(v=office.12)) に関する技術記事を参照してください。 Visual Studio では、リボン コード ファイルで作成するコールバック メソッドの IntelliSense サポートは提供されていません。 有効なシグネチャに一致しないコールバック メソッドを作成した場合、コードはコンパイルされますが、ユーザーがコントロールをクリックしても、何も起こりません。

  すべてのコールバック メソッドには、メソッドを呼び出すコントロールを表す <xref:Microsoft.Office.Core.IRibbonControl> パラメーターがあります。 このパラメーターを使用して、同じコールバック メソッドを複数のコントロールで再利用できます。 次のコード例は、ユーザーがクリックするコントロールに応じて異なるタスクを実行する **onAction** コールバック メソッドを示しています。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs" id="Snippet2":::
  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb" id="Snippet2":::

## <a name="ribbon-xml-file-reference"></a><a name="RibbonDescriptorFile"></a> リボン XML ファイル リファレンス
 リボン XML ファイルに要素と属性を追加することにより、カスタム リボンを定義できます。 既定では、リボン XML ファイルには次の XML が含まれています。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<customUI xmlns="http://schemas.microsoft.com/office/2006/01/customui" onLoad="OnLoad">
  <ribbon>
    <tabs>
      <tab idMso="TabAddIns">
        <group id="MyGroup"
               label="My Group">
        </group>
      </tab>
    </tabs>
  </ribbon>
</customUI>
```

 次の表は、リボン XML ファイルの既定の要素について説明しています。

|要素|説明|
|-------------|-----------------|
|**customUI**|VSTO アドイン プロジェクトのカスタム リボンを表します。|
|**ribbon**|リボンを表します。|
|**タブ**|[リボン] タブのセットを表します。|
|**タブ**|単独の [リボン] タブを表します。|
|**group**|[リボン] タブのコントロールのグループを表します。|

 これらの要素には、カスタム リボンの外観と動作を指定する属性があります。 次の表は、リボン XML ファイルの既定の属性について説明しています。

|属性|親要素|説明|
|---------------|--------------------|-----------------|
|**onLoad**|**customUI**|アプリケーションでリボンを読み込むときに呼び出されるメソッドを識別します。|
|**idMso**|**タブ**|リボンに表示する組み込みタブを識別します。|
|**id**|**group**|グループを識別します。|
|**label**|**group**|グループに表示するテキストを指定します。|

 リボン XML ファイルの既定の要素と属性は、使用できる要素と属性の小さなサブセットです。 使用可能な要素と属性の完全な一覧については、[開発者向けの Office (2007) リボンのユーザー インターフェイスをカスタマイズする (パート 2/3)](/previous-versions/office/developer/office-2007/aa338199(v=office.12)) に関する技術記事を参照してください。

## <a name="ribbon-class-reference"></a><a name="RibbonExtensionClass"></a> リボン クラスのリファレンス
 Visual Studio は、リボン コード ファイルにリボン クラスを生成します。 このクラスに、リボン上のコントロールのコールバック メソッドを追加します。 このクラスは、 <xref:Microsoft.Office.Core.IRibbonExtensibility> インターフェイスを実装します。

 次の表はこのクラスの既定のメソッドについて説明しています。

|メソッド|説明|
|------------|-----------------|
|`GetCustomUI`|リボン XML ファイルの内容を返します。 Microsoft Office アプリケーションではこのメソッドを呼び出して、カスタム リボンのユーザー インターフェイスを定義する XML 文字列を取得します。 このメソッドは、 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> メソッドを実装します。 **注:** `GetCustomUI` は、リボン XML ファイルの内容を返すためだけに実装する必要があります。VSTO アドインを初期化するために使用してはいけません。 具体的には、 `GetCustomUI` の実装で、ダイアログ ボックスや他のウィンドウを表示しようとしてはいけません。 それ以外の場合は、カスタム リボンが正しく動作しない可能性があります。 VSTO アドインを初期化するコードを実行する必要がある場合は、そのコードを `ThisAddIn_Startup` イベント ハンドラーに追加します。|
|`OnLoad`|<xref:Microsoft.Office.Core.IRibbonControl> パラメーターを `Ribbon` フィールドに割り当てます。 Microsoft Office アプリケーションでは、カスタム リボンが読み込まれるときに、このメソッドを呼び出します。 このフィールドを使用すると、カスタム リボンを動的に更新することができます。 詳細については、[開発者向けの Office (2007) リボンのユーザー インターフェイスをカスタマイズする (パート 1/3)](/previous-versions/office/developer/office-2007/aa338202(v=office.12)) に関する技術記事を参照してください。|
|`GetResourceText`|`GetCustomUI` メソッドによって呼び出され、リボン XML ファイルの内容を取得します。|

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [チュートリアル : リボン XML を使用してカスタム タブを作成する](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
