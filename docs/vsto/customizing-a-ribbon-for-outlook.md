---
title: Outlook のリボンをカスタマイズする
description: Microsoft Office Outlook でリボンをカスタマイズする際には、カスタム リボンがアプリケーションのどこに表示されるかを考慮する必要があります。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Outlook [Office development in Visual Studio], Ribbon
- customizing the Ribbon, about customizing the Ribbon
- custom Ribbon, about customizing the Ribbon
- Ribbon [Office development in Visual Studio], Outlook
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: df28de0f8a9497fabecff816c26db7593bf349bd
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828060"
---
# <a name="customize-a-ribbon-for-outlook"></a>Outlook のリボンをカスタマイズする
  Microsoft Office Outlook でリボンをカスタマイズする場合、アプリケーションのどこにカスタム リボンを表示するかを検討する必要があります。 Outlook によりメイン アプリケーション ユーザー インターフェイス (UI) にリボンが表示されます。また、ユーザーが電子メール メッセージの作成など、特定のタスクを実行すると、ウィンドウが開いてリボンが表示されます。 これらのアプリケーション ウィンドウをインスペクターと呼びます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-a-custom-ribbon-to-the-main-application-ui"></a>カスタム リボンをメイン アプリケーション UI に追加する
 Outlook のメインのアプリケーション UI は、エクスプローラーと呼ばれます。 **リボン (ビジュアル デザイナー)** 項目を使用する場合は、**プロパティ** ウィンドウでリボンの **[RibbonType]** プロパティをクリックした後、 **[Microsoft.Outlook.Explorer]** を選択すると、エクスプローラーにリボンを追加できます。

## <a name="assign-a-ribbon-to-an-inspector"></a>インスペクターにリボンを割り当てる
 インスペクターのメッセージ クラスに対応するリボンの種類を指定することによって、カスタマイズするインスペクターを指定します。

 **リボン (ビジュアル デザイナー)** 項目を使用する場合は、**プロパティ** ウィンドウでリボンの **[RibbonType]** プロパティをクリックし、値の一覧から 1 つ以上のリボン ID を選択します。

 1 つのプロジェクトに複数のリボンを追加することができます。 複数のリボンで 1 つのリボン ID を共有する場合は、プロジェクトの `ThisAddin` クラスの `CreateRibbonExtensibilityObject` メソッドをオーバーライドし、実行時に表示するリボンを指定します。 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。 リボンのそれぞれの種類について詳しくは、技術記事「[Outlook 2007 におけるリボンのカスタマイズ](/previous-versions/office/developer/office-2007/bb226712(v=office.12))」をご覧ください。

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>リボン XML を使用してリボンの種類を指定する
 **リボン (XML)** 項目を使用する場合は、<xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> メソッドの *ribbonID* パラメーターの値を確認して、適切なリボンを返します。

 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> メソッドは、Visual Studio によってリボン コード ファイルに自動的に生成されます。 *ribbonID* パラメーターは、エクスプローラーまたは特定の種類のインスペクターを識別する文字列です。 *ribbonID* パラメーターの有効値の完全な一覧については、技術記事「[Outlook 2007 におけるリボンのカスタマイズ](/previous-versions/office/developer/office-2007/bb226712(v=office.12))」を参照してください。

 次のコード例は、`Microsoft.Outlook.Mail.Compose` インスペクターにのみカスタム リボンを表示する方法を示しています。 これは、ユーザーが新しい電子メール メッセージを作成するときに表示されるインスペクターです。 表示するリボンは、**Ribbon** クラスで生成される `GetResourceText()` メソッドで指定します。 **Ribbon** クラスについて詳しくは、「[リボン XML](../vsto/ribbon-xml.md)」をご覧ください。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb" id="Snippet1":::

## <a name="see-also"></a>こちらもご覧ください
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
