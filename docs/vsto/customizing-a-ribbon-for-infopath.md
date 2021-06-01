---
title: InfoPath のリボンのカスタマイズ
description: Microsoft Office InfoPath でリボンをカスタマイズする場合に、カスタム リボンをアプリケーションのどこに表示するかを検討する必要があることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- InfoPath [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5af7c4ed2f396c5a806cc42c49c8f4209b6b5c2c
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828138"
---
# <a name="customize-a-ribbon-for-infopath"></a>InfoPath のリボンのカスタマイズ
  Microsoft Office InfoPath でリボンをカスタマイズする場合、アプリケーションのどこにカスタム リボンを表示するかを検討する必要があります。 [!INCLUDE[InfoPath_14_short](../vsto/includes/infopath-14-short-md.md)] では、次の 3 種類の InfoPath アプリケーション ウィンドウにリボンを表示できます。

- デザイン モードで開くフォーム テンプレートを表示するウィンドウ。

- フォーム テンプレートを基にしたフォームを表示するウィンドウ。

- [印刷プレビュー] ウィンドウ。

  **対象:** このトピックの情報は、InfoPath 2010 の VSTO アドインのプロジェクトに適用されます。 詳細については、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

  ユーザーとデザイナーは、フォーム テンプレートをデザイン モードで開き、テンプレートの外観とレイアウトを変更します。 ユーザーは、フォーム テンプレートを基にしたフォームを開き、コンテンツを追加します。

  [印刷プレビュー] ウィンドウでは、デザイナーとユーザーがフォームまたはフォーム テンプレートを印刷前にプレビューできます。

> [!NOTE]
> [印刷プレビュー] ウィンドウには **[アドイン]** タブは表示されません。 [印刷プレビュー] ウィンドウにカスタム タブを表示する場合は、タブの **OfficeId** プロパティが **TabAddIns** に設定されていないことを確認してください。

 リボンを表示する各ウィンドウのリボンの種類を指定する必要があります。

## <a name="specify-the-ribbon-type-in-the-ribbon-designer"></a>リボン デザイナーでリボンの種類を指定する
 **リボン (ビジュアル デザイナー)** 項目を使用する場合は、 **[プロパティ]** ウィンドウでリボンの **RibbonType** プロパティをクリックし、次の表に示すリボン ID のいずれかを選択します。

|リボン ID|プロジェクトの実行時にリボンが表示されるウィンドウ|
|---------------|---------------------------------------------------------------------|
|**Microsoft.InfoPath.Designer**|デザイン モードで開くフォーム テンプレートを表示するウィンドウ。|
|**Microsoft.InfoPath.Editor**|フォーム テンプレートを基にしたフォームを表示するウィンドウ。|
|**Microsoft.InfoPath.PrintPreview**|[印刷プレビュー] ウィンドウ。|

 1 つのプロジェクトに複数のリボンを追加することができます。 複数のリボンで 1 つのリボン ID を共有する場合は、プロジェクトの `ThisAddin` クラスの `CreateRibbonExtensibilityObject` メソッドをオーバーライドし、実行時に表示するリボンを指定します。 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>リボン XML を使用してリボンの種類を指定する
 **リボン (XML)** 項目を使用する場合は、<xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> メソッドの *ribbonID* パラメーターの値を調べて、適切なリボンを返します。

 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> メソッドは、Visual Studio によってリボン コード ファイルに自動的に生成されます。 *ribbonID* パラメーターは、開いている InfoPath ウィンドウの種類を識別する文字列です。

 デザイン モードでフォーム テンプレートを表示するウィンドウにのみカスタム リボンを表示する方法を次のコード例に示します。 表示するリボンは、リボン クラスで生成される `GetResourceText()` メソッドで指定します。 リボン クラスの詳細については、「 [Ribbon XML](../vsto/ribbon-xml.md)」を参照してください。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/myinfopathproject/ribbon.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/myinfopathproject/ribbon.vb" id="Snippet1":::

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
