---
title: .NET Framework を対象とする Office プロジェクトのデザインの変更
description: .NET Framework 4 以降を対象とする Office プロジェクトのデザインについて、Visual Studio で導入された変更を説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio 2010, what's new
- what's new [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2bb8f6064bd2c2df55c7d0cf8fea1e25c513da0f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903790"
---
# <a name="changes-to-the-design-of-office-projects-that-target-the-net-framework-4-or-the-net-framework-45"></a>.NET Framework 4 または .NET Framework 4.5 を対象とする Office プロジェクトのデザインの変更点
  [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]以降の Visual Studio では、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする Office プロジェクトのデザインに対していくつかの変更が導入されました。 以前のバージョンの Visual Studio の Office プロジェクトに慣れている場合は、これらの変更内容を確認してから、.NET Framework 4.0 以降のこれらのバージョンを対象とする Office プロジェクトを開発してください。 既定では、Visual Studio 2013 以降を使用して作成したすべてのプロジェクトは、.NET Framework 4.0 以降が対象になります。

 次のセクションでは、これらの Office プロジェクトのデザインの変更について説明します。

## <a name="understand-the-interface-based-design-of-the-visual-studio-2010-tools-for-office-runtime"></a>Visual Studio 2010 Tools for Office Runtime のインターフェイス ベースのデザインについて
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする Office プロジェクトを開発する際に、Visual Studio 2010 Tools for Office Runtime で最もよく使用する型はインターフェイスです。 これは、以前のバージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]からの重大な変更点です。以前のバージョンでは、これらの型はクラスです。 たとえば、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とする場合、 <xref:Microsoft.Office.Tools.Excel.Worksheet> と <xref:Microsoft.Office.Tools.Word.Document> の型はクラスではなくインターフェイスです。 詳細については、「[Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)」を参照してください。

 以前のバージョンの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] で直接インスタンス化できた型の場合は、`Globals.Factory` オブジェクトのメソッドを使用して型のインスタンスを取得できます。 たとえば、<xref:Microsoft.Office.Tools.Excel.SmartTag> インターフェイスを実装するオブジェクトを取得するには、`Globals.Factory.CreateSmartTag` メソッドを使用します。 詳細については、次のトピックを参照してください。

- [.NET Framework 4 または .NET Framework 4.5 に移行する Excel プロジェクトと Word プロジェクトを更新する](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

- [.NET Framework 4 または .NET Framework 4.5 に移行する Office プロジェクトのリボンのカスタマイズを更新する](update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5.md)

- [.NET Framework 4 または .NET Framework 4.5 に移行する Outlook プロジェクトのフォーム領域を更新する](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

### <a name="new-base-classes-in-office-projects"></a>Office プロジェクトの新しい基底クラス
 Visual Studio 2010 Tools for Office Runtime の新しいインターフェイス ベースのデザインは、Office プロジェクトで生成される `ThisDocument`、 `ThisWorkbook`、 `ThisAddIn`などのクラスに影響します。 .NET Framework 3.5 および以前のバージョンのフレームワークを対象とする Office プロジェクトでは、これらの生成されるクラスは、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]、`Microsoft.Office.Tools.Word.Document`、`Microsoft.Office.Tools.Excel.Worksheet` などの `Microsoft.Office.Tools.AddIn` のクラスから派生します。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトでは、これらの [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] クラスがインターフェイスになりました。 そのため、Office プロジェクトで生成されるクラスでは実装を派生できなくなりました。 代わりに、生成されるクラスは、 <xref:Microsoft.Office.Tools.Word.DocumentBase>、 <xref:Microsoft.Office.Tools.Excel.WorksheetBase>、 <xref:Microsoft.Office.Tools.AddInBase>などの新しい基底クラスから派生します。 詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」と「[プログラム ドキュメント レベルのカスタマイズ](../vsto/programming-document-level-customizations.md)」を参照してください。

 基底クラスは、再頒布可能な [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] には含まれません。 代わりに、Visual Studio に含まれるユーティリティ アセンブリに定義されています。 これらのアセンブリは、Office プロジェクトのビルド時に出力フォルダーにコピーし、ソリューションと共に配置する必要があります。 ユーティリティ アセンブリについて詳しくは、「[Visual Studio Tools for Office Runtime のアセンブリ](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)」をご覧ください。

## <a name="breaking-changes-in-office-projects-that-are-retargeted-to-the-net-framework-4"></a>.NET Framework 4 に再ターゲットされた Office プロジェクトの互換性に影響する変更点
 次の表では、 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に対象が変更された Office プロジェクトの互換性に影響する主な変更点を示します。 詳細については、「[.NET Framework 4 移行への Office ソリューションの移行](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)」を参照してください。

|互換性に影響する変更点|結果|
|---------------------|-----------------|
|<xref:System.Security.SecurityTransparentAttribute> が Office プロジェクトで使用またはサポートされなくなりました。|Visual Studio 2008 からアップグレードする Office プロジェクトの AssemblyInfo コード ファイルからこの属性を削除する必要があります。 詳細については、[.NET Framework 4 または .NET Framework 4.5 に移行する Office プロジェクトの実行に必要な変更](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)に関するページを参照してください。|
|**ExcelLocale1033Attribute** が Excel プロジェクトで使用またはサポートされなくなりました。|Excel プロジェクトの *AssemblyInfo* コード ファイルからこの属性を削除する必要があります。 詳細については、「[.NET Framework 4 または .NET Framework 4.5 に移行する Excel プロジェクトと Word プロジェクトを更新する](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)」を参照してください。|
|**リボン (ビジュアルなデザイナー)** プロジェクト項目のプログラミング モデルが変更されました。|プロジェクトのすべてのリボン項目の分離コード ファイルを変更する必要があります。 また、実行時にリボン コントロールをインスタンス化するコード、リボン イベントを処理するコード、またはリボン コンポーネントの位置をプログラムによって設定するコードをすべて変更する必要があります。 詳細については、[.NET Framework 4 または .NET Framework 4.5 に移行する Office プロジェクトのリボンのカスタマイズの更新](update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5.md)に関するページを参照してください。|
|Outlook フォーム領域のプログラミング モデルが変更されました。|プロジェクトのフォーム領域の分離コード ファイル、および実行時に特定のフォーム領域クラスをインスタンス化するすべてのコードを変更する必要があります。 詳細については、[.NET Framework 4 または .NET Framework 4.5 に移行する Outlook プロジェクトのフォーム領域の更新](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)に関するページを参照してください。|
|Excel プロジェクトと Word プロジェクトでのスマート タグのプログラミング モデルが変更されました。 スマート タグは、[!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] および [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)] で非推奨とされます。|ソリューションでスマート タグを使用している場合は、プロジェクトをビルドするときにエラーが発生します。 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] および [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)] ではスマート タグが非推奨とされているため、[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 以降でソリューションをテストおよびデバッグするには、タグを削除する必要があります。|
|`GetVstoObject` メソッドと `HasVstoObject` メソッドの構文が変更されました。|プライマリ相互運用機能アセンブリ (PIA) からネイティブ オブジェクトでこれらのメソッドにアクセスするときに、`Globals.Factory` オブジェクトをメソッドに渡す必要があります。または、プロジェクトの `Globals.Factory` プロパティによって返されるオブジェクトでこれらのメソッドにアクセスすることもできます。 詳細については、「[.NET Framework 4 または .NET Framework 4.5 に移行する Excel プロジェクトと Word プロジェクトを更新する](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)」を参照してください。|
|Word コンテンツ コントロールのイベントが新しいデリゲートに関連付けられています。|Word コンテンツ コントロールのイベントを処理するすべてのコードを変更し、新しいデリゲートを指定する必要があります。 詳細については、「[.NET Framework 4 または .NET Framework 4.5 に移行する Excel プロジェクトと Word プロジェクトを更新する](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)」を参照してください。|
|`OLEObject` クラスと `OLEControl` クラスの名前が変更されました。|これらのクラスのインスタンスを使用するすべてのコードを変更し、代わりに <xref:Microsoft.Office.Tools.Excel.ControlSite> オブジェクトまたは <xref:Microsoft.Office.Tools.Word.ControlSite> オブジェクトを使用する必要があります。 詳細については、「[.NET Framework 4 または .NET Framework 4.5 に移行する Excel プロジェクトと Word プロジェクトを更新する](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)」を参照してください。|
|ホスト項目クラス (`ThisWorkbook`、`Sheet`*n*、`ThisDocument`、`ThisAddIn`) では、オーバーライドできる `Dispose` メソッドが提供されなくなりました。|`Dispose` メソッド オーバーライドのすべてのコードをホスト項目クラス (`Shutdown` など) の `ThisAddIn_Shutdown` イベント ハンドラーに移動し、ホスト項目クラスから `Dispose` メソッド オーバーライドを削除する必要があります。|

## <a name="see-also"></a>関連項目
- [Office ソリューションを .NET Framework 4 以降に移行する](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [Office 開発の新機能](/previous-versions/86bkz018(v=vs.110))
- [Visual Studio Tools for Office ランタイムの概要](../vsto/visual-studio-tools-for-office-runtime-overview.md)