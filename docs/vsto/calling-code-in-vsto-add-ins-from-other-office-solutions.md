---
title: 他の Office ソリューションから VSTO アドインのコードを呼び出す
description: 他の Microsoft Office ソリューションを含む他のソリューションに VSTO アドイン内のオブジェクトを公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 2519c9d1a22eb6f5577a258fb9b465cfd7caafc2
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826981"
---
# <a name="call-code-in-vsto-add-ins-from-other-office-solutions"></a>他の Office ソリューションから VSTO アドインのコードを呼び出す
  VSTO アドイン内のオブジェクトは、他の Microsoft Office ソリューションを含む、他のソリューションに公開できます。 このことは、VSTO アドインが他のソリューションで使用可能なサービスを含む場合に便利です。 たとえば、Web サービスから受け取る財務データについて計算を実行する、Microsoft Office Excel 向けの VSTO アドインがある場合、他のソリューションでは、実行時に Excel VSTO アドインを呼び出すことでこれらの計算を実行できます。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 この処理には主に 2 つの手順があります。

- VSTO アドインで、オブジェクトを他のソリューションに公開します。

- もう 1 つのソリューションで、VSTO アドインにより公開されたオブジェクトにアクセスし、オブジェクトのメンバーを呼び出します。

## <a name="types-of-solutions-that-can-call-code-in-an-add-in"></a>アドイン内のコードを呼び出すことができるソリューションの種類
 VSTO アドイン内のオブジェクトは次の種類のソリューションに公開できます。

- VSTO アドインと同じアプリケーション プロセスに読み込まれるドキュメント内の Visual Basic for Applications (VBA) コード。

- VSTO アドインと同じアプリケーション プロセスに読み込まれるドキュメント レベルのカスタマイズ。

- Visual Studio に含まれる Office プロジェクト テンプレートを使用して作成された他の VSTO アドイン。

- COM VSTO アドイン (つまり、 <xref:Extensibility.IDTExtensibility2> インターフェイスを直接実装する VSTO アドイン)。

- VSTO アドインとは異なるプロセスで実行中の任意のソリューション (こうした種類のソリューションは *アウト プロセス クライアント* とも呼ばれます)。 これらには、Windows フォームまたはコンソール アプリケーションなど、Office アプリケーションを自動化するアプリケーションと、異なるプロセスに読み込まれる VSTO アドインが含まれます。

## <a name="expose-objects-to-other-solutions"></a>他のソリューションにオブジェクトを公開する
 VSTO アドイン内のオブジェクトを他のソリューションに公開するには、VSTO アドインで次の手順を実行します。

1. 他のソリューションに公開するクラスを定義します。

2. <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> クラスの `ThisAddIn` メソッドをオーバーライドします。 他のソリューションに公開するクラスのインスタンスを返します。

### <a name="define-the-class-you-want-to-expose-to-other-solutions"></a>他のソリューションに公開するクラスを定義する
 少なくとも、公開するクラスはパブリックであり、 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性の設定は **true** であり、 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) インターフェイスを公開する必要があります。

 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) インターフェイスを公開する推奨方法は以下の手順を実行することです。

1. 他のソリューションに公開するメンバーを宣言するインターフェイスを定義します。 このインターフェイスは、VSTO アドイン プロジェクトで定義できます。 ただし、クラスを非 VBA ソリューションに公開する場合、このインターフェイスを別のクラス ライブラリ プロジェクトで定義することを推奨します。そうすることで、VSTO アドインを呼び出すソリューションは VSTO アドイン プロジェクトを参照することなく、インターフェイスを参照できます。

2. <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性をこのインターフェイスに適用し、この属性を **true** に設定します。

3. クラスを変更して、このインターフェイスを実装します。

4. <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性をクラスに適用し、この属性を <xref:System.Runtime.InteropServices.ClassInterfaceType> 列挙体の **None** 値に設定します。

5. このクラスをアウト プロセス クライアントに公開する場合、次も実行する必要がある可能性があります。

   - <xref:System.Runtime.InteropServices.StandardOleMarshalObject>からクラスを派生させます。 詳細については、「[アウト プロセス クライアントにクラスを公開する](#outofproc)」を参照してください。

   - インターフェイスを定義するプロジェクトで、 **[COM の相互運用機能に登録]** プロパティを設定します。 このプロパティは、クライアントで事前バインディングを使用して VSTO アドインを呼び出せるようにする場合にのみ必要です。

   次のコード例は、他のソリューションによって呼び出し可能な `AddInUtilities` メソッドを持つ、 `ImportData` クラスを示します。 より大きなチュートリアルのコンテキストでこのコードを確認するには、「[チュートリアル: VSTO アドイン内のコードを VBA から呼び出す](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)」を参照してください。

   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs" id="Snippet3":::
   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb" id="Snippet3":::

### <a name="expose-classes-to-vba"></a>VBA にクラスを公開する
 上記の手順を実行すると、VBA コードはインターフェイス内で宣言するメソッドのみを呼び出すことができます。 VBA コードは、 <xref:System.Object>など、クラスが基本クラスから取得するメソッドを含め、クラス内の他のメソッドを呼び出すことはできません。

 代わりに、<xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性を <xref:System.Runtime.InteropServices.ClassInterfaceType> 列挙体の AutoDispatch または AutoDual 値に設定し、[IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) インターフェイスを公開できます。 インターフェイスを公開する場合、メソッドを別のインターフェイスで宣言する必要はありません。 ただし、VBA コードは、 <xref:System.Object>など、基本クラスから取得されるメソッドを含め、クラス内の任意のパブリックおよび非静的メソッドを呼び出すことができます。 さらに、事前バインディングを使用するアウト プロセス クライアントはクラスを呼び出すことができません。

### <a name="expose-classes-to-out-of-process-clients"></a><a name="outofproc"></a> アウト プロセス クライアントにクラスを公開する
 VSTO アドイン内のクラスをアウト プロセス クライアントに公開する場合、 <xref:System.Runtime.InteropServices.StandardOleMarshalObject> からクラスを派生させ、アウト プロセス クライアントが公開された VSTO アドイン オブジェクトを呼び出せるようにする必要があります。 そうしないと、アウト プロセス クライアントで公開されたオブジェクトのインスタンスを取得しようとしたとき、予期せずに失敗する可能性があります。

 この失敗は、Office アプリケーションのオブジェクト モデルのすべての呼び出しはメイン UI スレッド上で実行される必要があるのに対して、アウト プロセス クライアントからオブジェクトへの呼び出しは任意の RPC (リモート プロシージャ コール) スレッドに到着するために発生します。 .NET Framework における COM マーシャリング機構はスレッドを切り替えず、メイン UI スレッドではなく、受信 RPC スレッド上のオブジェクトに呼び出しをマーシャリングすることを試みます。 オブジェクトが <xref:System.Runtime.InteropServices.StandardOleMarshalObject>から派生するクラスのインスタンスである場合、オブジェクトへの受信呼び出しは、公開されたオブジェクトが作成されたスレッド、つまりホスト アプリケーションのメイン UI スレッドに自動的にマーシャリングされます。

 Office ソリューションにおけるスレッドの使用法の詳細については、「[Office でのスレッドのサポート](../vsto/threading-support-in-office.md)」を参照してください。

### <a name="override-the-requestcomaddinautomationservice-method"></a>RequestComAddInAutomationService メソッドをオーバーライドする
 次のコード例は、VSTO アドイン内の <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> クラスで `ThisAddIn` をオーバーライドする方法を示します。 この例では、他のソリューションに公開する `AddInUtilities` という名前のクラスを定義済みであると想定しています。 より大きなチュートリアルのコンテキストでこのコードを確認するには、「[チュートリアル: VSTO アドイン内のコードを VBA から呼び出す](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)」を参照してください。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb" id="Snippet1":::

 VSTO アドインが読み込まれると、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] は <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> メソッドを呼び出します。 ランタイムでは、返されるオブジェクトを、VSTO アドインを表す <xref:Microsoft.Office.Core.COMAddIn> オブジェクトの COMAddIn.Object プロパティに割り当てます。 この <xref:Microsoft.Office.Core.COMAddIn> オブジェクトは他の Office ソリューションおよび Office を自動化するソリューションで利用できます。

## <a name="access-objects-from-other-solutions"></a>他のソリューションからオブジェクトにアクセスする
 VSTO アドインで公開されたオブジェクトを呼び出すには、クライアント ソリューションで以下の手順を実行します。

1. 公開された VSTO アドインを表す <xref:Microsoft.Office.Core.COMAddIn> オブジェクトを取得します。 クライアントは、ホスト Office アプリケーションのオブジェクト モデル内の `Application.COMAddIns` プロパティを使用して、使用可能なすべての VSTO アドインにアクセスできます。

2. <xref:Microsoft.Office.Core.COMAddIn> オブジェクトの COMAddIn.Object プロパティにアクセスします。 このプロパティは VSTO アドインから公開されたオブジェクトを返します。

3. 公開されたオブジェクトのメンバーを呼び出します。

   COMAddIn.Object プロパティの戻り値を使用する方法は VBA クライアントと非 VBA クライアントで異なります。 アウト プロセス クライアントの場合、可能性のある競合状態を避けるために追加のコードが必要です。

### <a name="access-objects-from-vba-solutions"></a>VBA ソリューションからオブジェクトにアクセスする
 次のコード例は、VBA を使用して、VSTO アドインにより公開されたメソッドを呼び出す方法を示しています。 この VBA マクロでは、**ExcelImportData** という名前の VSTO アドインで定義される `ImportData` という名前のメソッドを呼び出します。 より大きなチュートリアルのコンテキストでこのコードを確認するには、「[チュートリアル: VSTO アドイン内のコードを VBA から呼び出す](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)」を参照してください。

```vb
Sub CallVSTOMethod()
    Dim addIn As COMAddIn
    Dim automationObject As Object
    Set addIn = Application.COMAddIns("ExcelImportData")
    Set automationObject = addIn.Object
    automationObject.ImportData
End Sub
```

### <a name="access-objects-from-non-vba-solutions"></a>非 VBA ソリューションからオブジェクトにアクセスする
 非 VBA ソリューションでは、実装されるインターフェイスに COMAddIn.Object プロパティ値をキャストする必要があり、その後、インターフェイス オブジェクト上で公開されたメソッドを呼び出すことができます。 次のコード例は、Visual Studio に含まれる Office Developer Tools を使用して作成された異なる VSTO アドインから `ImportData` メソッドを呼び出す方法を示します。

```vb
Dim addIn As Office.COMAddIn = Globals.ThisAddIn.Application.COMAddIns.Item("ExcelImportData")
Dim utilities As ExcelImportData.IAddInUtilities = TryCast( _
    addIn.Object, ExcelImportData.IAddInUtilities)
utilities.ImportData()
```

```csharp
object addInName = "ExcelImportData";
Office.COMAddIn addIn = Globals.ThisAddIn.Application.COMAddIns.Item(ref addInName);
ExcelImportData.IAddInUtilities utilities = (ExcelImportData.IAddInUtilities)addIn.Object;
utilities.ImportData();
```

 この例で、COMAddIn.Object プロパティの値を `IAddInUtilities` インターフェイスではなく `AddInUtilities` クラスにキャストしようとすると、コードによって <xref:System.InvalidCastException> がスローされます。

## <a name="see-also"></a>関連項目
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [チュートリアル : VSTO アドイン内のコードを VBA から呼び出す](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [Office ソリューションを開発する](../vsto/developing-office-solutions.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [機能拡張インターフェイスを使用した UI 機能のカスタマイズ](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
