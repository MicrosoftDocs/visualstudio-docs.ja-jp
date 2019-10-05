---
title: Outlook のリボンのカスタマイズ
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 646192baa6caaa33410b1dd8d17d1983f7d27e30
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71255549"
---
# <a name="customize-a-ribbon-for-outlook"></a>Outlook のリボンのカスタマイズ
  Microsoft Office Outlook でリボンをカスタマイズする場合、アプリケーションのどこにカスタム リボンを表示するかを検討する必要があります。 Outlook によりメイン アプリケーション ユーザー インターフェイス (UI) にリボンが表示されます。また、ユーザーが電子メール メッセージの作成など、特定のタスクを実行すると、ウィンドウが開いてリボンが表示されます。 これらのアプリケーション ウィンドウをインスペクターと呼びます。

 ![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク")関連のビデオデモについて[は、操作方法を参照してください。リボンデザイナーを使用して Outlook のリボンをカスタマイズしますか?](http://go.microsoft.com/fwlink/?LinkID=130312).

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-a-custom-ribbon-to-the-main-application-ui"></a>メインアプリケーション UI にカスタムリボンを追加する
 Outlook のメインのアプリケーション UI は、エクスプローラーと呼ばれます。 **リボン (ビジュアルデザイナー)** 項目を使用している場合は、 **[プロパティ]** ウィンドウでリボンの **[ribbontype]** プロパティをクリックし、 **[Microsoft]** を選択して、エクスプローラーにリボンを追加できます。

## <a name="assign-a-ribbon-to-an-inspector"></a>インスペクターへのリボンの割り当て
 インスペクターのメッセージ クラスに対応するリボンの種類を指定することによって、カスタマイズするインスペクターを指定します。

 **リボン (ビジュアルデザイナー)** 項目を使用している場合は、 **[プロパティ]** ウィンドウでリボンの **[ribbontype]** プロパティをクリックし、値の一覧から1つまたは複数のリボン id を選択します。

 1 つのプロジェクトに複数のリボンを追加することができます。 複数のリボンで 1 つのリボン ID を共有する場合は、プロジェクトの `ThisAddin` クラスの `CreateRibbonExtensibilityObject` メソッドをオーバーライドし、実行時に表示するリボンを指定します。 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。 各リボンの種類の詳細については、技術記事「 [Outlook 2007 でのリボンのカスタマイズ](/previous-versions/office/developer/office-2007/bb226712(v=office.12))」を参照してください。

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>リボン XML を使用してリボンの種類を指定する
 **リボン (XML)** 項目を使用している場合は、 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A>メソッドの*ribbonid*パラメーターの値を確認し、適切なリボンを返します。

 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> メソッドは、Visual Studio によってリボン コード ファイルに自動的に生成されます。 *Ribbonid*パラメーターは、エクスプローラーまたは特定の種類のインスペクターを識別する文字列です。 *Ribbonid*パラメーターの有効な値の完全な一覧については、技術記事「 [Outlook 2007 でのリボンのカスタマイズ](/previous-versions/office/developer/office-2007/bb226712(v=office.12))」を参照してください。

 次のコード例は、`Microsoft.Outlook.Mail.Compose` インスペクターにのみカスタム リボンを表示する方法を示しています。 これは、ユーザーが新しい電子メール メッセージを作成するときに表示されるインスペクターです。 表示するリボンは、**リボン**クラスで`GetResourceText()`生成されるメソッドで指定されます。 **リボン**クラスの詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。

 [!code-csharp[Trin_RibbonOutlookBasic#1](../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs#1)]
 [!code-vb[Trin_RibbonOutlookBasic#1](../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb#1)]

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボンデザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
