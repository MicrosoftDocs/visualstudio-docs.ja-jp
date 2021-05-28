---
title: Visual Studio Tools for Office runtime のアセンブリ
description: Visual Studio によって Visual Studio Tools for Office runtime アセンブリへの参照が自動的に追加されることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, assemblies
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 600408231e5085009e5edc546535ca8e5110fc6e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882558"
---
# <a name="assemblies-in-the-visual-studio-tools-for-office-runtime"></a>Visual Studio Tools for Office runtime のアセンブリ
  Office プロジェクトを作成すると、Visual Studio によって、そのプロジェクト タイプとプロジェクトの対象 .NET Framework に使用する [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] アセンブリの参照が自動的に追加されます。 .NET Framework 3.5、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]、 [!INCLUDE[net_v45](includes/net-v45-md.md)]の Office 拡張機能にさまざまなアセンブリがあります。 Office 拡張機能についての詳細は、「[Visual Studio Tools for Office runtime の概要](visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-4-and-the-net_v45"></a>Office 拡張機能に含まれる .NET Framework 4 および [!INCLUDE[net_v45](includes/net-v45-md.md)] 用のアセンブリ
 次の表は、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] と [!INCLUDE[net_v45](includes/net-v45-md.md)]の Office 拡張機能に含まれているアセンブリをまとめたものです。 これらのアセンブリの名前空間と型に関するドキュメントについては、「[マネージド リファレンス &#40;Visual Studio での Office 開発&#41;](managed-reference-office-development-in-visual-studio.md)」を参照してください。

|アセンブリ名|説明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.dll|次の型を提供します。<br /><br /> - リボンのカスタマイズとスマート タグを作成するための型。 **注:** スマート タグは、[!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] および [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] で非推奨になっています。<br />- ドキュメント レベルのカスタマイズの操作ウィンドウと VSTO アドインのカスタム作業ウィンドウを作成するための型。|
|Microsoft.Office.Tools.Excel.dll|Excel プロジェクトのホスト項目とホスト コントロールを表すインターフェイスとサポートする型を提供します。 詳細については、「[拡張オブジェクトを使用して Excel を自動化する](automating-excel-by-using-extended-objects.md)」を参照してください。|
|Microsoft.Office.Tools.Outlook.dll|Outlook VSTO アドインでカスタム フォーム領域の作成に使用できる型を提供します。|
|Microsoft.Office.Tools.Word.dll|Word プロジェクトのホスト項目とホスト コントロールを表すインターフェイスとサポートする型を提供します。 詳細については、「[拡張オブジェクトを使用して Word を自動化する](automating-word-by-using-extended-objects.md)」を参照してください。|
|Microsoft.Office.Tools.v4.0.Framework.dll|次の型を提供します。<br /><br /> - Visual Studio Tools for Office runtime によってスローされる例外。<br />- Outlook フォーム領域の作成時に使用できる属性。|
|Microsoft.Office.Tools.dll|Visual Studio Tools for Office Runtime インフラストラクチャに属し、コードから直接使用するものではない型を提供します。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.dll|次の型を提供します。<br /><br /> - ドキュメントレベル カスタマイズでデータ オブジェクトのキャッシュに使用できる <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性と <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> インターフェイス。 詳細については、「[キャッシュ データ](caching-data.md)」を参照してください。<br />- Office ソリューションの ClickOnce インストーラーの最後の手順として追加のインストール手順を実行するために実装できる <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> インターフェイス。 詳細については、「[ClickOnce を使用して Office ソリューションを配置する](deploying-an-office-solution-by-using-clickonce.md)」を参照してください。<br />- Visual Studio Tools for Office runtime によってスローされる例外。<br />- Visual Studio Tools for Office Runtime インフラストラクチャに属するその他の種類。これらは、コードから直接使用するものではありません。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll|次の型を提供します。<br /><br /> - カスタマイズ アセンブリをドキュメントに添付し、ドキュメントでキャッシュされたデータにアクセスするために使用できる <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラス。 詳細については、「[ServerDocument クラスを使用してサーバー上のドキュメントを管理する](managing-documents-on-a-server-by-using-the-serverdocument-class.md)」を参照してください。<br />- ドキュメントレベル カスタマイズでキャッシュされたデータの階層を表すいくつかのクラス。 詳細については、「[サーバー上のドキュメントのデータにアクセスする](accessing-data-in-documents-on-the-server.md)」を参照してください。|

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](includes/net-v45-md.md)] を対象とするプロジェクトは次のアセンブリも参照します。 これらのアセンブリは再頒布可能な [!INCLUDE[vsto_runtime](includes/vsto-runtime-md.md)] に含まれません。 これらはむしろ、ソリューションで展開しなければならない従属アセンブリです。 既定では、プロジェクトのビルド出力フォルダーにコピーされます (これらのアセンブリの **[ローカル コピー]** プロパティは **True** に設定されます)。 ClickOnce を使用してプロジェクトを展開する場合、これらのアセンブリは生成されたパッケージに含まれます。

|アセンブリ名|説明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v4.0.Utilities.dll|VSTO アドイン プロジェクトで生成される `ThisAddIn` クラスとすべてのプロジェクトで生成される Ribbon クラスの基底クラスを提供します。|
|Microsoft.Office.Tools.Excel.v4.0.Utilities.dll|次の型を提供します。<br /><br /> - Excel のドキュメントレベル プロジェクトで生成される `ThisWorkbook` クラスと `Sheet` クラスの基底クラス。<br />- Excel プロジェクトのワークシートで使用できる Windows フォーム コントロール。|
|Microsoft.Office.Tools.Outlook.v4.0.Utilities.dll|Outlook プロジェクトで生成される `ThisAddIn` とフォーム領域クラスの基本クラスを提供します。|
|Microsoft.Office.Tools.Word.v4.0.Utilities.dll|次の型を提供します。<br /><br /> - Word の文書レベル プロジェクトで生成される `ThisDocument` クラスの基底クラス。<br />- Word プロジェクトの文書で使用できる Windows フォーム コントロール。|

## <a name="assemblies-in-the-office-extensions-for-the-net-framework-35"></a>.NET Framework 3.5 用の Office 拡張機能のアセンブリ
 次の表は、.NET Framework 3.5 の Office 拡張機能に含まれているアセンブリをまとめたものです。 これらのアセンブリの名前空間とクラスの詳細については、Visual Studio 2008 ドキュメントの参照セクション [http://go.microsoft.com/fwlink/?LinkId=160658](managed-reference-office-development-in-visual-studio.md) を参照してください。

|アセンブリ名|説明|
|-------------------|-----------------|
|Microsoft.Office.Tools.Common.v9.0.dll|次の型を提供します。<br /><br /> - VSTO アドイン用の Microsoft.Office.Tools.AddIn 基底クラス。<br />- リボンのカスタマイズとスマート タグを作成するためのクラス。 **注:** スマート タグは、[!INCLUDE[Excel_14_short](includes/excel-14-short-md.md)] および [!INCLUDE[Word_14_short](includes/word-14-short-md.md)] で非推奨になっています。<br />- ドキュメント レベルのカスタマイズの操作ウィンドウと VSTO アドインのカスタム作業ウィンドウを作成するためのクラス。|
|Microsoft.Office.Tools.Excel.v9.0.dll|Excel ソリューションのホスト項目とホスト コントロールを提供します。 詳細については、「[拡張オブジェクトを使用して Excel を自動化する](automating-excel-by-using-extended-objects.md)」を参照してください。|
|Microsoft.Office.Tools.Outlook.v9.0.dll|Outlook VSTO アドインでカスタム フォーム領域の作成に使用できるクラスを提供します。|
|Microsoft.Office.Tools.Word.v9.0.dll|Word ソリューションのホスト項目とホスト コントロールを提供します。 詳細については、「[拡張オブジェクトを使用して Word を自動化する](automating-word-by-using-extended-objects.md)」を参照してください。|
|Microsoft.Office.Tools.v9.0.dll|次の型を提供します。<br /><br /> - ドキュメントレベル カスタマイズでホスト コントロールのデータ バインディング機能を提供する [RemoteBindableComponent](/previous-versions/visualstudio/visual-studio-2008/bb546360(v=vs.90)) クラス。<br />- Visual Studio Tools for Office Runtime インフラストラクチャに属するその他の種類。これらは、コードから直接使用するものではありません。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v9.0.dll|次の型を提供します。<br /><br /> - ドキュメントレベル カスタマイズでデータ オブジェクトのキャッシュに使用できる <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性と <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> インターフェイス。 詳細については、「[キャッシュ データ](caching-data.md)」を参照してください。<br />- Visual Studio Tools for Office runtime によってスローされる例外。<br />- Visual Studio Tools for Office Runtime インフラストラクチャに属するその他の種類。これらは、コードから直接使用するものではありません。|
|Microsoft.VisualStudio.Tools.Applications.Runtime.v10.0.dll|Office ソリューションの ClickOnce インストーラーの最後の手順として追加のインストール手順を実行するために実装できる <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> インターフェイスを提供します。 詳細については、「[高度な Office ソリューションの配置](/previous-versions/visualstudio/visual-studio-2010/dd234217(v=vs.100))」を参照してください。|
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.v10.0.dll|次の型を提供します。<br /><br /> - プログラミングでカスタマイズ アセンブリをドキュメントに添付し、ドキュメントでキャッシュされたデータにアクセスするために使用できる <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラス。 詳細については、「[ServerDocument クラスを使用してサーバー上のドキュメントを管理する](managing-documents-on-a-server-by-using-the-serverdocument-class.md)」を参照してください。<br />- ドキュメントレベル カスタマイズでキャッシュされたデータの階層を表すいくつかのクラス。 詳細については、「[サーバー上のドキュメントのデータにアクセスする](accessing-data-in-documents-on-the-server.md)」を参照してください。|
|Microsoft.VisualStudio.Tools.Office.Runtime.v10.0.dll|次の型を提供します。<br /><br /> - .NET Framework 3.5 を対象とする Office ソリューションに信頼を与えるユーザー信頼リスト エントリの作成に使用できる Microsoft.VisualStudio.Tools.Office.Runtime.Security.AddInSecurityEntry クラスと Microsoft.VisualStudio.Tools.Office.Runtime.Security.UserInclusionList クラス。<br />- Visual Studio Tools for Office Runtime インフラストラクチャに属するその他の種類。これらは、コードから直接使用するものではありません。|

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio Tools for Office ランタイムの概要](visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office ランタイムのインストール シナリオ](visual-studio-tools-for-office-runtime-installation-scenarios.md)
