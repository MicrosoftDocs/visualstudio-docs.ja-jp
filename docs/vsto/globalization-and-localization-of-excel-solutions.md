---
title: Excel ソリューションのグローバリゼーションとローカリゼーション
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], configuring
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ade59e757778ac7858732f5bf9880b9f88eacd69
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567458"
---
# <a name="globalization-and-localization-of-excel-solutions"></a>Excel ソリューションのグローバリゼーションとローカリゼーション
  ここでは、Windows に英語以外の言語を設定しているコンピューターで実行される Microsoft Office Excel ソリューションにおいて、特に考慮が必要な事項について説明します。 Microsoft Office ソリューションのグローバリゼーションとローカリゼーションは、ほとんどの点で、Visual Studio を使用して他の種類のソリューションを作成する場合と同じです。 一般的な情報は、次を参照してください。 [Globalize とアプリケーションのローカライズ](/visualstudio/ide/globalizing-and-localizing-applications)します。  
  
 既定では、Microsoft Office Excel のホスト コントロールは、マネージド コードを使用して渡されるデータや操作されるデータがすべて英語 (米国) の書式で設定されている限り、Windows のどの地域設定でも正常に動作します。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]を対象にしたプロジェクトでは、この動作は共通言語ランタイム (CLR) によって制御されます。  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="format-data-in-excel-with-various-regional-settings"></a>書式設定データを Excel のさまざまな地域設定  
 日付や通貨など、ロケールに依存する書式設定を持つデータはすべて、Microsoft Office Excel に渡したり、Office プロジェクトのコードからデータを読み込んだりする前に、英語 (米国) のデータ形式 (ロケール ID 1033) を使用して書式設定する必要があります。  
  
 既定では、Visual Studio で Office ソリューションを開発する場合、Excel オブジェクト モデルはロケール ID 1033 によるデータの書式設定を予期します (これは、オブジェクト モデルのロケール ID 1033 へのロック、ともいいます)。 この動作は、Visual Basic for Applications の動作方法と一致します。 ただし、この動作は Office ソリューションで変更できます。  
  
### <a name="understand-how-the-excel-object-model-always-expects-locale-id-1033"></a>Excel オブジェクト モデルが常にロケール ID 1033 を要求する方法を理解します。  
 既定では、Visual Studio を使用して作成する Office ソリューションは、エンド ユーザーのロケール設定の影響を受けません。ロケールは常に英語 (米国) であるかのように動作します。 たとえば、Excel で <xref:Microsoft.Office.Interop.Excel.Range.Value2%2A> プロパティを取得または設定する場合、データはロケール ID 1033 が予期する方法で書式設定する必要があります。 別のデータ書式を使用すると、予期しない結果になる場合があります。  
  
 マネージド コードに渡されるデータや、マネージド コードによって処理されるデータに英語 (米国) の書式を使用した場合でも、Excel では、エンド ユーザーのロケール設定に従って、データが正確に解釈および表示されます。 Excel がデータを正確に書式設定できるのは、マネージド コードによってデータと共にロケール ID 1033 が渡されるからです。このロケール ID は、データが英語 (米国) の書式であることを示し、ユーザーのロケール設定に合わせてデータを再度書式設定する必要があることを示します。  
  
 たとえば、エンド ユーザーの地域オプションがドイツ語 (ドイツ) ロケールに設定されている場合、ユーザーは 2005 年 6 月 29 日という日付が 29.06.2005 として書式設定されると予測します。 ですが、ソリューションがこの日付を文字列として Excel に渡す場合は、英語 (米国) の書式に従って 6/29/2005 と書式設定する必要があります。 セルが日付セルとして書式設定されている場合、Excel はこの日付をドイツ語 (ドイツ) の書式で表示します。  
  
### <a name="pass-other-locale-ids-to-the-excel-object-model"></a>Excel オブジェクト モデルを他のロケール Id を渡す  
 共通言語ランタイム (CLR) は、ロケールに依存するデータを受け入れる Excel オブジェクト モデルのすべてのメソッドとプロパティに対して、自動的にロケール ID 1033 を渡します。 どのオブジェクト モデルへの呼び出しでも、この動作を自動的に変更する方法はありません。 ただし、 <xref:System.Type.InvokeMember%2A> を使用してメソッドを呼び出し、メソッドの *culture* パラメーターにロケール ID を渡すことで、特定のメソッドに別のロケール ID を渡すことができます。  
  
## <a name="localize-document-text"></a>ドキュメントのテキストをローカライズします。  
 プロジェクト内のドキュメントや、テンプレート、ブックには、アセンブリや他のマネージド リソースとは別にローカライズする必要がある静的テキストが含まれていることもあります。 これを簡単に実行するには、ドキュメントのコピーを作成し、そのテキストを Microsoft Office Word または Microsoft Office Excel を使用して翻訳します。 どのドキュメントも同じアセンブリにリンクできるため、コードを変更しなくても、この処理を実行できます。  
  
 この場合でも、ドキュメントのテキストを操作するコードのすべての部分がテキストの言語と一致しているか確認する必要があります。また、ブックマーク、名前付き範囲、および他の表示フィールドが Office ドキュメントの再設定に対応しているか確認する必要もあります。この再設定は、異なる文法やテキストの長さに合わせて調整する場合に必要とされたものです。 ドキュメント テンプレートの比較的簡単なテキストが含まれている場合、リソース ファイルにテキストを格納して、実行時にテキストを読み込みを検討する可能性があります。  
  
### <a name="text-direction"></a>テキストの方向  
 Excel では、テキストが右から左へ表記されるようにワークシートのプロパティを設定できます。 ホスト コントロール、または任意のコントロールを持つ、`RightToLeft`デザイナーに自動的に配置されているプロパティは、実行時にこれらの設定に一致します。 Word の場合、双方向テキスト用のドキュメント設定はありません (テキストの配置を変更できるだけです)。そのため、コントロールをこの設定にマップすることはできません。 ユーザーは、代わりにテキストの配置を各コントロールに設定する必要があります。 コードを記述して、すべてのコントロールでテキストが右から左へ表記されるようにできます。  
  
### <a name="change-culture"></a>カルチャを変更します。  
 ドキュメント レベルのカスタマイズ コードは、通常、Excel のメイン UI スレッドを共有します。そのため、スレッド カルチャに対して行った変更は、そのスレッドで実行されている、すべてのものに影響します。変更はカスタマイズに限定されません。  
  
 Windows フォーム コントロールは、アプリケーション レベルの VSTO アドインがホスト アプリケーションによって起動される前に初期化されます。 このような場合は、カルチャを変更してから UI コントロールを設定する必要があります。  
  
## <a name="install-the-language-packs"></a>言語パックをインストールします。  
 Windows の言語を英語以外に設定している場合は、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] の言語パックをインストールすることにより、Windows と同じ言語で [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] のメッセージを表示できます。 エンド ユーザーが英語以外を設定している Windows でソリューションを実行する場合は、Windows と同じ言語でランタイム メッセージを表示するために、適切な言語パックが必要になります。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]言語パックはから利用可能な[Microsoft ダウンロード センター](http://www.microsoft.com/downloads)します。  
  
 さらに、ClickOnce メッセージ用に、再頒布可能な .NET Framework Language Pack が必要です。 .NET Framework 言語パックはから利用可能な[Microsoft ダウンロード センター](http://www.microsoft.com/downloads)します。  
  
## <a name="regional-settings-and-excel-com-calls"></a>地域設定と Excel COM 呼び出し  
 管理対象のクライアントが COM オブジェクトのメソッドを呼び出して、カルチャ固有の情報を渡す必要がある場合、現在のスレッド ロケールに一致する <xref:System.Globalization.CultureInfo.CurrentCulture%2A> (ロケール) が使用されます。 現在のスレッド ロケールは、既定では、ユーザーの地域設定から継承されます。 ただし、Visual Studio の Office 開発ツールを使用して作成された Excel ソリューションから Excel オブジェクト モデルを呼び出す場合は、自動的に英語 (米国) のデータ形式 (ロケール ID 1033) が Excel オブジェクト モデルに渡されます。 日付や通貨など、ロケールに依存する書式設定を持つデータはすべて、Microsoft Office Excel に渡したり、プロジェクトのコードからデータを読み込んだりする前に、英語 (米国) のデータ形式を使用して書式設定する必要があります。  
  
## <a name="considerations-for-storing-data"></a>データを格納するための考慮事項  
 アプリケーションが Excel ワークシートの式などのデータを、厳密に型指定されたオブジェクトではなくリテラル文字列 (ハードコーディングされた) に格納している場合は、データの正しい解釈や表示に問題が発生する可能性があることも考慮する必要があります。 カルチャに依存しないスタイルか、英語 (米国) (LCID 値 1033) のスタイルを想定して書式設定されたデータを使用する必要があります。  
  
### <a name="applications-that-use-string-literals"></a>文字列リテラルを使用するアプリケーション  
 ハードコーディングされた有効な値には、英語 (米国) 形式で記述された日付リテラルや、ローカライズされた関数名を含む Excel ワークシートの式が含まれます。 また、"1,000" などの数値を含むハードコーディングされた文字列がこれに該当する場合もあります。一部のカルチャでは、この数値は "1000" と解釈されますが、それ以外のカルチャでは "1.0" の意味になります。 誤った形式で数値を計算したり比較したりすると、結果のデータは不適切なものになります。  
  
 Excel では、文字列の解釈は文字列と共に渡された LCID に従って行われます。 これは、文字列の書式と渡された LCID が対応しない場合に、問題になることがあります。 Visual Studio の Office 開発ツールを使用して作成した Excel ソリューションでは、LCID 1033 (en-US) を使用して、すべてのデータを渡します。 Excel は、地域設定と Excel ユーザー インターフェイス言語に従って、データを表示します。 Visual Basic for Applications (VBA) も同じ方法で動作します。文字列は en-US として書式設定され、ほとんどの場合、VBA は LCID として 0 (ニュートラル言語) を渡します。 など、次の VBA コードは、現在のユーザー ロケール設定に従って 2004 年 5 月 12 日の正しく書式設定された値を表示します。  
  
```vb
'VBA  
Application.ActiveCell.Value2 = "05/12/04"  
```  
  
 同じコードを Visual Studio の Office 開発ツールを使用して作成したソリューションで使用し、COM 相互運用機能を通じて Excel に渡すと、日付の書式を en-US スタイルに設定した場合と同じ結果が得られます。  
  
 例えば:  
  
 [!code-vb[Trin_VstcoreCreatingExcel#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#6)]
 [!code-csharp[Trin_VstcoreCreatingExcel#6](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#6)]  
  
 可能な限り、リテラル文字列ではなく、厳密に型指定されたデータを使用する必要があります。 たとえば、日付をリテラル文字列ではなく <xref:System.Double>として格納し、操作時に <xref:System.DateTime> オブジェクトに変換します。  
  
 次に示すコードの例では、ユーザーがセル A5 に入力した日付を取得し、 <xref:System.Double>として格納します。次に、それを <xref:System.DateTime> オブジェクトに変換して、セル A7 に表示します。 セル A7 には、日付を表示するための書式が設定されている必要があります。  
  
 [!code-vb[Trin_VstcoreCreatingExcel#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb#7)]
 [!code-csharp[Trin_VstcoreCreatingExcel#7](../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs#7)]  
  
### <a name="excel-worksheet-functions"></a>Excel ワークシート関数  
 Excel では、ワークシート関数の名前が内部で変換されます。これは Excel の、ほぼすべての言語バージョンに共通しています。 ただし、潜在的な言語と COM 相互運用の問題の原因は、コードでは、英語のみの関数名を使用することをお勧めします。  
  
### <a name="applications-that-use-external-data"></a>外部データを使用するアプリケーション  
 レガシ システムからエクスポートされたコンマ区切り値を含むファイル (CSV ファイル) などの外部データを開いたり使用したりするコードは、ファイルが en-US 以外の形式でエクスポートされると影響が出る場合があります。 データベースへのアクセスはすべての値がバイナリ形式なので影響を受けないと考えられますが、データベースで日付が文字列として保存されていたり、バイナリ形式を使用しない操作が実行されたりする場合は、この限りではありません。 また、Excel のデータを使用して SQL クエリを作成する場合、使用する関数によってはデータを en-US 形式にする必要があります。  
  
## <a name="see-also"></a>関連項目  
 [方法: Office multilingual user Interface](../vsto/how-to-target-the-office-multilingual-user-interface.md)   
 [設計および Office ソリューションの作成](../vsto/designing-and-creating-office-solutions.md)   
 [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)  
  
  